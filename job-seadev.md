# Mục tiêu: SEADEV — C# Developer (ShedPro Ops Hub), Đà Nẵng

Nguồn: https://seadev.us/career/c-developer/ (đọc 2026-10-13)

## JD tóm tắt
- Team ShedPro, báo cáo trực tiếp Product Manager. Sản phẩm SaaS cho doanh nghiệp bán nhà kho/mái che (shed, carport) ở Bắc Mỹ.
- **Ops Hub**: báo giá (quoting) → đơn hàng (sales order) → hợp đồng thuê-mua (Rent-to-Own, RTO) → theo dõi sản xuất → lên lịch giao hàng.
- **Tiếp quản code từ đối tác ở Mỹ**, dẫn dắt tính năng mới, giữ hiệu năng, chất lượng, khả năng bảo trì lâu dài.
- Yêu cầu: C#/.NET (+ .NET Core) ≥ 3 năm; ASP.NET MVC và/hoặc Web API; AWS/cloud; frontend (React/Angular/Vue) là điểm cộng; design pattern + refactoring; clean code; Git; Agile; REST; unit test (cộng); tiếng Anh (cộng).
- Văn hoá: hiểu nghiệp vụ đằng sau tính năng, làm việc sát PM, "1% improvements", accountable.

## Đối chiếu với kinh nghiệm user
| Yêu cầu | Bằng chứng thật | Khoảng trống |
|---|---|---|
| ASP.NET MVC, EF Core | **Joblogic** (client UK): ASP.NET MVC, EF Core, MediatR, SQL Server — **Quoted Cost Breakdown, customer contract + audit, DocX template** (rất gần nghiệp vụ Ops Hub) | Ôn Razor/MVC model binding, EF Core sâu |
| Web API, REST | Sweeps .NET 8, NestJS EIM | Đã học Buổi 2 |
| AWS | Go project: KMS, S3, SES. Chủ yếu Azure | **Map Azure → AWS** (Service Bus→SQS/SNS, Functions→Lambda, Key Vault→Secrets Manager/KMS, App Insights→CloudWatch/X-Ray, Blob→S3) |
| Design pattern, refactoring | Repository/Dapper, MediatR, Quest Engine design | **Refactoring legacy khi tiếp quản code**: characterization test, strangler fig, seams |
| Unit test | xUnit/Moq ~200 file (Sweeps), Joblogic có test | Test pyramid, test code legacy, Testcontainers |
| Frontend | React 18, Redux, TanStack Query, Vue 3 | Đủ |
| Hiểu nghiệp vụ, làm với PM | TDD Quest Engine, làm rõ requirement với client | Kể STAR |

## Lộ trình ưu tiên (thay thứ tự plan.md cho mục tiêu này)
1. **EF Core + SQL + transaction** (Buổi 3 hiện tại) — Ops Hub là CRUD nặng nghiệp vụ, dữ liệu quan hệ.
2. **Domain modeling cho Ops Hub**: state machine Quote → Order → RTO contract → Production → Delivery; pricing/tính giá; audit; xử lý tiền (decimal, làm tròn, lịch trả góp RTO).
3. **Design patterns + refactoring + tiếp quản legacy** (strategy, factory, specification, state; code smell; characterization test; strangler fig).
4. **Unit testing** (xUnit, Moq/NSubstitute, test builder, integration test với WebApplicationFactory + Testcontainers).
5. **ASP.NET MVC** (Razor, model binding, validation, anti-forgery, over-posting) + ôn Buổi 2.
6. **AWS cho dev .NET** (map từ Azure).
7. **Behavioral (tiếng Anh)**: tiếp quản codebase, làm việc với PM, ví dụ Joblogic quoting/contract, "1% improvements".
8. **Mock interview** 45–60 phút theo JD + một bài system design nhỏ (scheduling giao hàng / RTO payment schedule).

Lược bớt cho job này: distributed systems sâu, Service Bus/saga (chỉ ôn mức nói được).

## Team thật: ShedPro Ops Hub (nghiên cứu 2026-10-16)
Nguồn: release notes shedpro.co (01–10/2026), App Store "ShedPro Ops Hub" (driver app), JD.
- **Ops Hub** = back-office vận hành cho nhà sản xuất/đại lý shed (multi-tenant, "Company", "Store Teams", Region). Web app + **Driver App** mobile (lịch giao, xác nhận giao, ảnh, thanh toán Stripe).
- Module thấy trong release notes:
  - **Quote** (Finalize & Lock Quote, Quote PDF có 2D floorplan, custom-build quote từ 3D)
  - **Cash Sale** (invoice PDF, Acceptance of Contract + T&C rich text, chữ ký nhiều trang)
  - **RTO Contract** (template PDF theo từng công ty RTO: Premier Rentals, DMD Solutions; chọn RTO option đủ điều kiện; credit check text)
  - **Inventory** (đơn vị tồn kho, bán web, giá giảm, huỷ inventory, export)
  - **Production** (Production Queues, sắp xếp build list thủ công)
  - **Delivery** (lịch giao `deliveryTime` + `estimatedDeliveryOn` UTC, Delivery Confirmation file, SMS/email khi giao xong)
  - **Thuế** (Ziptax API v6, tax suggestion theo địa chỉ), **thanh toán** (Stripe web + driver app, deposit, balance due)
  - **Tích hợp**: đồng bộ 3D Config → Ops Hub (mapping SKU, lỗi tích hợp), ShedSuite, Zapier, WooCommerce web template
  - Notifications email/SMS, History Notes (audit), Custom Tags, Company Settings, export dữ liệu
