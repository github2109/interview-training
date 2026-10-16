# Joblogic — kiến trúc hệ thống (ôn cho Solution Architect)

Nguồn: CLAUDE.md của từng service trong `joblogic-web`, `joblogic-mobile` + code đã kiểm (ResolveTenantSettingMiddleware, JobLogicContext). Lưu ý: tài liệu ghi "EF Core", nhưng DbContext của domain Core là **EF6** (`System.Data.Entity`) → nói "EF (EF6 ở domain Core cũ, EF Core ở phần mới) + Dapper".

## Bức tranh
- Clients: Web back-office (ASP.NET Core MVC + Razor + Vue nhúng, Kendo), Customer Portal, Mobile app (kỹ thuật viên, offline-first), WebAPI v1/v2 (JWT) cho đối tác/mobile, Webhooks (14+ nguồn ngoài, tenantless), YARP reverse proxy (blob, định tuyến vùng).
- ~30 "Jicroservices" = Azure Functions v4 isolated .NET 8: Core, License, Role, Audit, DocGen, Notification, File, Schedule, Payment, Workflow, Batch, Replication, Integration…
- Hạ tầng: SQL Server **sharded theo tenant**, MongoDB (audit, workflow, offline visit, GPS), Redis, Blob, Azure Service Bus (queue `-cmd` + topic event), Azure Search, App Configuration + FeatureManagement, App Insights, Azure DevOps + Sonar.

## Request pipeline của một Jicroservice
Trigger (HTTP / ServiceBus / Timer / WarmUp) → `IDispatcher` → middleware (ResolveTenantSetting: lấy **shard key** của tenant từ License (cache), kiểm tra tenant **active / frozen**) → `IHandler<TMsg, OneOf<TRes, Error>>` → service → EF/Dapper/Mongo.
- Giao tiếp: `RequestAsync` (HTTP, cần kết quả), `CommandAsync` (Service Bus, fire-and-forget có retry), **event** publish lên topic → nhiều service subscribe (Audit, Notification 185 handler, Workflow, Replication).
- Contract `*Msg/*Response` đóng gói NuGet (`__contract`), client NSwag; `DefaultMsgSenderWithRetryFactory`.

## Multi-tenancy
- Tenant context (operation info: TenantId, user) đi theo **mọi** message; tenant → shard key → connection string.
- Handler tách **Tenancy** (đa số) / **Tenantless** (onboarding, cleanup, quét mọi tenant). Timer tenantless quét tenant hợp lệ rồi **fan-out** message theo từng tenant theo batch. Webhook tenantless tự tìm tenant từ payload.
- Query tenant phải lọc TenantId (TenancyInterceptor). Cleanup tenantless dùng `sp_set_session_context` để vượt policy (gợi ý có Row-Level Security).
- Onboarding: `CreateCompanyHandler` + initial template data.

## Subscription & feature gating (License)
- Product tier (FSM, FSM Plus, Enterprise, CAFM…), 60+ `AppModule`, module add-on, tính phí PerUser/PerLicense qua Stripe/GoCardless, freeze/unfreeze, cảnh báo hết hạn (timer).
- Feature flag hệ thống (Azure App Config) + opt-in theo tenant (AI features). UI ẩn/hiện theo module (vd. Customer Contract field — user đã làm).

## Identity & RBAC (Role)
- 3 loại user: Web (back-office, OIDC/SSO), Mobile (kỹ thuật viên, JWT + refresh token, quản lý thiết bị, thu hồi session), Portal (khách hàng, role + permission chi tiết). Permission mới qua mapping file (user đã thêm Job Spend Limit permission + mapping CP).

## Các service đáng nói
- **Audit**: MongoDB theo tenant, 46+ loại entity, entry có version (rowversion), full content khi tạo/thiếu bản trước, giữ 6 tháng (timer).
- **DocGen**: 68+ loại tài liệu; template trên Blob (**template tenant → fallback template hệ thống**); Aspose.Words thay placeholder → PDF / DOCX; cache Redis theo checksum 7 ngày; Core cung cấp "document data" (handler GetXxxDocumentDataMsg), DocGen chỉ render.
- **Notification**: Email SendGrid (tracking open/click/bounce), SMS Twilio (1 chiều/2 chiều), push FCM/APNS, in-app, webhook ra ngoài (retry tối đa 3 lần, timer); fan-out theo role; idempotent theo OperationId.
- **Schedule**: timer mỗi phút, recurring job, nhắc lịch, export báo cáo; quét tenant theo license rồi dispatch.
- **Payment**: Stripe (payment intent, SCA, Klarna/iDEAL), **Stripe Connect** cho từng tenant, xử lý webhook, timer retry backoff, timer đối soát dữ liệu Stripe hằng ngày.
- **Workflow**: engine workflow trực quan (định nghĩa trong MongoDB), trigger theo event entity (Job/Quote/Invoice/Visit…) hoặc cron, timer bù lần chạy bị lỡ.
- **Batch**: import CSV 40+ loại (validate → map → **distributed lock** → import → lịch sử → xuất lỗi ra Blob), thao tác hàng loạt, email hàng loạt.
- **Replication**: đồng bộ sang **Azure Search** (read model, 130+ field, n-gram) theo event + range sync tăng dần theo rowversion + health check → CQRS read side.
- **File**: 41+ loại attachment, Blob, FTP/SFTP, thumbnail.

## Mobile (joblogic-mobile) — offline-first
- OfflineService (API v1/v2 cho app), MobileSync (đồng bộ form, job, attachment, expense, visit offline lưu Mongo, sync task + acknowledge, cleanup), Mobile (tính **library hash** cho dữ liệu tham chiếu: parts, forms… để thiết bị chỉ tải lại thư viện đã đổi; push FCM/APNS), GPSTracking (Mongo).
- Visit được "deploy" xuống thiết bị → dữ liệu trên máy là bản chụp; đổi ở văn phòng → cần redeploy/đồng bộ lại (user đã làm cờ RedeployRequired cho spend limit).

## Map Azure → AWS
Functions→Lambda; Service Bus queue/topic→SQS / SNS(+SQS) hoặc EventBridge; Service Bus sessions→SQS FIFO message group; App Service→ECS/Fargate/Elastic Beanstalk; Blob→S3; Azure SQL→RDS SQL Server/Aurora; Cosmos/Mongo→DocumentDB/DynamoDB; Redis→ElastiCache; App Configuration+FeatureManagement→AppConfig/Parameter Store; Key Vault→Secrets Manager/KMS; App Insights→CloudWatch + X-Ray; Azure Search→OpenSearch; SendGrid/Twilio→SES/SNS (hoặc giữ); Azure AD B2C→Cognito; YARP/Front Door→ALB/API Gateway/CloudFront; Azure DevOps→CodePipeline/GitHub Actions.
