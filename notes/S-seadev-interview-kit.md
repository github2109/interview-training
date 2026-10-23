# SEADEV C# Developer (ShedPro Ops Hub) — bộ kiến thức cho vòng Tech (Solution Architect + PO)

Cập nhật 2026-10-23, theo JD Hiệp dán (bản đăng trên dtalent). Giải thích tiếng Việt, câu trả lời mẫu tiếng Anh.
Tài liệu gốc chi tiết: `job-seadev.md`, `plan-joblogic-3-buoi.md`, `context/joblogic.md`, `notes/J-joblogic-architecture.md`, `notes/J-multitenant-deep.md`, `notes/01..03`.

---

## 0. Đánh giá: training hiện tại đã đủ chưa?

### JD bản mới khác bản đã lưu (13/10) ở đâu
| Điểm | Bản cũ | Bản dtalent | Hệ quả |
|---|---|---|---|
| Kinh nghiệm C#/.NET | ≥ 3 năm | **≥ 4 năm** | Tính từ intern 07/2022 → ~4 năm 3 tháng; full-time từ 12/2022 → ~3 năm 10 tháng. Nói "about four years of professional experience, mostly .NET on the backend". Đừng tự nói "3 năm". |
| Kiến trúc | "design pattern" | "clean, **testable**, well-structured code, **solid architectural patterns** để hệ thống **stable and scalable**" | SA sẽ hỏi layering, SOLID, DI, testability, scale. |
| Thái độ | — | "**learn quickly and adapt** to new tools" | Chuẩn bị 1 câu chuyện học nhanh (Socure tiếp quản, AWS ở Altar, Rive). |
| Vai trò | tiếp quản từ partner Mỹ | giữ nguyên + "**leading** new feature development" | Câu chuyện feature lead (Quest Engine V2, TDD). |

### Bảng đối chiếu JD ↔ những gì đã ôn
| Yêu cầu JD | Đã ôn | Trạng thái | Thiếu |
|---|---|---|---|
| C#, .NET, .NET Core | Buổi 1 async/DI | ✅ khá | C# nâng cao (record, pattern matching, LINQ), GC/IDisposable (Buổi 6 chưa học) |
| ASP.NET **MVC** và/hoặc Web API | Buổi 2 pipeline/REST | 🟡 Web API ok | **MVC chưa học**: Razor, model binding, validation, anti-forgery, over-posting, filter, ViewModel |
| AWS / cloud | map Azure→AWS trong note | 🟡 chỉ có bảng | Chưa luyện nói; cần biết SQS vs SNS, Lambda vs ECS, RDS, S3 presigned URL, IAM role, CloudWatch |
| HTML/CSS/JS, React/Angular/Vue (plus) | kinh nghiệm thật | ✅ | Chỉ cần câu trả lời ngắn |
| **Design patterns + refactoring** | chưa có buổi nào | ❌ | **Lỗ hổng lớn nhất.** Strategy, State, Factory, Specification, Decorator, Repository/UoW; code smell; refactoring an toàn |
| Readable, maintainable code | rải rác | 🟡 | SOLID, clean code, code review checklist |
| Git | — | ❌ (dễ) | Branching, rebase vs merge, PR, cherry-pick hotfix, revert |
| Agile | — | ❌ (dễ) | Scrum ceremony, story/AC, estimate, DoD, làm với PM |
| RESTful API design | Buổi 2 C2 | ✅ (bỏ bài kiểm tra) | Ôn nhanh 5 câu chờ sẵn trong `progress.md` |
| Unit test (plus) | kinh nghiệm thật | ❌ chưa ôn | Test pyramid, mock gì/không mock gì, test legacy, integration test |
| English (plus) | đang luyện PTE | 🟡 | Luyện nói các câu mẫu bên dưới |
| **Tiếp quản code partner Mỹ** | trong plan Joblogic Buổi 3 | ❌ chưa học | Characterization test, strangler fig, 2 tuần đầu, hotfix khi chưa có test |
| **Nghiệp vụ Ops Hub** (quote → order → RTO → production → delivery) | plan Joblogic Buổi 2–3 | 🟡 đang học | State machine, tiền (decimal, làm tròn, deposit/balance due, thuế), thời gian/DST, PDF/template, tích hợp |
| Câu chuyện Joblogic | Buổi 1 ✅, Buổi 2 đang feature 1 | 🟡 | 4 feature STAR, mock |
| Behavioral | Buổi 12 chưa học | ❌ | 6 câu STAR |

