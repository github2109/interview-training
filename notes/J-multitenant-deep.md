# Multi-tenant — cơ chế sâu (Joblogic, ShedPro, thế giới)

> Ký hiệu độ tin cậy: **[code]** = đã thấy trong code / notes đã kiểm của Joblogic. **[suy luận]** = hợp lý theo kiến trúc nhưng chưa kiểm, khi phỏng vấn nói "I believe…" hoặc nói theo dạng "the typical way is…". Không bịa thêm chi tiết nội bộ.

---

## 0. Ba mô hình, và sharding nằm ở đâu

| Mô hình | Cách lưu | Cô lập | Chi phí / vận hành | Ví dụ |
|---|---|---|---|---|
| **Silo** (DB per tenant) | Mỗi tenant một database | Mạnh nhất, backup/restore từng tenant dễ | Đắt, migrate schema N lần, nhiều connection pool | Khách enterprise, yêu cầu compliance |
| **Bridge** (schema per tenant) | Chung DB, mỗi tenant một schema | Trung bình | Migrate N schema | Postgres schema-per-tenant |
| **Pool** (shared table) | Chung bảng, cột `TenantId` | Yếu nhất, dựa vào code + RLS | Rẻ, 1 lần migrate | Đa số SaaS SMB |

**Sharding = Pool nhưng chia thành nhiều database.** Mỗi shard là một database có **schema giống hệt nhau**, chứa một **nhóm tenant**; trong shard, các tenant chung bảng và phân biệt bằng `TenantId`. Tenant to có thể được đặt riêng một shard (tức là silo cho riêng tenant đó) mà code không đổi gì.

Joblogic: SQL Server **sharded theo tenant** **[code]**, nên đây là mô hình *pool trong từng shard + nhiều shard*. Vì thế có **2 lớp cô lập**: vật lý (khác shard = khác DB) và logic (chung shard thì lọc `TenantId`).

Đời thường: một chung cư (shard) có nhiều căn hộ (tenant). Thẻ từ (TenantId) quyết định bạn vào căn nào. Thành phố có nhiều chung cư; sổ hộ khẩu (shard map) cho biết hộ nào ở chung cư nào.

---

## 1. Shard trong database trông như thế nào

### 1.1 Shard map (catalog)
Cần một nơi trả lời câu "tenant X ở DB nào". Ba cách chia:
- **Directory / lookup**: bảng `TenantId → ShardKey`. Linh hoạt nhất, di chuyển tenant chỉ cần đổi 1 dòng. Phải cache vì nó nằm trên mọi request.
- **Hash**: `shard = hash(TenantId) % N`. Không cần bảng, nhưng thêm shard là phải di chuyển rất nhiều tenant (trừ khi dùng consistent hashing / nhiều logical shard).
- **Range**: TenantId 1–1000 ở shard 1… Dễ lệch tải.

Joblogic: middleware lấy **shard key của tenant từ License service, có cache** **[code]**, tức là **directory-based**. Phần `ShardKey → connection string` nằm ở đâu (config, Key Vault, bảng catalog) **[suy luận]**: chưa kiểm, nói chung chung là "a shard catalog".

```text
License (catalog)                     Shards (SQL Server, cùng schema)
TenantId | ShardKey | Status          shard-01: Tenant 12, 57, 98 ...
12       | shard-01 | Active          shard-02: Tenant 33, 41 ...
33       | shard-02 | Frozen          shard-07: Tenant 500 (tenant rất lớn, ở riêng)
500      | shard-07 | Active
```

### 1.2 Bên trong một shard
- Mọi bảng nghiệp vụ có `TenantId NOT NULL`.
- **Index bắt đầu bằng `TenantId`**: `(TenantId, JobId)`, `(TenantId, CustomerId, CreatedAt)`. Lý do: mọi query đều có `WHERE TenantId = @t`, nên seek đúng vùng của tenant. Không có, một tenant query sẽ quét dữ liệu của tất cả tenant trong shard (vừa chậm vừa noisy neighbor).
- Khoá ngoại nên **kèm TenantId** (`FK (TenantId, CustomerId) → Customer(TenantId, CustomerId)`) để DB chặn việc Job của tenant A trỏ vào Customer của tenant B. Joblogic có làm vậy không **[chưa kiểm]**.
- **Dữ liệu dùng chung** (system template, danh mục quốc gia, tiền tệ): hoặc bảng tenantless trong mỗi shard (đồng bộ), hoặc DB/service riêng. Joblogic DocGen: *template tenant → fallback template hệ thống* **[code]**.

