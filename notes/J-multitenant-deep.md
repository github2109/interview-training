# Multi-tenant — Joblogic thực tế (đã kiểm chứng trong code, 2026-10-17)

Nguồn: `joblogic-web` (Core, License, DocGen, Webhooks), `joblogic-databaseproject` (SSDT schema), package nội bộ trong `~/.nuget`.
Ký hiệu: **[code]** = đã thấy trong code/schema. **[docs]** = chỉ thấy trong tài liệu nội bộ (CLAUDE.md). **[chưa kiểm]** = không nói chắc khi phỏng vấn.

## 1. Mô hình: shard, mỗi shard nhiều tenant [code]
- Shard map nằm ở **License DB**: bảng `Company` có cột `ShardKey` (directory-based).
- `ShardKey → connection string`: dictionary `JobLogicDbShardConnStrings` trong **Azure App Configuration**. Có thêm bộ `JobLogicReplicateDbShardConnStrings` (bản replica để đọc).
- **Onboarding** (`CreateCompanyHandler`): tenant mới vào **shard mặc định cấu hình sẵn** (`RegisterDefaultShardKey`, mặc định `"A0000"`); nếu bật `EnableCustomShardKey` thì được chỉ định shard (phải tồn tại trong config). Không có thuật toán tự chọn shard ít tải.
- Không dùng Elastic Database client library; tự viết `ShardyDbManagerProvider`.
- DB tách: `JoblogicDB` (shardy, dữ liệu tenant) và `JoblogicShardlessDB` (dữ liệu dùng chung). Quy tắc: một script SQL không được đụng cả bảng shardy lẫn shardless.

## 2. Bên trong một shard [code]
- Bảng thật nằm ở schema **`tbl_multitenant`**, mọi bảng có `TenantId`.
- **Khoá chính clustered bắt đầu bằng TenantId**: `PK (TenantId, AutoId)` → dữ liệu mỗi tenant nằm liền nhau.
- **Khoá ngoại kèm TenantId**: `FK (TenantId, CustomerAutoId) → Customer(TenantId, AutoLastID)` → DB không cho Job của tenant A trỏ vào Customer của tenant B. (Ví dụ: `FK_Job_CustomerContract (TenantId, CustomerContractId)` — cột của feature Customer Contract.)

## 3. Cách cô lập khi ĐỌC và GHI (cơ chế thật — quan trọng nhất)
```
Middleware (ResolveTenantSetting): TenantId (từ operation info) → ShardKey (License, có cache)
                                    → chặn tenant không active / frozen
→ JobLogicContext(connStringCủaShard, tenantId)   — EF6
→ Mở connection: interceptor đặt SESSION_CONTEXT
     • EnsureTenancySessionContextInterceptor → 'TenantId'
     • DepotSessionContextInterceptor        → 'DepotIds' (chi nhánh user được xem)
→ EF map entity vào VIEW ở schema dbo (vd. dbo.Job), không phải bảng thật:
     SELECT ... FROM tbl_multitenant.Job
     WHERE TenantId = SESSION_CONTEXT('TenantId')            ← lọc tenant
       AND (Deleted = 0 OR SESSION_CONTEXT('ShowAll') = 1)   ← soft delete
       AND (DepotId thuộc SESSION_CONTEXT('DepotIds') ...)   ← lọc chi nhánh
→ Khi GHI: Row-Level Security BLOCK PREDICATE trên ~416 bảng tbl_multitenant
     chặn insert/update dòng có TenantId ≠ SESSION_CONTEXT('TenantId')
     (job hệ thống bỏ qua bằng SESSION_CONTEXT 'IgnoreTenantBlockPolicy' = 1)
```
- **Đọc** được lọc bởi **view** (414/466 view ở `dbo` lọc theo tenant), **không** phải bởi RLS filter predicate (có hàm `tenantFilterPredicate` nhưng không gắn vào policy).
- **Ghi** được chặn bởi **RLS block predicate**.
- Interceptor **không** sửa câu LINQ/SQL; nó chỉ đặt session context mỗi lần mở connection (cần vì connection được tái sử dụng từ pool).
- Hệ quả: dev viết `db.Visits.Where(v => v.Id == id)` không cần `TenantId`, DB tự lọc. Raw SQL/Dapper cũng an toàn **nếu** truy vấn qua view `dbo` và connection đã có session context.
- **Depot** = phạm vi con **trong** tenant (chi nhánh) → đây là lớp cô lập "intra-tenant" có sẵn ở DB.

