# Buổi 2 — ASP.NET Core pipeline và API design (tóm tắt)

## A. Pipeline
- Kestrel → HttpContext → middleware lồng nhau (búp bê Nga) → endpoint; response đi ngược. Không gọi `next` = short-circuit.
- Thứ tự: ExceptionHandler (ngoài cùng) → HttpsRedirection → Routing (chọn endpoint, lộ metadata) → CORS → AuthN → AuthZ → RateLimiter → endpoints.
- Exception handler chỉ bắt lỗi của lớp **bên trong** nó. Với `WebApplication`, endpoint luôn tự gắn cuối pipeline → đặt handler sau `MapControllers` vẫn bắt lỗi controller nhưng không bắt lỗi middleware trước nó (dễ lọt).
- AuthZ trước AuthN → `ctx.User` anonymous → "token đúng mà vẫn 401".
- Middleware class = singleton → inject Scoped qua tham số `InvokeAsync` (captive dependency).
- **"Middleware lo HTTP, Filter lo Action."** Middleware: mọi request (kể cả 401/404/429), chỉ thấy HttpContext → exception, correlation/tracing, auth, rate limit. Filter: chỉ action MVC, biết action + args đã bind → validate, audit, hash callback provider. Business logic → service.
- Hash Pragmatic: filter cho controller callback; body là stream đọc một lần → resource filter (trước model binding) + `EnableBuffering`, hoặc `Request.Form`. Action filter chỉ thấy object đã bind → serialize lại có thể sai hash.
- Correlation/timing: middleware **đầu tiên**; .NET 8 dùng W3C traceparent + OpenTelemetry, metric `http.server.request.duration`.

## B. Exception handling
- "Exception cho chuyện bất ngờ, Result cho chuyện bình thường" (thiếu số dư là chuyện bình thường). Domain exception cũng được nếu nêu trade-off (chi phí stack trace, goto ẩn, log bẩn).
- Status: 400 validation, 401/403, 404, 409 conflict/đã claim, **422 vi phạm luật nghiệp vụ (thiếu số dư)**, 429, 500, 503 + Retry-After.
- **Callback provider:** trả theo spec provider (thường 200 + mã lỗi riêng), không phải ProblemDetails.
- ProblemDetails (RFC 9457): type/title/status/detail/instance + `errorCode` ổn định + `traceId`. 500 không lộ `ex.Message`/stack.
- .NET 8: `AddProblemDetails`, `IExceptionHandler` (trả false để chuyển tiếp), `UseStatusCodePages`. 4xx log Warning, 5xx Error + alert.

## C1. Cấu trúc API
- Vertical slice cho application, Domain chung cho luật, Infrastructure ở rìa. Không giáo điều Clean Architecture.
- Luật nghiệp vụ ở Domain (`wallet.Debit()`), handler điều phối, được dùng DbContext trực tiếp.
- **Repository: "EF thì khỏi bọc, Dapper thì nên bọc, nhiều nguồn thì phải bọc."** Không `IRepository<T>` generic. Repository cụ thể khi: Dapper/SP (gom tên SP có version), nhiều store (SQL + Cosmos + Redis), dịch lỗi UNIQUE (2627/2601) thành "duplicate".
- Không trả EF entity ra API: lộ dữ liệu, **over-posting** (`balance`), khoá schema, vòng tham chiếu/lazy N+1.
- DIP: interface do **tầng nghiệp vụ** định nghĩa (`IWalletGateway`), hạ tầng triển khai (Nexus). Phân biệt abstraction thật vs interface chỉ để mock.
- **Dapper** = micro-ORM NuGet bên thứ ba (StackExchange), extension method trên `IDbConnection`; bạn viết SQL, nó map (IL được cache). Connection vẫn là ADO.NET provider. Bẫy: nối chuỗi (injection), quên truyền `transaction`, `IN` lớn (giới hạn 2.100 tham số → TVP), buffered mặc định, `nvarchar` vs `varchar` mất index seek (`DbString IsAnsi`). EF Core 8 `SqlQuery<T>` map được SQL thô.

> "With EF Core I usually don't add a repository — DbSet already is one and DbContext is a unit of work. With Dapper and stored procedures, as on PlaySweeps, a specific repository keeps SP names and mapping in one place, hides which store the data lives in, and translates unique-key violations into a domain result."

## C2. REST, idempotency, versioning, pagination
- **POST tạo resource:** 201 Created + header `Location` + body. Validate → 400 ProblemDetails. Đã tồn tại → 409 (hoặc trả lại resource nếu là retry cùng Idempotency-Key).
- **Idempotent theo HTTP:** GET, PUT, DELETE (và HEAD/OPTIONS) idempotent; POST, PATCH không. Idempotent ≠ safe (GET safe, DELETE không safe).
- **Idempotency-Key header** (kiểu Stripe): client sinh UUID; server lưu (key, user, hash body, response) với UNIQUE; trùng key + cùng body → replay response; trùng key + khác body → 422; đang xử lý → 409. Giữ ~24h (API client) — khác ledger ví (giữ vĩnh viễn).
- **Versioning:** URL (`/v1/`) dễ nhìn/cache/route; header/media type gọn URL nhưng khó debug. Public API → URL. Breaking change: xoá/đổi tên field, đổi kiểu, thêm field bắt buộc ở request, đổi ý nghĩa/status code, đổi enum. Non-breaking: thêm field optional/response. Client phải **tolerant reader** (bỏ qua field lạ). Deprecation: header `Deprecation`/`Sunset`, đo traffic theo version, báo trước 6–12 tháng. Package `Asp.Versioning.Http/Mvc`.
- **Pagination:** offset (`OFFSET 10000`) phải quét bỏ 10k dòng → chậm dần; insert giữa chừng → trùng/sót. **Keyset/cursor**: `WHERE (CreatedAt, Id) < (@c, @id) ORDER BY CreatedAt DESC, Id DESC LIMIT 20`, cursor opaque (base64), index `(PlayerId, CreatedAt DESC, Id DESC)`. Sort phải **xác định** (thêm Id làm tie-breaker). Offset ok cho admin cần nhảy trang; keyset cho feed/lịch sử giao dịch/infinite scroll. Tránh `COUNT(*)` mỗi trang trên bảng lớn.