**Kết luận:** Phần kỹ thuật nền (async, API, EF/SQL, multi-tenant) đã đủ cho vòng này. Thiếu chủ yếu là: (1) **design pattern + refactoring + tiếp quản legacy**, (2) **ASP.NET MVC**, (3) **unit test**, (4) **nghiệp vụ Ops Hub + câu hỏi PO**, (5) Git/Agile/AWS mức nói được, (6) mock interview. Phần distributed system sâu (saga, CAP, Buổi 5) chỉ cần nói được ở mức khái niệm.

### Thứ tự ôn đề xuất (nếu còn ~5 buổi)
1. Joblogic Buổi 2: kể xong 4 feature (đang dở) — **quan trọng nhất**, vì SA/PO sẽ đào vào CV.
2. Design patterns + refactoring + tiếp quản legacy (mục 4, 5 của file này).
3. Nghiệp vụ Ops Hub + câu hỏi PO (mục 7, 8).
4. MVC + unit test + Git/Agile/AWS ôn nhanh (mục 3, 6, 9, 10).
5. Mock 45 phút SA + PO.

---

## 1. Pitch bản thân (60 giây)

> I'm a full-stack developer with about four years of experience, strongest on the .NET backend. Most recently I worked on PlaySweeps, a US sweepstakes gaming platform with over two million registered players, on .NET 8, SQL Server, Azure and React. I was a feature lead there: I wrote technical designs, delivered features like the Quest Engine and the KYC integration with Socure, and handled on-call incidents. In parallel, I worked part-time for a UK field-service SaaS called Joblogic, on ASP.NET MVC and a .NET microservice platform, where I delivered features in the Projects and Jobs modules such as cost breakdowns, customer contracts with audit trails, and job spend limits. What attracts me to ShedPro is that the Ops Hub is a business-heavy product, quoting, contracts, production, delivery, which is very close to what I did at Joblogic, and I like working closely with a product manager to understand why a feature matters.

Lưu ý trung thực (đã chốt trong `context/joblogic.md`): Joblogic dùng **EF6 + EF Core**, handler tự viết trả `OneOf`, Razor + jQuery + Vue. Nếu SA hỏi "EF Core hay EF6?" → "The core domain still uses EF6 running on .NET 8, newer parts use EF Core, plus Dapper for read-heavy queries."

---

## 2. Kiến trúc & .NET — những gì SA chắc chắn hỏi (đã học, ôn lại)

| Chủ đề | Ý chốt | Note |
|---|---|---|
| async/await | `await` I/O không giữ thread; `.Result` chặn thread + có thể deadlock; starvation khi blocking | `notes/01` |
| DI lifetime | Singleton giữ Scoped = captive dependency; DbContext là Scoped, không dùng song song (`Task.WhenAll`) | `notes/01` |
| Pipeline | Middleware (mọi request) vs filter (MVC, có context action/model); exception → ProblemDetails | `notes/02` |
| REST | Resource + HTTP verb đúng nghĩa, status code, idempotency key cho POST, versioning, keyset pagination | `notes/02` |
| EF / SQL | IQueryable vs IEnumerable, N+1, tracking, rowversion (optimistic), transaction, index, parameter sniffing | `notes/03` |
| Concurrency | Atomic UPDATE / rowversion trước, distributed lock sau. **Không check-then-act**: INSERT có UNIQUE trong cùng transaction | `progress.md` |
| Multi-tenant | Shard theo tenant, SESSION_CONTEXT + view + RLS block predicate, FK kèm TenantId, cache key có tenant | `notes/J-multitenant-deep.md` |
| Messaging | Query qua HTTP, command qua queue, event qua topic; at-least-once → consumer idempotent; outbox nếu cần ghi DB + gửi message nhất quán | `notes/J-joblogic-architecture.md` |

