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