### 3.1 Không phải mọi query đều qua view lọc tenant [code]
- **EF6/EF Core (tenancy)**: interceptor đặt `TenantId` (EF Core package cũng có `EnsureTenancySessionContextInterceptor`) → đọc qua view `dbo`.
- **Dapper / DbExecutionManager**: thư viện nội bộ (`BaseDbExecutionDapper.SetSessionContextAsync`, `DbExecutionManager.SetSessionContextForMultiTenant`) cũng `EXEC sp_set_session_context 'TenantId', @tenantId` → SQL viết tay dùng `dbo.*` (~379 chỗ) được lọc như EF. Không thấy cờ `@read_only`.
- **Schema `multitenant.*`** (64 view): **chỉ lọc soft delete, KHÔNG lọc tenant** → dùng cho **handler tenantless** tra cứu xuyên tenant (vd. Role: tìm mobile user theo company), tự viết điều kiện tenant trong SQL (~80 chỗ).
- **`tbl_multitenant.*` trực tiếp**: rất hiếm (1 chỗ trong app + processor/migration tool).
- 52 view `dbo` không có điều kiện tenant đều xây trên view `dbo` khác (vd. `VWC_AMSJobs FROM dbo.Job`) → thừa hưởng bộ lọc.
- Stored procedure trong `dbo` không đọc thẳng `tbl_multitenant`.

## 4. Các điểm vào và tenant context [code]
- **Web**: sau đăng nhập, claim `JLClaimType.TenantId` lấy từ `loginToken.Company.TenantId` (không lấy từ request client gửi).
- **Gọi giữa service**: thư viện client mang **operation info** (`ContextTenantId`, `OperationId`); bên nhận `ExtractTenancyOperationInfo` → middleware resolve shard. Có loại message `TenantlessMsg` / `TenantlessEvent` cho việc hệ thống.
- **Timer** chạy tenantless → lấy danh sách tenant hợp lệ → gửi message cho từng tenant [docs + code middleware].
- **Webhook Stripe Connect**: bắt buộc có field `account` (connected account id), chuyển cho Payment service xử lý ở chế độ tenantless (tenant được suy ra từ tài khoản Stripe ở phía Payment [chưa kiểm chi tiết]).
- **Feature flag theo tenant**: `Microsoft.FeatureManagement` + `TargetingFilter` với `TenantTargetingContextAccessor(TenantId)` → bật tính năng cho từng tenant.
- **Cache DocGen**: key tạo từ `tenantId + entityId + templateType + docType + templateId` → không lộ giữa tenant.

## 5. Phòng thủ nhiều lớp — Joblogic có gì
| Lớp | Joblogic |
|---|---|
| Token | TenantId từ claim đăng nhập [code] |
| Middleware | Resolve shard + chặn tenant inactive/frozen [code] |
| Phân quyền trong tenant | Permission/role [code]; Depot lọc ở view [code]; Portal theo customer [chưa kiểm] |
| Đọc | View `dbo` lọc theo SESSION_CONTEXT [code] |
| Ghi | RLS block predicate [code] |
| Toàn vẹn | FK kèm TenantId [code] |
| Cache | Key có tenantId (DocGen) [code] |

## 6. Bài toán "khách thấy job của công ty khác" — dùng cơ chế thật
1. **Làm rõ**: tenant khác (công ty dùng phần mềm) hay customer khác trong cùng tenant (Portal)?
2. **Cross-tenant** khó xảy ra ở đường EF thông thường (view + session context). Nghi vấn theo thứ tự: truy vấn đi thẳng vào `tbl_multitenant` (bỏ qua view), job tenantless có `ShowAll`/`IgnoreTenantBlockPolicy`, connection dùng lại mà session context sai, cache/blob/search key thiếu tenant, message mang sai operation info.
3. **Intra-tenant**: lỗi phân quyền theo customer/depot ở Portal hoặc endpoint lấy theo id mà không kiểm tra quyền sở hữu.
4. **Điều tra**: App Insights theo OperationId/TenantId, endpoint và query đã chạy, audit log (MongoDB) xem ai xem/sửa gì.
5. **Phòng ngừa**: mọi truy vấn qua view; cấm truy cập trực tiếp `tbl_multitenant` từ code ứng dụng (quyền DB user); test với 2 tenant; review mọi chỗ bật `ShowAll`/bỏ qua policy.

## 7. Kiến thức chung (khi SA hỏi "industry practice")
- Silo (DB/tenant) – Bridge (schema/tenant) – Pool (chung bảng) – Shard (pool chia nhiều DB).
- Shard map: directory (linh hoạt, cần cache) vs hash vs range.
- Di chuyển tenant: copy → khoá ghi ngắn → copy phần chênh → đổi mapping → **xoá cache mapping ở mọi instance**.
- Noisy neighbor: đo theo tenant, giới hạn theo tenant, tách tenant lớn sang shard riêng, replica cho báo cáo.
- Migration nhiều shard: expand → deploy → contract, chạy theo đợt.

## 8. Tự kiểm tra
1. Đọc dữ liệu được lọc tenant ở lớp nào? Ghi bị chặn ở lớp nào?
2. Vì sao phải đặt SESSION_CONTEXT mỗi lần **mở connection**?
3. Depot dùng để làm gì, và nó khác TenantId thế nào?
4. Tenant mới được gán shard theo cách nào?