### 1.3 Vòng đời tenant
- **Onboarding**: chọn shard (đang ít tải nhất), ghi mapping vào catalog, seed dữ liệu khởi tạo. Joblogic: `CreateCompanyHandler` + initial template data **[code]**; thuật toán chọn shard **[chưa kiểm]**.
- **Freeze / hết hạn**: catalog giữ trạng thái, middleware chặn **[code]**.
- **Di chuyển tenant (rebalance)**: copy dữ liệu sang shard mới → chặn ghi ngắn → copy phần chênh → đổi mapping → **xoá cache mapping ở mọi instance** → mở lại. Lỗi kinh điển: quên invalidate cache, một số instance vẫn ghi vào shard cũ.
- **Offboarding / GDPR**: xoá hoặc export toàn bộ dữ liệu một tenant. Mô hình pool phải `DELETE ... WHERE TenantId` trên mọi bảng, mọi store (SQL, Mongo, Blob, Search, Redis). Joblogic có cleanup tenantless dùng `sp_set_session_context` **[code]**.

---

## 2. Làm sao một query biết lấy DB nào (data-dependent routing)

Nguyên tắc: **connection string không cố định lúc khởi động app, mà được chọn theo tenant ở mỗi request/message**.

```csharp
// 1. Tenant context: scoped per request / per message
public sealed class TenantContext
{
    public Guid TenantId { get; private set; }
    public string ShardKey { get; private set; } = default!;
    public void Set(Guid tenantId, string shardKey) { TenantId = tenantId; ShardKey = shardKey; }
}

// 2. Middleware (giống ý tưởng ResolveTenantSettingMiddleware)
public async Task Invoke(FunctionContext ctx, FunctionExecutionDelegate next)
{
    var op = ctx.GetOperationInfo();                 // TenantId lấy từ token / message, KHÔNG từ body
    var setting = await _cache.GetOrAddAsync(        // cache vài phút
        $"tenant-setting:{op.TenantId}",
        () => _license.GetTenantSettingAsync(op.TenantId));

    if (setting is null)            { Reject(ctx, "Unknown tenant"); return; }
    if (setting.Status == Frozen)   { Reject(ctx, "Tenant frozen"); return; }

    _tenantContext.Set(op.TenantId, setting.ShardKey);
    await next(ctx);
}

// 3. Connection factory: shard key -> connection string
public sealed class ShardConnectionFactory(TenantContext t, IShardCatalog catalog)
{
    public string GetConnectionString() => catalog.ConnectionStringFor(t.ShardKey);
}

// 4. DbContext / Dapper tạo theo tenant
services.AddScoped(sp => new JobLogicContext(
    sp.GetRequiredService<ShardConnectionFactory>().GetConnectionString())); // EF6 nhận nameOrConnectionString
```

Điểm Senior cần nói thêm:
- **Không có tenant thì không tạo được connection** (fail closed). Code tenancy không có "connection mặc định".
- **Connection pool là theo connection string**: mỗi shard một pool. Con số: 10 instance × 8 shard × max pool 100 = tới 8.000 connection tiềm năng, phải so với giới hạn của SQL Server / Azure SQL tier. (Liên hệ bài pods × pool ở Buổi 3.)
- **Cache shard map có TTL + invalidate khi di chuyển/freeze tenant.** Freeze mà cache 10 phút thì tenant hết hạn còn dùng được 10 phút: chấp nhận được hay không là quyết định nghiệp vụ.
- **Background job / message** không có HTTP request: tenant phải nằm **trong message** và middleware của consumer làm lại đúng bước 2. Joblogic: operation info đi theo mọi message, pipeline Function (HTTP / ServiceBus / Timer) đều qua middleware **[code]**.
- Microsoft có thư viện chính thống cho đúng việc này: **Elastic Database client library** (`ShardMapManager`, `ListShardMap`, `OpenConnectionForKey`) gọi là *data-dependent routing*. Joblogic có dùng thư viện này không **[chưa kiểm]**; dùng làm từ khoá khi nói chuyện với SA.

---

## 3. Tenant được validate ở những đâu (defense in depth)

Câu hỏi "chặn ở đâu" thì trả lời **nhiều lớp**, mỗi lớp chặn một kiểu lỗi khác:

| # | Lớp | Kiểm tra gì | Chặn được lỗi gì |
|---|---|---|---|
| 1 | **Authentication** | TenantId lấy từ **token / session** (claim), không bao giờ từ body, query string, header client gửi | Người dùng sửa `tenantId` trên URL |
| 2 | **Tenant middleware** | Tenant tồn tại, active/frozen, user thuộc tenant; chọn shard | Tenant hết hạn, token tenant giả |
| 3 | **Authorization (permission + ownership)** | Role/permission (RBAC), và **resource thuộc phạm vi của user**: user Portal chỉ thấy job của *customer của mình* trong tenant | IDOR, Portal user A xem job của customer B **cùng tenant** |
| 4 | **Message boundary** | Message phải có tenant context; consumer resolve lại tenant, không tin dữ liệu khác trong payload | Fan-out gán sai tenant, message thiếu tenant chạy trên shard sai |
| 5 | **Data access (logic)** | Interceptor / global query filter tự thêm `WHERE TenantId = @t` khi đọc và gán `TenantId` khi ghi | Dev quên điều kiện tenant trong LINQ |
| 6 | **Database (RLS)** | Row-Level Security đọc `SESSION_CONTEXT('TenantId')`, DB tự lọc | Raw SQL / Dapper quên `WHERE` |
| 7 | **Store phụ** | Cache key, Blob path, Search index filter, Mongo collection/filter đều có tenant | Lộ qua cache, file, search |
| 8 | **Observability** | Log/trace mang TenantId; cảnh báo khi response chứa entity khác tenant | Phát hiện sớm |

Joblogic: lớp 2 **[code]**, lớp 5 (TenancyInterceptor) **[code]**, lớp 6 có dấu hiệu (cleanup tenantless phải `sp_set_session_context` để "vượt policy") **[suy luận]**, lớp 3 có permission + mapping quyền Portal **[code, user đã thêm Job Spend Limit permission]**, lớp 1/4/7/8 **[chưa kiểm chi tiết]**.

### 3.1 Bẫy quan trọng: "another company" là cấp nào?
Ở Joblogic, **tenant = công ty dùng phần mềm** (công ty bảo trì), còn **Customer Portal** là nơi **khách hàng của tenant** đăng nhập. Một khách báo "tôi thấy job của công ty khác" có thể là:
- **Cross-tenant leak**: thấy job của một tenant khác → lỗi lớp 1/2/4/5/6/7. Nghiêm trọng nhất, có thể là sự cố dữ liệu cá nhân (GDPR ở UK).
- **Intra-tenant leak**: thấy job của *customer khác cùng tenant* → lỗi lớp 3 (thiếu lọc theo CustomerId / site của portal user). Interceptor TenantId **không** chặn được lỗi này.

Câu hỏi làm rõ đầu tiên này là điểm cộng lớn với SA.

### 3.2 Global query filter và RLS (code minh hoạ)
EF Core (phần mới):
```csharp
modelBuilder.Entity<Job>().HasQueryFilter(j => j.TenantId == _tenant.TenantId);
// IgnoreQueryFilters(), FromSqlRaw(), Dapper, ExecuteUpdate với raw SQL đều có thể bỏ qua -> cần RLS
```
EF6 (domain Core của Joblogic) không có `HasQueryFilter`; làm tương tự bằng **`IDbCommandTreeInterceptor`** (sửa command tree để thêm điều kiện) hoặc thư viện như EntityFramework.DynamicFilters. TenancyInterceptor của Joblogic hoạt động cụ thể kiểu nào **[chưa kiểm]**.

SQL Server RLS:
```sql
CREATE FUNCTION sec.fn_tenant(@TenantId uniqueidentifier)
RETURNS TABLE WITH SCHEMABINDING AS
RETURN SELECT 1 AS ok WHERE @TenantId = CAST(SESSION_CONTEXT(N'TenantId') AS uniqueidentifier);

CREATE SECURITY POLICY sec.TenantPolicy
  ADD FILTER PREDICATE sec.fn_tenant(TenantId) ON dbo.Job,
  ADD BLOCK  PREDICATE sec.fn_tenant(TenantId) ON dbo.Job AFTER INSERT
  WITH (STATE = ON);

-- Mỗi lần mở connection (connection interceptor):
EXEC sp_set_session_context @key = N'TenantId', @value = @tenantId, @read_only = 1;
```
- FILTER chặn **đọc** sai tenant, BLOCK chặn **ghi** sai tenant.
- Đặt session context **mỗi lần mở connection**, vì connection được tái sử dụng từ pool.
- Job tenantless (cleanup) cần một cách vượt policy có kiểm soát, đúng với dấu hiệu thấy ở Joblogic.
- Trade-off: thêm predicate vào mọi query (cần index có TenantId), debug khó hơn ("sao query trả 0 dòng?").

---

## 4. Một luồng request điển hình (Joblogic)

**Kịch bản:** nhân viên văn phòng của tenant *ACME Maintenance* mở Job #123 rồi sửa trạng thái, hệ thống gửi email cho khách.

