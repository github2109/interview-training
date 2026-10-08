# Career facts — Dinh Quang Hiep (đã kiểm chứng)

Nguồn sự thật cho mọi lần sửa CV. Mỗi mục ghi rõ **nguồn kiểm chứng**: git (repo trong `~/Desktop/Company/MainFolderJob`, `~/Desktop/ExtraJob`), tài liệu nội bộ, hoặc user xác nhận.
Chỉ đưa vào CV những gì có ở đây. Thông tin mới cần kiểm chứng xong mới thêm vào file này.

## Thông tin cá nhân
- Da Nang, Vietnam • quanghiep2109@gmail.com • 0853163302
- LinkedIn trên CV: `linkedin.com/in/đinh-quảng-hiệp-41815b239`. User có gửi URL khác: `linkedin.com/in/dinhquanhiep2109` → **chưa chốt** URL nào đúng.
- Không đưa: Facebook, GitHub (`github2109` không có nội dung đáng xem).
- Tiếng Anh: "good at reading and listening; currently studying for PTE Academic". **Không** ghi TOEIC 600, **không** ghi "Limited/Professional working proficiency".
- Học vấn: Bachelor of IT, Danang University of Science and Technology, Jul 2020 – Jan 2025, GPA 3.66/4. Học bổng 2020 (đầu vào 50% học phí kỳ đầu; khuyến khích học tập GPA 9.04/10) và 2022 (GPA 9.01/10). Giải Nhất Vật lý cấp thành phố 2019 → không đưa vào CV.

## Timeline (theo commit đầu/cuối của user)
| Giai đoạn | Thời gian | Nguồn |
|---|---|---|
| Astraler — Backend Developer Intern | Jul 2022 – Nov 2022 | user |
| Geargames — Junior Fullstack Engineer | Dec 2022 – Oct 2023 | hợp đồng (user) |
| Geargames — Fullstack Engineer (chức danh hợp đồng: "Engineer", tương đương middle) | Nov 2023 – Sep 2026 | user |
| Game configuration platform (tool-v2, trolls, cbg, fm) | Dec 2022 – Nov 2023 | git |
| EIM (employee management) | Nov 2023 – May 2024 | git (eim-tool: 268 commit) |
| Altar of Sacrifice + NFT Commerce | May 2024 – Dec 2024 | git |
| Tangram level tool (nhỏ, 9 commit) | Dec 2024 | git → không đưa vào CV |
| PlaySweeps | Jan 2025 – Sep 2026 | git (web từ 01/2025, backend từ 02/2025) |
| Joblogic — part-time freelance qua công ty HMT (không ghi tên HMT) | Jan 2026 – Jun 2026 | git + user |
| Bị layoff khỏi Geargames | Sep 2026 | user — không ghi lý do lên CV |

**Không** ghi "Senior" (hợp đồng không phải Senior). Không ghi dòng "Promoted from Junior" (user đã bỏ).

## PlaySweeps (client: PLAYSTUDIOS) — US sweepstakes gaming platform
- Gọi là "sweepstakes gaming platform". **Không dùng "casino", "real-money".**
- Quy mô: **2M+ registered players** (user). DAU ~5.5–6.8K, user mới ~500–1.1K/ngày (Splunk dashboard) → **không** đưa DAU, doanh thu (~30K USD/ngày), lợi nhuận lên CV (bảo mật, công ty niêm yết NASDAQ: MYPS).
- Backend `playsweeps-backend`: .NET 8, khoảng 150 project. User có **khoảng 1.330 commit**, nhiều nhất team. Data access dùng **Dapper + stored procedure + LINQ**, DI bằng **Autofac**. Cosmos DB, Redis, Azure (Functions, Service Bus, Event Hub, Key Vault, App Insights).
- Web `playsweeps-web`: React 18, Redux, khoảng 340 commit của user (01/2025 – 09/2026).
- Vai trò: **feature lead** (không phải team lead), review chéo PR (lead feature nào thì review kỹ feature đó), on-call. Không phỏng vấn tuyển người.
- Đã làm (git):
  - **Socure KYC** cho user US: DocV (ID + selfie), SSN, soft KYC/manual review. Tích hợp ban đầu do `huyenntl` làm (10/2024); user **tiếp quản**, tự tìm hiểu dashboard/decision module, sửa prototype sai của client → chạy ổn định trên production. Viết là "Owned… reworking the initial prototype", không viết "built from scratch".
  - **Quest Engine V2** (Personalized Quests / Mission Engine): user viết TDD (07/2026), làm từ thiết kế đến release, **đã lên production**. Công thức nghiệp vụ (ncalc) do **client thiết kế**; user làm rõ requirement và viết technical design. Cosmos DB lưu state, Redis + RedLock, **idempotency key cho claim**.
  - **Pragmatic Play** seamless wallet: bet/result/refund/promo-win/free-spin/buy-bonus hook, xác thực hash, khoá pending wager, **idempotency** (user xác nhận; code có `GetByRoundIdAsync`).
  - MFA + trusted device, multi-account abuse prevention, spend limit, redemption (Skrill, ACH, Prizeout, Paysafe), Apple Pay (FE).
  - Live Ops: **setup và vận hành config trên AVA** (remote config / A/B testing của PLAYSTUDIOS), tối ưu fetch/cache AVA; **Kinoa** (Live Ops/CRM): event OnGameSpin/Win/Lose, quest event, polling API.
  - Marketing/analytics: Braze, Singular, Scaleo, **Google Tag Manager**, Kinoa; BI event tracking. PLAYSTUDIOS Nexus (cross-app balance sync).
  - **Exponential rate limiting** cho các API nhạy cảm (user).
  - Viết 3 TDD: Quest Engine V2, Banner System (09/2025), CRM Direct-Target Offers (08/2026).
  - Unit test xUnit/Moq: khoảng 200 file test.
  - On-call: theo dõi exception spike, điều tra bằng **Application Insights, Grafana Loki, Splunk** (Splunk nhận BI event, dùng để lần theo các bước user đã đi qua), ra hotfix, chốt giải pháp với tech lead và QA.
  - Rive: user làm **template Rive cho Popup/Banner/Widget manager**, cache file .riv, event CTA, quy ước file .riv v2, làm việc với designer nước ngoài. Hook gốc do NhoNH tạo, RiveView do người khác mở rộng sau → viết "Rive animation layer", không viết "Rive codebase".
  - Azure Functions/Event Hub: user **không tự setup**, có cấu hình và vận hành, hiểu cách hoạt động → chỉ ghi trong stack, không ghi "built the worker".
  - Agile **Scrum**, Jira (khoảng 354 ticket WIN-xxxx).
  - Giao tiếp: Slack hằng ngày và họp technical design với team PLAYSTUDIOS (Mỹ).
