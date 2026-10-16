# Joblogic — sự thật đã kiểm chứng từ code (2026-10-16)

Nguồn: `/Users/hiepdinhquang/Desktop/ExtraJob/Joblogic/joblogic-web` (git, ~139 commit của user, tác giả `hiepdq` / `HMTS - Hiep Dinh` / `hiepdq2`), 01/2026 – 06/2026. Repo khác: databaseproject (10 commit), material (3), mobile (2).

## Kiến trúc thật
- Multi-tenant SaaS quản lý dịch vụ hiện trường (UK). Repo `joblogic-web` = **FrontApps** (ASP.NET Core .NET 8: Web MVC/Razor lớn nhất, Portal cho khách hàng, WebAPI…) + **"Jicroservices"** (Azure Functions isolated worker): Core, Audit (MongoDB), DocGen (PDF/DOCX), Notification, Schedule, Payment (Stripe), ContractLayer…
- Giao tiếp: `RequestAsync` (HTTP, query) và `CommandAsync` (Azure Service Bus, command); contract dùng chung qua NuGet `__contract`; retry `DefaultMsgSenderWithRetryFactory`.
- Handler trả `OneOf<TSuccess, Error>` (không throw cho lỗi nghiệp vụ). Handler tách `TenancyHandler` / `TenantlessHandler`; mọi query phải lọc `TenantId` (có TenancyInterceptor).
- Data: **Entity Framework 6** (`System.Data.Entity.DbContext`, `IDbSet`, Z.EntityFramework.Plus.EF6) chạy trên .NET 8, + Dapper, SQL Server, có read-only context. **Không phải EF Core.**
- Test: **MSTest** + AutoFixture + AutoMocker (không phải xUnit/Moq).
- Frontend Web: Razor + jQuery + **Vue component nhúng trong trang** (gulp/babel). Không thấy React trong phần user sửa.
- MediatR có trong package Domain.Models nhưng handler chính dùng `IHandler<TMsg, OneOf<...>>` tự viết.
- Azure DevOps (PR "Merged PR 85354…"), code review với team UK, có nhánh uat.

## 4 feature (module Projects và Jobs)
1. **Project Cost Breakdown (Proj43, 01/2026)** — tab Summary của Project: chi phí **Actual vs Estimated** theo 10 loại (Material, Labour, Expense, Subcontractor, Travel, Callout, Mileage, Overtime, Schedule of Rates, Other) + **Cost Variance**, **Actual/Estimated Profit & Margin**, quy đổi đa tiền tệ. Estimated lấy từ dòng của Project Quote Sections, Actual từ job cost lines + PO. User sửa `GetProjectJobCostHandler` (thêm EstimatedCost, CostVariance), `ProjectController`, view model, UI mới.
2. **Customer Contract cho Project (Proj62, 01–04/2026)** — dropdown Customer Contract ở Project Details / Project Quote; ẩn/hiện theo tenant có subscribe app Customer Contract; **Audit & Traceability**: audit message tạo/sửa Project mang CustomerContractId, lưu MongoDB có version (rowversion → ulong), unit test audit handler; **DocX tags** mới cho template Project Invoice, Application (T&M application for payment), Quote, cập nhật system template + guideline; logic **Previously Claimed** theo từng dòng khi invoice cộng dồn (cumulative).
3. **Selling Rate Times & Holidays (03–04/2026)** — lưới tuần: các khoảng thời gian (ngày/giờ/phút bắt đầu–kết thúc) gắn giá bán, màu, loại (pay band / holiday), liên kết **Pay Band**; lưới kéo-thả có chế độ read-only; logic "chargeable" của selling rate; nhiều bug critical (không lưu được pay band, validate). Có unit test. Entity `SellingRateTime`.
4. **Job Spend Limit (05–06/2026, làm cùng Harrison Nguyen)** — ước tính chi tiêu của Visit so với hạn mức của Job: banner OverLimit/InLimit (lần visit 1 so với hạn mức, visit 2+ so với **phần còn lại** sau các visit trước), cờ **RedeployRequired** khi hạn mức đổi sau khi visit đã deploy; **BO notification** (fan-out tới role Admin/JobDesk/Costing, idempotent theo `EventIdempotentId`), **CP** (Customer Portal) cho phép khách sửa spend limit, **permission** mới (Settings>Staff>Business>Job>Job Spend Limit, file mapping quyền CP). User viết `GetVisitSpendEstimateBannerMsgHandler`, phần BO noti, CP, permission, nhiều bugfix.
- Khác: Projects Dashboard pagination, fix multi-currency, chuyển 1 component jQuery → Vue (bị revert rồi làm lại), test SchedulerController.

## ⚠️ Lệch giữa CV và code
CV ghi "Entity Framework Core, MediatR, React". Code: **EF6**, handler tự viết (OneOf), Vue/jQuery, Azure Functions + Service Bus + MongoDB. Cần user quyết định sửa CV hoặc chuẩn bị cách nói trung thực.