1. **Browser → Web (ASP.NET Core MVC)**: cookie/OIDC; claim của user chứa TenantId của ACME **[suy luận về tên claim]**.
2. **Web → Core service** bằng `RequestAsync` (HTTP, cần kết quả) với `GetJobMsg { JobId = 123 }` + **operation info** (TenantId, UserId) **[code]**.
3. **Core (Azure Function, HTTP trigger)** → `IDispatcher` → **ResolveTenantSetting middleware**: lấy setting của ACME từ License (cache): `ShardKey = shard-03`, `Status = Active` **[code]**. Nếu Frozen thì dừng ở đây.
4. **Handler** `IHandler<GetJobMsg, OneOf<JobResponse, Error>>` (TenancyHandler) → service → `JobLogicContext` mở connection tới **shard-03**.
5. **TenancyInterceptor** thêm điều kiện TenantId: `SELECT … FROM Job WHERE JobId = 123 AND TenantId = @acme`. Job 123 của tenant khác (nằm cùng shard) trả về **0 dòng → Error NotFound**, không phải 403, để không lộ việc job tồn tại.
6. Trả `OneOf` → Web render.
7. User đổi trạng thái → `UpdateJobStatusMsg` → ghi DB → **publish event** `JobStatusChanged` (có TenantId) lên topic Service Bus **[code: event topic]**.
8. **Notification service** nhận event (ServiceBus trigger) → **cùng middleware** resolve tenant lại từ message → đọc template email của ACME → gửi SendGrid; idempotent theo OperationId **[code]**. **Audit service** cũng nhận event → ghi MongoDB của tenant **[code]**.
9. **Timer** (Schedule) mỗi phút là **tenantless**: lấy danh sách tenant hợp lệ từ License rồi **fan-out** từng message mang TenantId riêng **[code]**, sau đó mỗi message lại đi qua bước 3.

Ghi nhớ: **mọi điểm vào (HTTP, queue, timer, webhook) đều phải dẫn tới bước 3**. Webhook tenantless tự suy ra tenant từ payload (vd. Stripe Connect account id → tenant) **[code: webhook tenantless]**; đây là điểm vào rủi ro nhất vì tenant không đến từ token.

---

## 5. Bài toán có thể bị hỏi

### 5.1 Joblogic (SA hỏi về hệ thống bạn đã làm)
1. **Một customer thấy job của công ty khác** → bài tập đang chờ (câu trả lời mẫu sẽ thêm sau khi chấm).
2. **Noisy neighbor**: một tenant lớn import 50k job làm chậm cả shard → xác nhận bằng Query Store / DMV theo TenantId, App Insights theo tenant; tạm: throttle/queue riêng, giới hạn batch (Batch service dùng distributed lock) ; tận gốc: rate limit theo tenant, chuyển tenant lớn sang shard riêng, read replica cho báo cáo, Azure Search cho tìm kiếm.
3. **Thêm một shard mới / di chuyển tenant** → quy trình ở 1.3, nhấn mạnh invalidate cache và kiểm tra counts sau khi copy.
4. **Migrate schema cho 20 shard** → migration backward-compatible (expand → deploy code → contract), chạy theo đợt (canary shard), theo dõi lỗi, có khả năng dừng giữa chừng; code phải chạy được khi shard ở 2 version khác nhau.
5. **Báo cáo xuyên tenant cho admin nội bộ** (doanh thu toàn hệ thống) → không query fan-out lên mọi shard từ app; đẩy dữ liệu sang kho phân tích (ETL/event) .
6. **Cache bị lộ**: DocGen cache Redis theo checksum **[code]** → checksum có tính TenantId không? Nếu hai tenant cùng nội dung template + data thì cùng key (thường vô hại vì nội dung giống, nhưng phải chắc data nằm trong checksum). Nguyên tắc: key luôn có prefix tenant.
7. **Tenant hết hạn nhưng còn message trong queue** → middleware chặn tenant frozen; message đó nên dead-letter hay bỏ qua có log, tuỳ loại (thanh toán thì không được bỏ).
8. **Mobile offline**: thiết bị kỹ thuật viên giữ dữ liệu của tenant; logout / đổi tenant phải xoá dữ liệu local, sync API kiểm tra tenant của token khớp với dữ liệu gửi lên.