- Cơ chế balance (để trả lời phỏng vấn): Sweeps Coin do **Nexus** sở hữu (gửi delta + TransactionId GUID; stored procedure của Nexus kiểm tra idempotency rồi kiểm tra số dư và cập nhật; không dùng queue). Bảng SQL `PlayerBalances` là bản sao, ghi giá trị tuyệt đối qua `SetPlayerBalanceChange_v0_2`. Lock Redis ở BE: spin theo (player, game), deposit/redemption theo transaction, PrizeOut theo player.

## Altar of Sacrifice (client: Immutable, game Guild of Guardians)
- Go (Gin), MongoDB, Redis, AWS (KMS, S3, SES), go-ethereum, Immutable zkEVM/Passport, Segment, New Relic.
- API: recipe/sacrifice engine, mint cap, streak breaker (pity), web2 asset, batch sacrifice, xử lý webhook burn/mint qua Redis queue có tracking lỗi.
- Client: React 18, Redux, @biom3, Immutable Passport, làm đợt overhaul (10–11/2024). Admin: Vue 3 + Pinia.
- Commerce: Next.js storefront + plugin WooCommerce (PHP): bonding-curve discount, allowlist.
- Client phản hồi tốt khi bàn giao (user).

## Internal platforms (Geargames)
- **EIM:** NestJS, TypeScript, TypeORM, MySQL (`mysql2`, **không phải PostgreSQL**), Redis, JWT/Passport, Swagger, @nestjs/schedule, cache-manager, throttler. Frontend React + TanStack Query + Ant Design. User sửa: 39 module, 28 controller, 172 service, 46 entity, 26 migration, 10 subscriber. Module chính: leave-time, employee, project, notifications, accrued-leave-hours, lock-record, overtime-request.
- **Game config (tool-v2…):** NestJS, TypeORM, MariaDB, Protobuf (protobufjs), ExcelJS, React + Ant Design. Import/export Excel blueprint, JSON diff trước khi deploy, Protobuf có version, link player với social account. Tool crawl/automation cho data team (user).
- Jest: chỉ khoảng 3 file test → CV ghi "Jest" trong danh sách unit testing (user chọn).

## Joblogic (part-time freelance, client UK)
- .NET, **ASP.NET MVC** (20 view .cshtml, 27 controller), **Entity Framework Core**, **MediatR**, SQL Server, React, Azure. Platform microservice có sẵn → viết "delivered features", **không** viết "built microservice architecture".
- Feature: Quoted Cost Breakdown, customer contract + audit + DocX template tags, Selling Rate Times & Holidays (pay band), Job Spend Limit (BO notification, CP, permission). Có viết unit test.

## Astraler
- Lead team intern 4 người, ứng dụng driver-license, Node.js.

## Kỹ năng KHÔNG đưa vào CV (không đủ bằng chứng)
PostgreSQL, Kubernetes/Helm (chỉ sửa config Jenkins/Helm values), Java, C/C++, Python (chưa xác nhận), Express (riêng lẻ), GitHub Actions.