### "Stable and scalable as it grows" — câu trả lời mẫu
> For a system like the Ops Hub I'd start with a well-structured modular monolith rather than microservices: clear modules for Quotes, Orders, Contracts, Production and Delivery, each with its own application layer, and communication through interfaces or in-process events. That keeps transactions simple, which matters when money and contracts are involved. To keep it scalable I'd keep the web tier stateless so it can scale horizontally behind a load balancer, push slow work like PDF generation, emails and third-party sync to background workers through a queue, add read replicas or caching for heavy reports, and watch the database with proper indexes and query monitoring. I'd only split a module into a separate service when there's a real reason, like a different scaling profile or a separate team.

### Clean architecture / layering
- **Presentation** (Controller/Razor/API) → **Application** (use case, handler, validation, transaction) → **Domain** (entity, rule, value object) ← **Infrastructure** (EF, S3, email, Stripe). Domain không phụ thuộc Infrastructure (dependency inversion).
- Controller mỏng: nhận request → gọi handler/service → map kết quả. Không để logic tính giá trong controller hay Razor view.
- Joblogic: Web MVC → message tới Jicroservice → `IHandler<TMsg, OneOf<TRes, Error>>` → service → EF/Dapper. Đây là ví dụ thật cho "application layer + result type".

### SOLID — một câu mỗi chữ, kèm ví dụ nghiệp vụ
- **S**: `QuotePricingService` chỉ tính giá; `QuotePdfRenderer` chỉ render.
- **O**: thêm loại thuế/RTO provider mới bằng class mới implement interface, không sửa `if/else` lớn.
- **L**: mọi `IPaymentProvider` phải trả kết quả cùng ngữ nghĩa (không throw `NotSupported` ở 1 provider).
- **I**: tách `IReadQuotes` / `IWriteQuotes` thay vì repository khổng lồ.
- **D**: handler phụ thuộc `IClock`, `ITaxCalculator`, `IDocumentStorage`, không `DateTime.Now`, không `new S3Client()` → **testable** (JD nhấn chữ này).

---

## 3. ASP.NET MVC (❌ chưa học — phải ôn)

| Chủ đề | Cần nói được |
|---|---|
| MVC flow | Routing → controller action → model binding → validation → action → `ViewResult` → Razor render HTML |
| Model binding | Nguồn: route, query, form, body (`[FromBody]` chỉ 1 lần). Binding vào ViewModel, không bind thẳng entity |
| **Over-posting** | Form gửi thêm field `IsApproved=true` → bind vào entity → bị sửa. Chặn: ViewModel riêng chỉ có field cho phép, hoặc map tay; tránh `[Bind]` dài |
| Validation | DataAnnotations / FluentValidation, `ModelState.IsValid`, validate cả server (client-side chỉ là UX) |
| **Anti-forgery (CSRF)** | Cookie auth → trình duyệt tự gửi cookie → site lạ có thể POST thay user. `@Html.AntiForgeryToken()` / tag helper `<form>` tự thêm, `[ValidateAntiForgeryToken]` hoặc `AutoValidateAntiforgeryToken` toàn cục. API dùng bearer token thì không cần |
| PRG | Post-Redirect-Get: POST xong `RedirectToAction` để F5 không submit lại (liên quan double submit quote/order) |
| Filters | Authorization → Resource → Action → Exception → Result. Dùng cho permission (Joblogic có `[Permission(PROJECT_DOWNLOAD)]`), audit, transaction |
| Partial view / View component / Tag helper | Tái sử dụng UI; view component có logic riêng |
| XSS | Razor tự encode `@value`; nguy hiểm khi dùng `Html.Raw` (vd. rich text T&C) → sanitize HTML |
| MVC vs Web API | MVC trả HTML (server render), API trả JSON; ASP.NET Core gộp chung `ControllerBase`/`Controller` |