### 5.2 ShedPro / Ops Hub (chỉ dựa trên phạm vi công khai của JD; khi trả lời nói dạng giả định + hỏi lại)
1. **Tenant phân cấp**: một nhà sản xuất có nhiều đại lý/cửa hàng. Đại lý A có thấy quote của đại lý B không? → tenant = công ty, thêm **sub-scope** (store/region) ở lớp authorization; hỏi PO quy tắc hiển thị.
2. **Đối tác bên thứ ba (công ty RTO, đơn vị tài chính)** cần xem hợp đồng của nhiều tenant → không cho họ "đăng nhập như tenant"; tạo quyền chia sẻ tường minh theo hợp đồng, audit mọi lần truy cập.
3. **Cấu hình theo tenant**: template PDF hợp đồng, thuế, múi giờ, giá → bảng settings theo tenant + fallback hệ thống (giống DocGen); cache có tenant prefix.
4. **Múi giờ theo tenant/địa điểm**: lưu UTC, hiển thị theo time zone của tenant hoặc địa chỉ giao hàng; lịch giao lệch ngày do DST.
5. **Tiếp quản codebase từ đối tác**: làm sao biết code cũ có cô lập tenant đúng không? → tìm mọi raw SQL không có TenantId, viết test "tenant A không đọc được dữ liệu tenant B" cho từng endpoint, bật RLS ở chế độ thử trên staging.
6. **Tích hợp (webhook, Zapier-like)**: webhook đến phải map về đúng tenant bằng định danh tài khoản bên ngoài + chữ ký, không tin tenantId trong payload.
7. **Trên AWS**: tenant isolation bằng IAM (session tags, ABAC) cho S3 prefix theo tenant, SQS message attribute mang tenant.

### 5.3 Câu hỏi multi-tenant phổ biến trên thế giới
1. Chọn silo, bridge hay pool? Khi nào chuyển một tenant từ pool sang silo? (khách enterprise, compliance, noisy).
2. Thiết kế sharding: chọn shard key thế nào (tenant id), xử lý **hot shard**, resharding không downtime.
3. Tenant isolation ở mọi tầng: compute, data, cache, queue, file, search, log.
4. Per-tenant rate limit và quota (token bucket theo tenant).
5. Per-tenant encryption key (BYOK), xoá dữ liệu tenant (crypto-shredding).
6. Backup/restore **một** tenant trong DB dùng chung (khó: phải export theo TenantId hoặc point-in-time restore ra DB tạm rồi copy).
7. Schema migration trên hàng trăm DB/shard.
8. Billing theo usage: đo lường theo tenant.
9. Data residency: tenant EU phải ở region EU, nên shard map còn mang thông tin region (Joblogic có YARP định tuyến vùng **[code]**).
10. Test isolation: integration test tạo 2 tenant, gọi mọi endpoint bằng tenant A với ID của tenant B.

---

## 6. Hệ thống thật trên thế giới (để có ví dụ khi SA hỏi "industry practice")
- **Salesforce**: mô hình pool kinh điển, mọi bảng có `OrgId`, metadata-driven; khách chia vào nhiều "instance/pod".
- **Shopify**: shop được chia vào các **pod** (mỗi pod có MySQL riêng), có công cụ di chuyển shop giữa pod không downtime (Ghostferry).
- **Slack**: ban đầu shard MySQL theo workspace, gặp khó khi một khách (Enterprise Grid) trải nhiều workspace, sau chuyển sang Vitess để shard linh hoạt hơn.
- **Notion**: Postgres shard theo `workspace_id`: 480 logical shard trên 32 DB vật lý (2021), sau đó mở rộng số DB vật lý. Ý tưởng **nhiều logical shard hơn physical** giúp resharding chỉ là di chuyển logical shard.
- **Azure SQL**: Elastic pools + Elastic Database tools (shard map manager, data-dependent routing); có hướng dẫn "multi-tenant SaaS database tenancy patterns" trên Microsoft Learn.
- **AWS**: SaaS Lens / SaaS Factory dùng đúng từ vựng **silo / bridge / pool**; tenant isolation bằng IAM policy động.
- **Citus (Postgres)**: distributed table theo `tenant_id`, co-locate các bảng cùng tenant để join trong một node.

---

## 7. Tự kiểm tra
1. Vì sao index phải bắt đầu bằng TenantId? Nếu thiếu thì ảnh hưởng gì (2 ý)?
2. Directory-based sharding hơn hash-based ở điểm nào? Nhược điểm nào phải xử lý?
3. Kể 4 đường làm bypass TenancyInterceptor.
4. Job #123 thuộc tenant khác: trả 403 hay 404? Vì sao?
5. Di chuyển tenant sang shard mới: bước nào hay bị quên?
6. Timer chạy tenantless lấy TenantId từ đâu, và lớp nào đảm bảo nó vào đúng shard?