- Loại bug thường gặp (gợi ý câu hỏi phỏng vấn): **DST làm sai ngày giao dự kiến**, timestamp History Notes lệch múi giờ, **balance due tính sai**, ký tự đặc biệt làm hỏng PDF, layout PDF, crash khi lưu dữ liệu nhúng, mapping SKU.
- Hệ quả cho ôn tập: thêm **tạo tài liệu PDF/e-signature** (khớp Joblogic DocX template tags), **tích hợp bên thứ ba** (webhook, retry, idempotency — khớp Sweeps), **thời gian/múi giờ/DST**, **tính tiền: deposit/balance due/thuế**, multi-tenant settings.

## Lộ trình cập nhật (2026-10-16) — ưu tiên Joblogic
CV gửi đi ghi: "Delivered Projects and Jobs module features for a UK field-service management SaaS on a .NET microservice platform, including cost breakdowns, contract audit trails, pay-band rates and spend limits. Wrote unit tests… code review with the client's UK team."
- **J1. Thu thập sự thật Joblogic** (user trả lời bảng câu hỏi) → ghi `context/joblogic.md`. Không bịa.
- **J2. Kể dự án 2 phút + đào sâu 4 feature** (STAR tiếng Anh), mỗi feature nối sang Ops Hub:
  - Quoted Cost Breakdown ↔ Quote pricing, Finalize & Lock Quote, balance due
  - Customer contract + audit + DocX template tags ↔ RTO/Cash Sale PDF template theo công ty RTO, History Notes
  - Selling Rate Times & Holidays (pay band) ↔ tính giá theo thời gian, ngày lễ, timezone/DST, lịch giao
  - Job Spend Limit (BO notification, CP, permission) ↔ phân quyền, ngưỡng duyệt, thông báo email/SMS
- **J3. Kỹ thuật Joblogic bị hỏi sâu**: ASP.NET MVC (Razor, model binding, anti-forgery), EF Core, MediatR (CQRS, pipeline behavior), microservice platform có sẵn, unit test, làm việc remote với team UK / code review.
- **J4. Mock Q&A** kiểu interviewer SEADEV: "tell me about Joblogic" → follow-up → "how would you apply that to Ops Hub".
Sau đó: domain Ops Hub (balance due, DST, PDF/template, tích hợp Stripe/Ziptax), refactoring legacy, AWS, behavioral, mock interview.

## Lộ trình Joblogic → SEADEV (cập nhật 2026-10-16, theo yêu cầu user)
User **không muốn** nêu điểm yếu/tự phê bình code Joblogic; tập trung vào việc đã làm, cách giải quyết vấn đề, độ hiểu hệ thống.
- **JA. Business chung** Joblogic (field service) ↔ Ops Hub (shed): quote→job/order, pricing (rate, uplift, chargeable, thuế), costing & margin, contract định kỳ vs RTO, invoicing (cumulative/retention vs deposit/balance due), document template, scheduling/dispatch + mobile, approval/limit/permission, subscription gating, audit, integration.
- **JB. Pattern & công nghệ**: multi-tenancy, microservice messaging (request/command, Service Bus, retry, idempotency), OneOf result, audit có version, document generation bằng tag, feature gating theo gói, RBAC, notification fan-out, EF6 vs EF Core, Azure Functions; map Azure→AWS.
- **JC. 4 feature theo khung "vấn đề → hiểu nghiệp vụ → thiết kế → edge case → kiểm chứng"**, bản kể tiếng Anh + câu đào sâu + nối Ops Hub.
- **JD. Mock interview**.

## Người phỏng vấn & nguyên tắc trả lời (2026-10-16)
- Phỏng vấn bởi **Solution Architect + Product Owner**.
- **Không nhắc chi tiết nội bộ ShedPro** (release notes, bug, tên đối tác RTO, Ziptax…) trong câu trả lời — chỉ dùng để tự định hướng ôn tập. Được phép dựa vào phạm vi **công khai trong JD** ("quoting, sales orders, RTO contracts, production tracking, delivery scheduling", "taking over from a US partner") và nói dạng giả định + hỏi lại.
- SA quan tâm: hiểu hệ thống, trade-off kiến trúc, multi-tenant, tích hợp, dữ liệu/tiền/thời gian, tiếp quản legacy, chất lượng (test, review).
- PO quan tâm: hiểu nghiệp vụ, làm rõ yêu cầu, edge case, ưu tiên, giao tiếp, giao giá trị theo từng bước, xử lý thay đổi yêu cầu.