Câu mẫu:
> In Joblogic's back-office, pages are Razor views with Vue components embedded for the interactive parts. Controllers stay thin: they bind to a view model, check permissions with an attribute filter, then send a message to the backend service and map the result. I never bind directly to entities, to avoid over-posting, and all POST forms use the anti-forgery token because it's cookie-authenticated.

---

## 4. Design patterns (❌ lỗ hổng lớn nhất)

Nguyên tắc trả lời: **vấn đề → pattern → ví dụ thật/ví dụ Ops Hub → trade-off**. Đừng liệt kê định nghĩa.

| Pattern | Khi nào | Ví dụ để kể |
|---|---|---|
| **Strategy** | Nhiều thuật toán đổi được theo cấu hình | Tính giá theo loại sản phẩm; RTO provider khác nhau tính lịch trả góp khác nhau; Joblogic selling rate theo khung giờ/holiday |
| **State / state machine** | Thực thể có vòng đời, mỗi trạng thái cho phép hành động khác nhau | Quote: Draft → Sent → Accepted/Expired → Order: Confirmed → InProduction → Ready → Scheduled → Delivered / Cancelled. Chặn chuyển trạng thái sai ở domain, không ở UI |
| **Factory** | Tạo object phức tạp hoặc chọn implementation lúc chạy | `IRtoProviderFactory.Get(companyId)`; DocGen chọn template tenant → fallback hệ thống |
| **Template Method** | Các bước giống nhau, chi tiết khác | Sinh tài liệu: lấy data → chọn template → thay tag → xuất PDF (Joblogic DocGen) |
| **Decorator** | Thêm hành vi ngang (log, cache, retry) không sửa class gốc | `CachedTaxRateProvider` bọc `ZipTaxClient`; MediatR pipeline behavior (validation, logging) |
| **Repository + Unit of Work** | Tách data access; UoW = 1 transaction | `DbContext` đã là UoW + repository; không cần bọc generic repository thêm. PlaySweeps: repository bọc stored procedure Dapper |
| **Specification** | Điều kiện nghiệp vụ tái sử dụng/ghép | "RTO option eligible": credit, giá trị tối thiểu, bang |
| **Mediator / CQRS** | Tách command/query, pipeline chung | Joblogic: message + handler; Replication sang Azure Search = read model |
| **Observer / domain event** | Một sự kiện kéo theo nhiều việc | OrderDelivered → gửi SMS/email, cập nhật balance, audit. Joblogic: Notification/Audit subscribe event |
| **Outbox** | Ghi DB + gửi message nhất quán | Đơn đã lưu nhưng message "gửi email" mất. Ghi outbox trong **cùng transaction**, worker gửi sau (đừng nhầm với Mediator) |
| **Adapter / Anti-corruption layer** | Tích hợp hệ ngoài có model khác | Map SKU từ 3D configurator, Stripe, thuế → model nội bộ; đổi provider chỉ sửa adapter |
| **Result type (OneOf)** | Lỗi nghiệp vụ là kết quả bình thường | Joblogic handler trả `OneOf<TSuccess, Error>`, exception chỉ cho lỗi bất ngờ |

Câu mẫu (State):
> An order has a clear lifecycle, so I'd model it as a state machine in the domain: the Order entity exposes methods like `Confirm()`, `StartProduction()`, `ScheduleDelivery(date)`, `Cancel(reason)`, and each one checks the current status and the business rules before changing it. The UI only shows the actions that are allowed, but the rule lives in the domain, so an API call or a background job can't put the order in an invalid state. Every transition writes an audit entry with who, when and why — similar to the contract audit trail I built at Joblogic.

Câu hỏi bẫy: "Khi nào **không** dùng pattern?" → khi chỉ có 1 cách làm và không có dấu hiệu thay đổi; pattern thêm tầng gián tiếp. "I add a pattern when a second case actually appears, not up front."

---

## 5. Refactoring + tiếp quản code từ partner Mỹ (❌ chưa học)

### Code smell hay gặp & cách sửa
| Smell | Refactoring |
|---|---|
| Method dài, controller béo | Extract Method / Extract Class → service/handler |
| `switch` theo loại lặp ở nhiều nơi | Replace Conditional with Polymorphism (Strategy) |
| Primitive obsession (`decimal price`, `string status`) | Value object `Money(amount, currency)`, enum/state |
| Duplicate logic tính tiền ở UI, PDF, API | Gom về 1 domain service; PDF đọc kết quả đã tính |
| `DateTime.Now` khắp nơi | Inject `IClock`/`TimeProvider` (.NET 8) |
| God repository / static helper | Tách theo use case, DI |

### Cách refactor an toàn (nói theo thứ tự)
1. **Characterization test** (golden master): viết test chụp lại hành vi hiện tại (kể cả hành vi "lạ") trước khi sửa.
2. Bước nhỏ, mỗi commit một thay đổi, chạy test sau mỗi bước; tách PR refactor và PR đổi hành vi.
3. Tạo **seam**: interface quanh phụ thuộc khó test (DB, thời gian, API ngoài).
4. **Strangler fig**: phần mới viết cạnh phần cũ, chuyển dần route/feature, có feature flag để quay lại.
5. Đo trước/sau nếu refactor vì performance.

### "2 tuần đầu khi tiếp quản" — câu trả lời mẫu (rất có thể bị hỏi)
> In the first two weeks I'd focus on understanding before changing. First, get the system running locally and through the deployment pipeline, and get access to logs and monitoring. Second, map the main business flows end to end — quote, order, contract, production, delivery — with the PM, and draw a simple architecture and data diagram. Third, ask the US partner for a knowledge-transfer session with a prepared list of questions: known bugs, risky areas, why certain decisions were made, how deployments and secrets are managed. Fourth, pick up a few small bugs so I learn the code by working in it. And I'd write down what I find as living documentation. I won't start a big rewrite; improvements go in small steps backed by tests. I did something similar at PlaySweeps when I took over the Socure KYC integration from a colleague: I studied the vendor dashboard and decision module, found that the initial prototype had wrong assumptions, and reworked it until it ran stably in production.

### "Bug gấp trên production, code chưa có test"
> First I'd reproduce it and limit the impact — for example a feature flag or a data fix if customers are blocked. Then I'd write a test that reproduces the bug, even a narrow one, make the smallest fix that passes it, and get a review. After the hotfix, I'd add a follow-up ticket to cover that area properly and look for the root cause, not only the symptom.

---

## 6. Unit test (❌ chưa ôn, nhưng có kinh nghiệm thật)

Bằng chứng: PlaySweeps ~200 file test **xUnit + Moq**; Joblogic **MSTest + AutoFixture + AutoMocker** (unit test audit handler, selling rate). Nói đúng tên framework từng nơi.

- **Test pyramid**: nhiều unit test (domain, tính tiền, state machine) → ít integration test (`WebApplicationFactory` + DB thật/Testcontainers) → rất ít E2E.
- **Mock gì**: phụ thuộc ngoài (HTTP, email, clock, queue). **Không mock**: domain object, value object; không mock `DbContext` để test query (dùng DB thật trong integration test).
- **Đặt tên**: `Method_Scenario_ExpectedResult`, cấu trúc Arrange–Act–Assert, một hành vi mỗi test.
- **Test tiền & thời gian**: case biên làm tròn, deposit = 0, trả quá, ngày DST, ca qua nửa đêm (giống Selling Rate Times).
- **Testable code** = DI + `IClock` + logic thuần trong domain (JD nhấn "testable").

Câu mẫu:
> I focus unit tests on business rules where bugs cost money — pricing, balance due, state transitions, date calculations — because those are pure logic and fast to test. For data access and integrations I prefer a few integration tests against a real database rather than mocking EF, since mocked queries give false confidence. At PlaySweeps I wrote unit tests with xUnit and Moq, around two hundred test files across the features I worked on; at Joblogic the team used MSTest with AutoFixture.

---

## 7. Nghiệp vụ Ops Hub — chủ đề cho cả SA và PO

Chỉ dùng phạm vi **công khai trong JD**. Không nhắc release notes, tên đối tác RTO, Ziptax, bug cụ thể của ShedPro. Nói dạng "I'd assume… and I'd confirm with the PM".

### 7.1 Luồng chính và dữ liệu
Quote (sản phẩm, option, giá, thuế, hết hạn) → **Finalize/Accept** (khoá giá, snapshot) → Sales Order (cash sale hoặc **RTO**) → Contract (template, chữ ký) → Production (queue, trạng thái) → Delivery (lịch, tài xế, xác nhận, ảnh, thu tiền còn lại).

### 7.2 Tiền
- Dùng `decimal`, không `double`. Làm tròn **một chỗ**, quy tắc rõ (`MidpointRounding.AwayFromZero` hay banker's), làm tròn theo dòng hay theo tổng → phải hỏi PO/kế toán.
- Lưu giá **snapshot** trên quote/order khi finalize; đổi bảng giá không ảnh hưởng quote đã gửi (giống Joblogic: tài liệu đã ký giữ nguyên).
- **Balance due = total (gồm thuế) − payments đã ghi nhận (deposit, …) − refund điều chỉnh**. Tính từ sổ giao dịch (ledger), không lưu một con số rồi cộng trừ tay → tránh lệch.
- **Markup vs margin**: markup = lợi nhuận/giá vốn; margin = lợi nhuận/giá bán (Joblogic cost breakdown có profit & margin).
- **RTO** (rent-to-own): khách thuê trả góp hằng tháng, đủ kỳ thì sở hữu; có phí ban đầu, số kỳ, điều kiện đủ điều kiện (eligibility), thường do công ty RTO bên thứ ba duyệt. → hỏi PO: ai tính lịch trả, ai giữ hợp đồng gốc.
- Thanh toán: webhook payment provider → **idempotent** theo event id (kinh nghiệm Pragmatic, Joblogic Stripe).

### 7.3 Thời gian / múi giờ / DST
- Lưu instant bằng UTC (`DateTimeOffset`), **ngày giao dự kiến là ngày lịch** → lưu `DateOnly` + timezone của cửa hàng/khách, không lưu "nửa đêm UTC".
- Bắc Mỹ có nhiều múi giờ + DST (Arizona không DST) → tính "+N ngày" theo lịch địa phương (`TimeZoneInfo`, NodaTime), không cộng 24h.
- Bug kinh điển: lưu `2026-11-02T00:00` giờ địa phương thành UTC rồi hiển thị ở múi giờ khác → lệch 1 ngày.
- Test bằng `TimeProvider` giả với ngày DST (2026-03-08, 2026-11-01 ở Mỹ).

Câu mẫu:
> A delivery date is a calendar date, not an instant, so I'd store it as a date plus the store's time zone, and only convert to UTC for actual timestamps like "delivered at". Off-by-one-day bugs usually come from storing local midnight as UTC and then rendering it in another zone, or from adding 24 hours across a DST change.

### 7.4 Tài liệu PDF / hợp đồng
- Template theo công ty (tenant) → fallback template hệ thống; tag thay thế; tài liệu **đã ký phải bất biến**: lưu file PDF đã sinh + phiên bản template + snapshot dữ liệu.
- Sinh PDF ở background worker nếu chậm; cache theo checksum dữ liệu (Joblogic DocGen); file lưu S3, tải bằng **presigned URL** ngắn hạn sau khi kiểm tra quyền (giống SAS + proxy ở Joblogic).
- Escape ký tự đặc biệt trong dữ liệu khi đưa vào template/HTML.

### 7.5 Multi-tenant SaaS
Mỗi công ty bán shed là một tenant (có cửa hàng/region bên trong). Cô lập dữ liệu, cấu hình theo tenant (thuế, template, quy trình), feature theo gói. → Dùng nguyên câu chuyện Joblogic (`notes/J-multitenant-deep.md`).

### 7.6 Tích hợp bên thứ ba
Webhook vào: xác thực chữ ký → lưu raw event → trả 200 nhanh → xử lý async, idempotent theo event id. Gọi ra: timeout + retry có backoff + circuit breaker (Polly), log correlation id, bảng "integration errors" để vận hành xem và retry tay (mapping SKU sai…).

### 7.7 Hiệu năng & ổn định
Production queue / báo cáo chậm: xem query plan, index, N+1, phân trang keyset, đọc từ replica, cache. Sự cố: logs/metrics/traces (CloudWatch, X-Ray hoặc App Insights), correlation id. Kinh nghiệm: on-call PlaySweeps (App Insights, Grafana Loki, Splunk).

---

## 8. Câu hỏi PO & bài toán thực tế (luyện nói)

Khung trả lời PO: **làm rõ (hỏi lại) → đề xuất phương án nhỏ giao trước → edge case → đo kết quả**.

| Câu hỏi | Ý chính |
|---|---|
| Quote đã gửi, bảng giá tăng | Quote là snapshot có hạn; giữ giá tới hết hạn; nếu muốn cập nhật thì tạo revision mới, khách thấy so sánh. Hỏi PO chính sách |
| Balance due sai ở một số đơn | Lấy danh sách đơn sai, tìm điểm chung (có refund? đổi thuế? sửa đơn sau deposit?), so ledger vs số lưu, sửa công thức + script sửa dữ liệu có audit, test hồi quy |
| Huỷ đơn khi đã vào sản xuất | Hỏi: phí huỷ? hoàn deposit bao nhiêu? sản phẩm dở thành hàng tồn kho? ai được duyệt? thông báo ai? RTO contract huỷ thế nào? |
| Ngày giao lệch 1 ngày | Mục 7.3 |
| Yêu cầu mơ hồ | Hỏi "vấn đề người dùng là gì", viết acceptance criteria + ví dụ cụ thể, mock nhanh, xác nhận lại trước khi code |
| Đổi yêu cầu giữa sprint | Nêu ảnh hưởng (thời gian, rủi ro), để PO chọn đổi phạm vi; không tự âm thầm làm thêm |
| Feature lớn | Cắt lát dọc (vertical slice), feature flag, giao bản tối thiểu dùng được trước ("1% improvements") |
| Không đồng ý với PO | Đưa dữ liệu/rủi ro, đề xuất phương án thay thế, PO quyết về giá trị, dev chịu trách nhiệm về cách làm |
| Ưu tiên bug vs feature | Theo tác động: tiền/dữ liệu sai/khách bị chặn trước; còn lại đưa vào backlog có mức ưu tiên |

Ví dụ thật để kể: Joblogic Job Spend Limit (visit 2+ so với phần còn lại, cờ RedeployRequired khi đổi hạn mức sau khi đã deploy xuống thiết bị) — đây là **edge case phát hiện khi hiểu nghiệp vụ**. PlaySweeps Quest Engine: client thiết kế công thức, user làm rõ requirement và viết TDD.

---

## 9. AWS cho dev .NET (🟡 có bảng map, cần nói được)

| Nhu cầu | AWS | Azure tương đương (đã dùng) |
|---|---|---|
| Chạy web app | ECS Fargate / Elastic Beanstalk / App Runner | App Service |
| Function | Lambda | Azure Functions |
| Queue | **SQS** (FIFO = thứ tự theo message group) | Service Bus queue (session) |
| Pub/sub | **SNS** (+SQS fan-out) / EventBridge | Service Bus topic, Event Hub |
| DB | RDS SQL Server / Aurora | Azure SQL |
| File | **S3** + presigned URL | Blob + SAS |
| Secret | Secrets Manager / KMS | Key Vault |
| Monitoring | CloudWatch Logs/Metrics + X-Ray | App Insights |
| Email/SMS | SES / SNS | SendGrid / Twilio |
| Quyền | **IAM role** cho service (không để access key trong code) | Managed Identity |

Kinh nghiệm thật AWS: Altar of Sacrifice (Go) — **KMS, S3, SES**. Câu mẫu:
> Most of my production cloud work was on Azure, and I've used AWS directly for KMS, S3 and SES on a Go project. The concepts map closely — Service Bus to SQS and SNS, Functions to Lambda, Key Vault to Secrets Manager, App Insights to CloudWatch and X-Ray — so I'd expect to be productive quickly and I'd learn the team's specific setup first.

---

## 10. Git & Agile (❌ dễ, ôn 15 phút)

**Git**: feature branch + PR + review; `rebase` để lịch sử gọn trên branch của mình, `merge` vào nhánh chung, không rewrite nhánh chung; `revert` để gỡ commit đã lên prod; `cherry-pick` hotfix sang release branch; commit nhỏ có ý nghĩa; conflict → hiểu cả hai thay đổi trước khi chọn. Joblogic dùng Azure DevOps PR + nhánh uat; PlaySweeps review chéo PR.

**Agile/Scrum**: sprint planning, daily, review/demo, retro; story có acceptance criteria; estimate story point; Definition of Done (code + test + review + deploy staging); backlog refinement với PO. PlaySweeps: Scrum + Jira (~354 ticket).

---

## 11. Behavioral (tiếng Anh, STAR) — chuẩn bị 6 câu chuyện

| Câu hỏi | Chất liệu |
|---|---|
| Tiếp quản hệ thống người khác làm | Socure KYC (tiếp quản, sửa prototype sai) |
| Dẫn dắt feature từ thiết kế tới release | Quest Engine V2 (TDD, Cosmos, RedLock, idempotency claim, lên prod) |
| Bug production khó nhất / on-call | Incident điều tra bằng App Insights + Loki + Splunk (chọn 1 vụ cụ thể, có con số) |
| Hiểu nghiệp vụ, edge case | Job Spend Limit (visit 2+, RedeployRequired) |
| Làm việc remote với team nước ngoài | Team PLAYSTUDIOS (Mỹ): Slack, họp technical design; team UK Joblogic: code review |
| Học nhanh công nghệ mới | AWS + Go ở Altar; Rive với designer nước ngoài |
| "1% improvements" / chủ động cải thiện | Exponential rate limiting cho API nhạy cảm; tối ưu fetch/cache AVA |

Câu hỏi khó: "Vì sao rời công ty cũ?" → "The company restructured and my position was affected in September; I'm now looking for a product team where I can own a business-critical system long term." (Không nói chi tiết.)

---

## 12. Câu hỏi ngược cho interviewer

Cho SA:
1. What does the current architecture of the Ops Hub look like — monolith or services, and which parts are you most worried about after the handover from the US partner?
2. How is testing and deployment set up today, and what would you want improved first?
3. Is the plan to keep building on the existing codebase or to gradually modernise parts of it?

Cho PO:
1. What are the biggest pain points your customers report in the Ops Hub right now?
2. How do you and the developers work together — how early am I involved in shaping a feature?
3. What would a successful first three months look like for this role?

---

## 13. Lỗi Hiệp hay mắc — tự nhắc trước khi vào phòng

- Check-then-act → luôn nói "**INSERT with a UNIQUE constraint in the same transaction**" hoặc atomic UPDATE.
- Trùng request → **replay response cũ**, không trả lỗi.
- Message liên quan tiền/hợp đồng **không được mất** → outbox / at-least-once + idempotent.
- Nêu **trade-off** (sync vs async, monolith vs service), không trả lời một chiều.
- Nêu **tên vấn đề + công cụ điều tra + xử lý tạm + xử lý gốc** khi nói về sự cố.
- Đưa **con số** (số player, số file test, số service, thời gian).
- Tiếng Anh: "-s" ngôi 3 ("it depends"), không "is depend", tránh bị động thừa ("will be encountered").
- Không nhắc chi tiết nội bộ ShedPro; không chê code Joblogic; nói đúng công nghệ thật (EF6, MSTest, Vue).
