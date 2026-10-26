# SEADEV — C# Developer (ShedPro Ops Hub): FILE HỌC TỔNG HỢP

Cập nhật: 2026-10-23. Gộp từ: `job-seadev.md` (JD), `notes/S-seadev-interview-kit.md`, `notes/S-seadev-interviewer-profile.md`, `plan.md`, `plan-joblogic-3-buoi.md`, `progress.md`, `notes/01..03`, `notes/J-*`, `context/career-facts.md`, `context/joblogic.md`, `question-bank.md`.
Nguyên tắc: giải thích tiếng Việt, **câu trả lời mẫu tiếng Anh**. Câu mẫu chỉ dùng sự thật đã kiểm chứng; chỗ nào cần Hiệp tự điền ghi **[Hiệp điền]**.

---

## 0. Cách dùng file này

### 0.1 Ai phỏng vấn, họ quan tâm gì
- **Vòng 1 = culture & core values** → học ở file riêng `notes/S-seadev-culture.md`. File này dành cho **vòng tech** (SA + PO). Tuy vậy, interviewer tech cũng sẽ nghe xem bạn có sống theo 5 value không: **1% Improvement, Driven by Customer Success, Enjoy Problem Solving, Be Accountable, Love our People & Communities** — câu nào nối được thì nối (đánh dấu 🟢 ở dưới).
- **Solution Architect (có thể là Khiet Vo)**: gốc frontend / full stack JS–TS (React, TypeScript, UX/UI, Node), skill tự khai ở vai trò SA: **Software Architecture, CI/CD**; trước đó **AWS** (AgilityIO), **REST, Clean Coding** (Urbanise, SaaS quản lý chung cư/facilities: tiền định kỳ, workflow bảo trì, tài liệu, tích hợp ngân hàng). Không khai C#/.NET → ít soi nội tại CLR, soi **thiết kế, API, chất lượng code, pipeline, cloud**.
- **Product Owner / PM**: nghiệp vụ, làm rõ yêu cầu, edge case, ưu tiên, giao tiếp, thái độ "1% improvements", accountable.
- Bối cảnh JD: tiếp quản code từ **đối tác Mỹ**, **dẫn dắt** tính năng mới, giữ hiệu năng, chất lượng, bảo trì lâu dài. Yêu cầu: **≥ 4 năm** C#/.NET, ASP.NET MVC và/hoặc Web API, AWS/cloud, design pattern + refactoring, clean code, Git, Agile, REST; cộng điểm: React/Angular/Vue, unit test, tiếng Anh.

### 0.2 Bảng tổng quan: section × khả năng bị hỏi
Thang ước lượng (chủ quan, dựa trên JD + profile SA + vai trò PO): **Rất cao ≥ 80%**, **Cao 60–80%**, **Trung bình 40–60%**, **Thấp 20–40%**, **Rất thấp < 20%**.
"Trạng thái" = mức Hiệp đã ôn (✅ chắc, 🟡 cần ôn lại/luyện nói, ❌ chưa học).

| # | Section | Ai hỏi | Khả năng | Trạng thái | Ưu tiên học |
|---|---|---|---|---|---|
| 1 | Giới thiệu bản thân, lý do ứng tuyển, câu hỏi cá nhân | SA + PO | Rất cao 95% | 🟡 | 1 |
| 2 | Kể dự án trong CV (PlaySweeps, Joblogic) + đào sâu | SA + PO | Rất cao 95% | 🟡 | 1 |
| 3 | Kiến trúc tổng thể, layering, SOLID, monolith vs microservices, scale | SA | Rất cao 90% | 🟡 | 1 |
| 4 | REST API design | SA | Rất cao 85% | ✅ lý thuyết | 1 |
| 5 | Clean code + code review (có bài review code) | SA | Rất cao 80% | 🟡 | 1 |
| 6 | Design patterns | SA | Cao 80% | ❌ | 1 |
| 7 | Refactoring + tiếp quản code partner Mỹ | SA + PO | Cao 80% | ❌ | 1 |
| 8 | Nghiệp vụ Ops Hub (quote → order → RTO → production → delivery, tiền, thời gian, tài liệu) | PO (+SA) | Rất cao 85% (PO) / Cao 60% (SA) | 🟡 | 1 |
| 9 | Câu hỏi PO: làm rõ yêu cầu, edge case, ưu tiên, thay đổi phạm vi | PO | Rất cao 85% | 🟡 | 1 |
| 10 | Behavioral STAR (tiếng Anh) | SA + PO | Cao 75% | ❌ | 1 |
| 11 | C# & .NET nền tảng (OOP, kiểu dữ liệu, record, LINQ, GC, IDisposable…) | SA | Cao 65% | 🟡 | 2 |
| 12 | Async / concurrency / thread pool | SA | Cao 60% | ✅ | 2 |
| 13 | ASP.NET Core: DI, middleware, filter, exception handling | SA | Cao 65% | ✅ | 2 |
| 14 | ASP.NET MVC (Razor, model binding, validation, CSRF, over-posting) | SA | Cao 60% | ❌ | 2 |
| 15 | EF Core / SQL / transaction / index / migration | SA | Cao 70% | ✅ | 2 |
| 16 | Concurrency dữ liệu, idempotency, chống double submit | SA | Cao 60% | ✅ | 2 |
| 17 | Multi-tenant SaaS | SA | Trung bình–Cao 60% | ✅ | 2 |
| 18 | Unit test / integration test | SA | Cao 65% | ❌ | 2 |
| 19 | Frontend (React/TS/JS/HTML/CSS) + hợp đồng FE–BE + UX | SA | Trung bình–Cao 60% | 🟡 | 2 |
| 20 | CI/CD, deploy, release an toàn | SA | Trung bình–Cao 60% | ❌ (điểm yếu) | 2 |
| 21 | AWS (map từ Azure) | SA | Trung bình–Cao 60% | 🟡 | 2 |
| 22 | Tích hợp bên thứ ba, resilience (timeout, retry, circuit breaker, webhook) | SA | Trung bình 55% | 🟡 | 2 |
| 23 | Messaging, background job, outbox, caching | SA | Trung bình 50% | 🟡 | 3 |
| 24 | Security (OWASP, authN/Z, JWT/cookie, XSS, CSRF, SQLi, secret) | SA | Trung bình 50% | ❌ | 3 |
| 25 | Observability, debug sự cố, performance | SA | Trung bình 50% | 🟡 | 3 |
| 26 | System design nhỏ (lịch giao hàng, lịch trả góp RTO, sinh PDF, thông báo) | SA | Trung bình 40% | ❌ | 3 |
| 27 | Git | SA | Trung bình 40% | ❌ (dễ) | 3 |
| 28 | Agile/Scrum, estimate, làm việc remote với Mỹ | PO + SA | Trung bình 55% | ❌ (dễ) | 3 |
| 29 | Câu hỏi ngược cho interviewer | SA + PO | Rất cao 95% (chắc chắn được mời hỏi) | 🟡 | 1 |
| 30 | Checklist trước giờ phỏng vấn + lỗi hay mắc | — | — | — | Đọc cuối |
| 31 | Phụ lục: thuật ngữ, câu tiếng Anh hay dùng, bảng con số | — | — | — | Tra cứu |

### 0.3 Lộ trình học đề xuất (gộp `plan-joblogic-3-buoi.md` + kit)
| Ngày | Nội dung | Section |
|---|---|---|
| 1 | Pitch + câu hỏi cá nhân + kể PlaySweeps và Joblogic (kiến trúc 2 phút + 4 feature) | 1, 2 |
| 2 | Kiến trúc + REST + clean code + bài code review | 3, 4, 5 |
| 3 | Design patterns + refactoring + tiếp quản legacy | 6, 7 |
| 4 | Nghiệp vụ Ops Hub + câu hỏi PO | 8, 9 |
| 5 | MVC + unit test + CI/CD + AWS + frontend | 14, 18, 19, 20, 21 |
| 6 | Ôn nhanh nền .NET (đã học) + security + observability + Git/Agile | 11–17, 22–28 |
| 7 | Behavioral STAR + mock 60 phút (SA 35' + PO 25') + câu hỏi ngược | 10, 29, 30 |
Nếu chỉ còn 2 ngày: học các section **ưu tiên 1**, đọc lướt phần "Câu hỏi" của các section còn lại.

### 0.4 Khung trả lời chung (dùng cho mọi câu kỹ thuật)
1. **Định nghĩa ngắn** (1 câu).
2. **Ví dụ thật** của Hiệp (PlaySweeps, Joblogic, EIM…) hoặc ví dụ Ops Hub.
3. **Trade-off**: khi nào dùng, khi nào không.
4. **Failure mode**: nó hỏng thế nào, phát hiện bằng công cụ gì, xử lý tạm và tận gốc.
Với sự cố: **tên vấn đề → cách xác nhận (công cụ) → xử lý tạm → xử lý gốc → phòng ngừa**.
Với PO: **làm rõ (hỏi lại) → phương án nhỏ giao trước → edge case → đo kết quả**.

### 0.5 Ranh giới trung thực (đọc kỹ)
- Không nhắc chi tiết nội bộ ShedPro (release notes, tên đối tác RTO, Ziptax, bug cụ thể). Chỉ dựa vào phạm vi công khai trong JD, nói dạng "I'd assume… and I'd confirm with the PM".
- Joblogic: **EF6** ở domain Core cũ + EF Core ở phần mới + Dapper; handler tự viết trả `OneOf`; frontend **Razor + jQuery + Vue**; test **MSTest + AutoFixture + AutoMocker**; Azure Functions + Service Bus + MongoDB. Platform microservice **có sẵn** → nói "delivered features", không nói "built the architecture". Không chê code Joblogic.
- PlaySweeps: "sweepstakes gaming platform", **không** nói casino/real-money; không nói DAU/doanh thu. Vai trò **feature lead**, không phải team lead.
- CI/CD: chỉ từng sửa config Jenkins/Helm values; **không** nhận đã dựng pipeline. GitHub Actions, Kubernetes, PostgreSQL: không nhận là kinh nghiệm chính.
- Không tự nhận "Senior" về chức danh; nói "about four years of professional experience".

---

## 1. Giới thiệu bản thân & câu hỏi cá nhân — Khả năng: Rất cao (95%)

### 1.1 Pitch 60 giây
> I'm a full-stack developer with about four years of experience, strongest on the .NET backend. Most recently I worked on PlaySweeps, a US sweepstakes gaming platform with over two million registered players, on .NET 8, SQL Server, Azure and React. I was a feature lead there: I wrote technical designs, delivered features like the Quest Engine and the KYC integration with Socure, and handled on-call incidents. In parallel, I worked part-time for a UK field-service SaaS called Joblogic, on ASP.NET MVC and a .NET microservice platform, where I delivered features in the Projects and Jobs modules such as cost breakdowns, customer contracts with audit trails, and job spend limits. What attracts me to ShedPro is that the Ops Hub is a business-heavy product, quoting, contracts, production, delivery, which is very close to what I did at Joblogic, and I like working closely with a product manager to understand why a feature matters.

Bản 30 giây (khi bị giục):
> I'm a .NET full-stack developer with about four years of experience. I've worked on a US sweepstakes gaming platform with over two million players, where I led features end to end, and on a UK field-service SaaS with quoting, contracts and cost tracking, which is close to what the Ops Hub does.

### 1.2 Timeline phải thuộc (đừng nói sai)
| Giai đoạn | Thời gian |
|---|---|
| Astraler — Backend Intern (Node.js, lead nhóm 4 intern) | 07/2022 – 11/2022 |
| Geargames — Junior Fullstack → Fullstack Engineer | 12/2022 – 09/2026 |
| ↳ Game config platform (NestJS, React) | 12/2022 – 11/2023 |
| ↳ EIM (NestJS, TypeScript, MySQL, React) | 11/2023 – 05/2024 |
| ↳ Altar of Sacrifice (Go, MongoDB, AWS KMS/S3/SES, React) | 05/2024 – 12/2024 |
| ↳ PlaySweeps (.NET 8, SQL Server, Azure, React) | 01/2025 – 09/2026 |
| Joblogic — part-time freelance (ASP.NET MVC, .NET 8) | 01/2026 – 06/2026 |
| Rời Geargames (công ty tái cấu trúc) | 09/2026 |
Kinh nghiệm: tính từ 07/2022 → ~4 năm 3 tháng; full-time từ 12/2022 → ~3 năm 10 tháng. Nói "about four years".

### 1.3 Câu hỏi cá nhân hay gặp
| Câu hỏi | Ý trả lời |
|---|---|
| Why are you leaving / why did you leave? | > The company restructured and my position was affected in September. I'm now looking for a product team where I can own a business-critical system for the long term. (Không nói thêm chi tiết, không chê công ty cũ.) |
| Why SEADEV / why this role? | Sản phẩm nhiều nghiệp vụ (quote, contract, production, delivery) giống Joblogic; làm sát PM; tiếp quản và phát triển dài hạn; .NET là thế mạnh; làm với đối tác Mỹ đã quen (PLAYSTUDIOS). 🟢 Thêm purpose "Create jobs, improve lives, make awesome stuff" và value 1% Improvement / Customer Success (bản đầy đủ: `S-seadev-culture.md` 4.2). |
| What do you know about ShedPro / Ops Hub? | Chỉ nói phạm vi JD: SaaS cho doanh nghiệp bán shed/carport ở Bắc Mỹ; Ops Hub quản lý quoting, sales orders, rent-to-own contracts, production tracking, delivery scheduling; đang tiếp quản từ đối tác Mỹ. > From the job description, the Ops Hub is the operational back office for shed and carport businesses in North America — quoting, sales orders, rent-to-own contracts, production tracking and delivery scheduling — and the codebase is being taken over from a US partner. |
| Strengths? | Backend .NET, hiểu nghiệp vụ và edge case, tự đào sâu (TDD Quest Engine, tiếp quản Socure), on-call bình tĩnh. Kèm một ví dụ. |
| Weakness? | Chọn điểm yếu thật nhưng đang cải thiện, không phạm vào yêu cầu cốt lõi. Ví dụ: tiếng Anh nói (đang học PTE), hoặc chưa tự dựng CI/CD pipeline từ đầu (đang học). > My spoken English is less fluent than my reading and listening, so I'm preparing for PTE Academic and I practise explaining technical designs in English. In my last role I wrote technical designs in English and joined design meetings with the US team. |
| Where do you see yourself in 3–5 years? | Senior/tech lead cho một mảng sản phẩm, sở hữu kiến trúc và chất lượng của module, mentor người mới. Gắn với vai trò "leading new feature development". |
| What does a senior developer mean to you? | Sở hữu kết quả chứ không chỉ task: hiểu nghiệp vụ, thiết kế có trade-off, chất lượng (test, review), vận hành (monitor, on-call), giúp team. |
| How do you learn new technology quickly? | Ví dụ thật: Go + AWS (KMS, S3, SES) ở Altar; Socure tự đọc dashboard/decision module; Rive làm với designer nước ngoài. Cách học: đọc tài liệu chính thống → làm prototype nhỏ → áp dụng vào task thật → ghi lại. |
| Expected salary? | [Hiệp điền con số]. Khung: nói khoảng (range) dựa trên thị trường Senior .NET Đà Nẵng, mở thương lượng tổng gói. > Based on my experience and the market for this role, I'm looking for a range of [X–Y] gross per month, and I'm open to discussing the full package. |
| Notice period / start date? | Đã rời Geargames 09/2026 → có thể bắt đầu sớm. [Hiệp xác nhận]. |
| Are you interviewing elsewhere? | Thật lòng, ngắn gọn; nhấn SEADEV là lựa chọn ưu tiên vì nghiệp vụ phù hợp. |
| Remote or onsite? | [Hiệp điền mong muốn]. |
| Do you have any questions? | Xem section 29. **Luôn có câu hỏi.** |

### 1.4 Câu hỏi luyện
1. Tell me about yourself. (60 giây, rồi 30 giây)
2. Walk me through your CV.
3. Why did you leave your last company?
4. Why should we hire you over other candidates?
5. What's the most valuable thing you built?
6. What do you know about our product?
7. What kind of team do you work best in?

---

## 2. Kể dự án trong CV + bị đào sâu — Khả năng: Rất cao (95%)

SA và PO sẽ chọn một dòng trong CV và đào: "tell me more about X → how did you design it → what went wrong → what would you change → how would you apply it here". Mỗi câu chuyện 60–90 giây theo khung **bối cảnh → vấn đề → bạn làm gì → kết quả → bài học / nối sang Ops Hub**.

### 2.1 PlaySweeps (01/2025 – 09/2026)
Sự thật: client PLAYSTUDIOS (NASDAQ: MYPS), 2M+ registered players; backend .NET 8 (~150 project, ~1.330 commit của Hiệp, nhiều nhất team), Dapper + stored procedure + LINQ, repository bọc SP, Autofac; Cosmos DB, Redis; Azure Functions, Service Bus, Event Hub, Key Vault, App Insights; web React 18 + Redux (~340 commit). Vai trò feature lead, review chéo PR, on-call. Scrum + Jira (~354 ticket). ~200 file test xUnit + Moq.

**Kiến trúc 1 phút:**
> PlaySweeps is a .NET 8 backend with around 150 projects, a React web client, SQL Server accessed through Dapper and stored procedures, Cosmos DB for some feature state, Redis for caching and distributed locks, and Azure Functions with Service Bus and Event Hub for background processing. Player balances for Sweeps Coin are owned by a PLAYSTUDIOS service called Nexus; we sent it deltas with a unique transaction ID and kept a local mirror.

**Câu chuyện chính:**
| Feature | Ý chính để kể | Câu đào sâu dự kiến |
|---|---|---|
| **Quest Engine V2** | Viết TDD (07/2026), làm từ thiết kế đến release, lên production. Công thức nghiệp vụ (ncalc) do client thiết kế, Hiệp làm rõ requirement. Cosmos DB lưu state, Redis + RedLock, **idempotency key cho claim** | Vì sao Cosmos? Vì sao cần lock? RedLock có vấn đề gì (không có fencing token)? Chống claim 2 lần thế nào? Reward async hay sync? |
| **Socure KYC** | Tiếp quản tích hợp do đồng nghiệp làm (10/2024), tự tìm hiểu dashboard/decision module, phát hiện prototype của client có giả định sai, sửa lại tới khi chạy ổn trên production. DocV (ID + selfie), SSN, soft KYC/manual review | Tiếp quản thế nào? Webhook/callback từ vendor xử lý ra sao? Trạng thái KYC lưu thế nào? |
| **Pragmatic Play seamless wallet** | Hook bet/result/refund/promo-win/free-spin/buy-bonus; xác thực hash; khoá pending wager; idempotency | Key idempotency là gì (transaction reference, không phải roundId)? Trùng thì trả gì (replay response)? Refund đến trước bet? |
| **Nexus balance** | Gửi delta + TransactionId GUID; Nexus kiểm idempotency + kiểm số dư + cập nhật trong 1 transaction; bản SQL local là mirror ghi giá trị tuyệt đối | Điểm yếu của mirror? (response về không theo thứ tự → cần sequence check) |
| **Exponential rate limiting** | Cho API nhạy cảm (đăng nhập, OTP…) | Đa instance thì lưu counter ở đâu (Redis)? Thuật toán? |
| **MFA + trusted device, multi-account abuse, spend limit, redemption (Skrill, ACH, Prizeout, Paysafe)** | Nghiệp vụ tiền + bảo mật | Spend limit tính theo cửa sổ thời gian nào? Chống race khi 2 request cùng lúc? |
| **On-call** | Theo dõi exception spike, điều tra bằng App Insights, Grafana Loki, Splunk (theo BI event để dựng lại hành trình user), hotfix, chốt với tech lead và QA | Kể 1 vụ cụ thể **[Hiệp điền: chọn 1 sự cố có con số]** |
| **3 TDD** | Quest Engine V2, Banner System (09/2025), CRM Direct-Target Offers (08/2026) | TDD gồm những phần gì? Ai review? |

Câu mẫu Quest Engine (dẫn dắt feature):
> I led Quest Engine V2 from design to production. The client defined the reward formulas, so my first job was to clarify the requirements with them and write the technical design. Quest progress was stored in Cosmos DB, updates for the same player were serialized with a Redis lock, and claiming a reward used an idempotency key so a retry or a double click could never pay twice. I wrote unit tests around progress calculation and claim rules, and after release I monitored it in Application Insights.

Câu tự phản biện (Senior hay được hỏi "what would you change"):
> If I did it again, I'd rely less on the distributed lock for correctness: a Redis lock has no fencing token, so a paused process could still write after its lock expired. I'd make the database the arbiter — a unique constraint on the claim key and an optimistic concurrency check on the progress document — and keep the lock only to reduce contention.

### 2.2 Joblogic (01/2026 – 06/2026, part-time freelance)
**Kiến trúc 2 phút:**
> Joblogic is a multi-tenant field-service management SaaS in the UK. The front apps are ASP.NET Core on .NET 8 — a large MVC back-office with Razor views and embedded Vue components, a customer portal and a Web API for mobile and partners. Behind them are around thirty backend services running as Azure Functions, which they call "Jicroservices": Core, Audit, DocGen, Notification, Payment, Schedule and so on. Queries go over HTTP, commands go over Service Bus queues, and events are published to topics so several services can react. Handlers return a result type, OneOf success or error, instead of throwing for business errors. Data is SQL Server sharded by tenant, plus MongoDB for audit and offline mobile data, Redis and Blob storage. Tenant isolation is enforced in the database: every connection sets the tenant ID in SQL Server session context, reads go through views filtered by it, and writes are blocked by row-level security if the tenant doesn't match.

**4 feature (khung: vấn đề → nghiệp vụ → thiết kế → edge case → kết quả → nối Ops Hub)**
| Feature | Nội dung thật | Edge case để kể | Nối sang Ops Hub |
|---|---|---|---|
| **Project Cost Breakdown** (01/2026) | Tab Summary: Actual vs Estimated theo 10 loại chi phí, Cost Variance, Actual/Estimated Profit & Margin, đa tiền tệ. Estimated từ dòng của Project Quote Sections, Actual từ job cost lines + PO. Sửa `GetProjectJobCostHandler` | Đa tiền tệ (quy đổi), margin vs markup, project lớn chậm | Giá quote, margin, balance due |
| **Customer Contract cho Project** (01–04/2026) | Dropdown Customer Contract ở Project/Quote; ẩn/hiện theo tenant có subscribe app; **audit có version** lưu MongoDB; **DocX tags** mới cho template Invoice/Application/Quote; logic **Previously Claimed** khi invoice cộng dồn | Tài liệu đã phát hành không được đổi khi template đổi; feature gating theo gói | RTO/cash sale contract template theo công ty, History Notes |
| **Selling Rate Times & Holidays** (03–04/2026) | Lưới tuần: khoảng thời gian gắn giá bán, loại (pay band / holiday), kéo-thả, read-only; logic "chargeable"; sửa nhiều bug critical; có unit test | Ca vắt qua nửa đêm, ngày lễ, chồng lấn khoảng thời gian | Tính giá theo thời gian, lịch giao, DST |
| **Job Spend Limit** (05–06/2026, làm cùng một đồng nghiệp) | Banner OverLimit/InLimit: visit 1 so với hạn mức, **visit 2+ so với phần còn lại**; cờ **RedeployRequired** khi hạn mức đổi sau khi visit đã xuống thiết bị; **BO notification** fan-out theo role, idempotent theo `EventIdempotentId`; Customer Portal cho khách sửa spend limit; permission mới | Đổi hạn mức sau khi đã deploy xuống mobile; trùng event → gửi 2 thông báo | Approval/ngưỡng, thông báo email/SMS, phân quyền |

Câu mẫu Job Spend Limit (edge case nghiệp vụ, PO rất thích):
> The requirement looked simple: warn when a visit's estimated spend goes over the job's spend limit. When I walked through real scenarios, two edge cases came up. First, for the second and later visits, the comparison had to be against the remaining limit after earlier visits, not the full limit. Second, a visit could already be deployed to the engineer's mobile device when the office changed the limit, so the data on the device was stale; we added a "redeploy required" flag. The back-office notification was fan-out to the right roles and idempotent on the event ID, so a retried event didn't notify people twice.

Câu đào sâu Joblogic hay gặp:
1. Why Azure Functions instead of normal web services? (Họ chọn sẵn; nói lợi: scale theo trigger, timer/queue trigger tiện; hại: cold start, giới hạn thời gian chạy, debug khó.)
2. How do services communicate and what if a message is processed twice? (At-least-once → consumer idempotent theo OperationId/EventIdempotentId.)
3. How is tenant isolation enforced? (SESSION_CONTEXT + view + RLS block predicate + FK kèm TenantId.)
4. Why return OneOf instead of throwing? (Lỗi nghiệp vụ là kết quả bình thường; exception cho bất ngờ; caller buộc xử lý.)
5. How did you work with the UK team? (Azure DevOps PR, code review, nhánh uat; giao tiếp async.)
6. EF Core or EF6? > The core domain still uses EF6 running on .NET 8, newer parts use EF Core, plus Dapper for read-heavy queries.
7. How did you generate documents? (DocGen: Core trả document model đã tính sẵn → chọn template tenant → fallback hệ thống → thay tag `@@Tag@@` bằng Xceed DocX → Aspose.Words xuất PDF/DOCX → cache theo checksum.)

### 2.3 Dự án khác (khả năng bị hỏi thấp, chuẩn bị 2 câu mỗi cái)
- **EIM** (NestJS, TypeScript, TypeORM, MySQL, Redis, JWT, Swagger; React + TanStack Query + Ant Design): module nghỉ phép, overtime, accrued leave hours, lock record, notification. 39 module, 46 entity, 26 migration.
- **Game config platform**: NestJS, MariaDB, Protobuf có version, import/export Excel blueprint, JSON diff trước khi deploy config.
- **Altar of Sacrifice** (client Immutable): Go (Gin), MongoDB, Redis, AWS KMS/S3/SES; recipe engine, mint cap, webhook burn/mint qua Redis queue có tracking lỗi. **Đây là bằng chứng AWS thật.**
- **Astraler**: lead nhóm 4 intern, Node.js.

### 2.4 Câu hỏi luyện
1. Tell me about the most complex feature you built.
2. Draw the architecture of PlaySweeps / Joblogic. Where would it break first under 10× load?
3. What was your exact role in the Quest Engine? What did you decide and what did others decide?
4. You took over the Socure integration — what was wrong and how did you find out?
5. How did you prevent double payouts in the wallet integration?
6. What would you do differently in the Joblogic spend-limit feature?
7. How did you ensure a signed contract document doesn't change when the template changes?
8. How did the margin calculation handle multiple currencies?
9. Tell me about a time a requirement changed late. (Gợi ý: Job Spend Limit, RedeployRequired.)
10. How much of PlaySweeps backend did you know? (~150 project; feature mình lead thì nắm sâu, phần khác nắm luồng chính.)

---

## 3. Kiến trúc tổng thể, layering, SOLID, scale — Khả năng: Rất cao (90%)

JD nhấn: "clean, testable, well-structured code, solid architectural patterns… stable and scalable as it grows". Đây là đất của SA.

### 3.1 Clean architecture / layering
- **Presentation** (Controller, Razor, API) → **Application** (use case, handler, validation, transaction, gọi port) → **Domain** (entity, value object, luật nghiệp vụ, domain event) ← **Infrastructure** (EF, S3, email, payment, HTTP client). Domain **không** phụ thuộc Infrastructure: interface do tầng nghiệp vụ định nghĩa (`IDocumentStorage`, `ITaxCalculator`), hạ tầng implement (**Dependency Inversion**).
- Controller mỏng: nhận request → gọi handler → map kết quả ra HTTP. Không để logic tính giá trong controller hay Razor view.
- **Vertical slice**: tổ chức theo feature (`Quotes/Finalize`, `Orders/Cancel`) thay vì theo tầng kỹ thuật; mỗi slice có handler, validator, DTO. Không giáo điều: handler được dùng `DbContext` trực tiếp.
- Ví dụ thật: Joblogic Web MVC → message → `IHandler<TMsg, OneOf<TRes, Error>>` → service → EF/Dapper. PlaySweeps: repository bọc stored procedure Dapper, DI bằng Autofac.
- **DTO vs domain model vs persistence model**: DTO là hợp đồng API (ổn định, chỉ field cần), domain model chứa luật, persistence model là cách lưu. Với EF thường gộp domain + persistence, nhưng **không trả entity ra API** (lộ dữ liệu, over-posting, khoá schema, vòng tham chiếu, lazy N+1).

### 3.2 SOLID — một câu mỗi chữ + ví dụ Ops Hub
- **S** (Single Responsibility): `QuotePricingService` chỉ tính giá; `QuotePdfRenderer` chỉ render. Lý do thay đổi khác nhau → class khác nhau.
- **O** (Open/Closed): thêm RTO provider/loại thuế mới bằng class mới implement interface, không sửa `if/else` lớn.
- **L** (Liskov): mọi `IPaymentProvider` trả kết quả cùng ngữ nghĩa; không có provider nào throw `NotSupportedException` cho một method trong interface.
- **I** (Interface Segregation): tách `IQuoteReader` / `IQuoteWriter` thay vì repository khổng lồ 40 method.
- **D** (Dependency Inversion): handler phụ thuộc `TimeProvider`, `ITaxCalculator`, `IDocumentStorage`; không `DateTime.Now`, không `new AmazonS3Client()` → **testable**.

### 3.3 Monolith vs microservices
| | Modular monolith | Microservices |
|---|---|---|
| Transaction | Đơn giản (1 DB) | Phân tán: outbox, saga, eventual consistency |
| Deploy | Một artifact | Độc lập từng service |
| Vận hành | Dễ | Cần observability, service discovery, versioning contract |
| Hợp khi | Team nhỏ–vừa, domain còn thay đổi | Nhiều team, scale khác nhau, ranh giới domain rõ |
Câu mẫu:
> For a system like the Ops Hub I'd start with a well-structured modular monolith rather than microservices: clear modules for Quotes, Orders, Contracts, Production and Delivery, each with its own application layer, and communication through interfaces or in-process events. That keeps transactions simple, which matters when money and contracts are involved. To keep it scalable I'd keep the web tier stateless so it can scale horizontally behind a load balancer, push slow work like PDF generation, emails and third-party sync to background workers through a queue, add read replicas or caching for heavy reports, and watch the database with proper indexes and query monitoring. I'd only split a module into a separate service when there's a real reason, like a different scaling profile or a separate team.
Câu đối chiếu kinh nghiệm: Joblogic có ~30 service (team lớn, sản phẩm lâu năm) — Hiệp đã thấy cả lợi (deploy độc lập, scale theo trigger) lẫn chi phí (contract NuGet chung, message trùng phải idempotent, debug xuyên service cần OperationId).

### 3.4 Scale & sẵn sàng (stable and scalable)
- **Horizontal vs vertical**: vertical = máy to hơn (giới hạn, downtime); horizontal = nhiều instance (cần stateless: session/cache ra Redis, file ra S3).
- **Stateless web tier** + load balancer + health check; **background worker** cho việc chậm; **queue** để san tải; **cache** cho dữ liệu đọc nhiều; **read replica** cho báo cáo; **index + query tuning** trước khi nghĩ shard.
- **Một instance chết**: ≥ 2 instance ở 2 AZ, health check gỡ instance lỗi, graceful shutdown (dừng nhận request, xử lý xong việc dở), job nền idempotent để instance khác chạy lại được.
- **Zero-downtime deploy**: rolling/blue-green + migration expand/contract (section 15, 20).
- **Scalability vs performance vs availability vs reliability**: scalability = chịu tải tăng khi thêm tài nguyên; performance = nhanh với tải hiện tại; availability = % thời gian phục vụ được; reliability = làm đúng, không mất dữ liệu.
- **Eventual consistency**: các bản sao/hệ thống sẽ khớp sau một khoảng thời gian. Ví dụ: read model search, báo cáo, số liệu dashboard. **Không** chấp nhận cho số dư/tiền đã thu.
- **CAP thực tế**: khi mạng phân vùng phải chọn trả lời (có thể sai/cũ) hay từ chối. Với tiền → ưu tiên đúng (consistency); với catalog/hiển thị → ưu tiên sẵn sàng.

### 3.5 Câu hỏi luyện (SA)
1. How would you structure a .NET solution for this product? Where does business logic live?
2. Explain SOLID with examples from your work.
3. Monolith or microservices for the Ops Hub? Why?
4. How do you make the system stable and scalable as it grows?
5. What's the difference between a DTO, a domain model and a persistence model? Should a controller return an EF entity?
6. What is dependency inversion and how does it make code testable?
7. How would you design the system so it survives one instance dying?
8. Where would this architecture break first if traffic grew 10×?
9. What's eventual consistency? Where is it acceptable in the Ops Hub and where isn't it?
10. How would you introduce a big architectural change (e.g. move PDF generation to a worker) into a running production system? → strangler, feature flag, chạy song song, đo, chuyển dần, có đường quay lại.
11. Describe an architecture you'd be comfortable owning in production.
12. When would you choose vertical slices over classic layers?

---

## 4. REST API design — Khả năng: Rất cao (85%)

Giao điểm lớn nhất giữa SA (skill REST tự khai) và vị trí C#. Đã học Buổi 2 (`notes/02`).

### 4.1 Kiến thức cốt lõi
- **Resource** là danh từ số nhiều: `GET /quotes`, `GET /quotes/{id}`, `POST /quotes`, `PATCH /quotes/{id}`. Hành động nghiệp vụ không phải CRUD → **action endpoint**: `POST /quotes/{id}/finalize`, `POST /orders/{id}/cancel` (chấp nhận được, nói rõ vì sao: chuyển trạng thái có luật, không phải sửa field).
- **Verb**: GET (safe + idempotent), PUT (thay toàn bộ, idempotent), PATCH (sửa một phần, không idempotent theo định nghĩa), DELETE (idempotent, không safe), POST (không idempotent).
- **Status code**:
  - 200 OK, **201 Created + header `Location`**, 202 Accepted (việc chạy nền), 204 No Content.
  - 400 validation, **401** chưa xác thực vs **403** không có quyền, 404, **409 Conflict** (trạng thái không cho phép / trùng), **412 Precondition Failed** (ETag lệch), 422 vi phạm luật nghiệp vụ (tuỳ team), 429 Too Many Requests, 500, 503 + `Retry-After`.
- **Lỗi** theo **ProblemDetails (RFC 9457)**: `type, title, status, detail, instance` + `errorCode` ổn định + `traceId`; validation trả `errors` theo field để React map vào form. 500 không lộ stack/`ex.Message`.
- **Idempotency**: POST tạo tiền/đơn → header `Idempotency-Key` (client sinh UUID). Server lưu (key, user, hash body, response) với **UNIQUE**; trùng key + cùng body → **replay response**; trùng key + khác body → 422; đang xử lý → 409. Giữ ~24h.
- **Concurrency**: response có `ETag` (từ `rowversion`), client gửi `If-Match` khi sửa → 412 nếu đã bị người khác sửa.
- **Pagination**: offset cho admin cần nhảy trang (chậm dần khi sâu, có thể trùng/sót khi chèn); **keyset/cursor** cho danh sách lớn: `WHERE (CreatedAt, Id) < (@c, @id) ORDER BY CreatedAt DESC, Id DESC`, cursor opaque, index khớp, sort xác định (có Id làm tie-breaker). Tránh `COUNT(*)` mỗi trang trên bảng lớn.
- **Filtering/sorting**: `GET /orders?status=InProduction&storeId=12&sort=-createdAt`; whitelist field được sort.
- **Versioning**: URL `/v1` (dễ nhìn, dễ route) hoặc header. Ưu tiên thay đổi **additive**. Breaking: xoá/đổi tên field, đổi kiểu, thêm field bắt buộc ở request, đổi ý nghĩa/status/enum. Client là **tolerant reader**. Deprecation: header `Deprecation`/`Sunset`, đo traffic theo version, báo trước. Package `Asp.Versioning`.
- **Hợp đồng FE–BE**: **OpenAPI** (Swashbuckle/NSwag) → sinh TypeScript types/client (EIM có Swagger). Contract test nếu nhiều client.
- **Việc chậm** (sinh PDF, gọi RTO provider): `202 Accepted` + `Location: /jobs/{id}`, client poll hoặc nhận push (SignalR/WebSocket).
- **Bảo mật API**: HTTPS, auth (JWT bearer hoặc cookie), authorization theo resource (kiểm tra quyền sở hữu, không chỉ đăng nhập), rate limit, validate input, không lộ ID tuần tự nếu nhạy cảm.
- **HATEOAS**: biết khái niệm (link trong response), thực tế ít dùng.

### 4.2 Câu mẫu
> For the Ops Hub I'd keep the API resource-oriented, with explicit action endpoints for business transitions like finalizing a quote, because those aren't just field updates. Errors follow ProblemDetails so the React side can map validation errors to fields. Anything that moves money or creates an order accepts an idempotency key, and edits use ETags so two staff members can't silently overwrite each other. The OpenAPI spec is the contract, and we generate TypeScript types from it so frontend and backend can't drift.

### 4.3 Câu hỏi luyện
1. Design the API for finalizing a quote and converting it to a sales order. Endpoints, status codes, error responses?
2. How do you design a REST endpoint that creates a resource? (201 + Location + body, 400 ProblemDetails, 409)
3. What does idempotent mean? Which HTTP methods are idempotent? Is idempotent the same as safe?
4. The user double-clicks "Create order" — what does the API do? (Idempotency-Key + UNIQUE + replay; UI disable nút; MVC thì PRG)
5. Two staff edit the same order at once — what does the API do and what does the user see? (ETag/If-Match → 412 → UI tải bản mới để so sánh)
6. 401 vs 403? 400 vs 422? 409 vs 412?
7. How do you version an API used by an external mobile app? What counts as a breaking change?
8. Offset vs cursor pagination — when each? Why does offset get slow?
9. PUT vs PATCH?
10. How do you keep TypeScript types in sync with C# DTOs?
11. How do you return errors consistently across the API?
12. An operation takes 10 seconds — how do you design the API?
13. How would you design filtering and sorting on the orders list safely?
14. How do you protect a public API from abuse? (rate limit theo user/IP/key, Redis sliding window/token bucket, 429 + Retry-After, exponential backoff cho login như PlaySweeps)
15. Should business actions be `PATCH /orders/{id} {status: "Cancelled"}` or `POST /orders/{id}/cancel`? Trade-off?

---

## 5. Clean code + code review — Khả năng: Rất cao (80%)

SA tự khai "Clean Coding". Có thể được đưa một đoạn code để review trực tiếp.

### 5.1 Clean code — nói được bằng ví dụ
- **Đặt tên** theo nghiệp vụ (`CalculateBalanceDue`, `IsEligibleForRto`), không `Process`, `Helper`, `data2`.
- **Hàm nhỏ, một việc**, ít tham số (gom thành object), không flag bool đổi hành vi (`Save(true)`).
- **Guard clause / early return** thay vì if lồng nhau.
- **Không magic number/string**: hằng số, enum, cấu hình.
- **Không lặp logic** (DRY), nhưng đừng gộp hai thứ chỉ giống nhau bề ngoài (AHA / "rule of three").
- **Bất biến** khi có thể: `record`, `init`, value object `Money`.
- **Xử lý lỗi rõ**: Result cho lỗi nghiệp vụ, exception cho bất ngờ; không `catch {}` nuốt lỗi; log có ngữ cảnh.
- **Comment giải thích "vì sao"**, không giải thích "làm gì".
- **Testable**: DI, không static/`DateTime.Now`, logic thuần ở domain.
- **Boy Scout rule / "1% improvements"**: mỗi lần chạm vào code thì để lại tốt hơn một chút (khớp văn hoá JD).

### 5.2 Checklist review PR (thứ tự nói)
1. **Đúng nghiệp vụ**: có làm đúng acceptance criteria, edge case (tiền, thời gian, null, rỗng, trùng)?
2. **Test**: có test cho luật mới và bug đã sửa không?
3. **Thiết kế**: đúng tầng, không lộ entity, không logic trong controller, đặt tên.
4. **Dữ liệu**: transaction boundary, concurrency, migration tương thích ngược, index cho query mới, N+1.
5. **Bảo mật**: authorization theo resource, validate input, không log dữ liệu nhạy cảm, SQL parameter.
6. **Vận hành**: log/metric, timeout/retry khi gọi ngoài, feature flag, rollback được.
7. **Hiệu năng**: async all the way, không `.Result`, phân trang.
Thái độ: comment cụ thể, đề xuất thay vì ra lệnh, tách "blocking" và "nit", khen chỗ tốt. PlaySweeps: lead feature nào review kỹ feature đó; Joblogic: review với team UK trên Azure DevOps.

### 5.3 Bài review code (từ question bank 133–136) — tập nói to
**133.**
```csharp
public async Task<User> GetUser(int id)
{
    var user = await _db.Users.FirstOrDefaultAsync(x => x.Id == id);
    return user;
}
```
Ý: trả `null` khi không có → controller trả **404**; không trả entity ra API → **project sang DTO** (`Select(u => new UserDto(...))`) — chỉ lấy cột cần, không tracking; nếu chỉ đọc mà không project thì `AsNoTracking()`; truyền `CancellationToken`; kiểm tra quyền xem user này (multi-tenant/ownership); đổi tên `GetUserAsync`; kiểu trả về `User?` (nullable reference).

**134.**
```csharp
public async Task ProcessAsync()
{
    var result = _client.GetAsync("/users").Result;
    Console.WriteLine(result);
}
```
Ý: `.Result` là **sync-over-async** → chiếm 2 thread, có thể **thread-pool starvation** (ASP.NET Core) hoặc deadlock (có SynchronizationContext); method `async` mà không `await`. Sửa: `await _client.GetAsync("/users", ct)`, `EnsureSuccessStatusCode`, `ReadFromJsonAsync`, timeout bằng CancellationToken/`HttpClient.Timeout`, retry có backoff (Polly/resilience handler), log bằng `ILogger` không `Console`. `HttpClient` **không tạo mới mỗi request** (cạn socket) → `IHttpClientFactory`/typed client (cũng xử lý DNS đổi).

**135.**
```csharp
public class OrderService
{
    private readonly DbContext _db;
    public OrderService(DbContext db) { _db = db; }
    public async Task CreateAsync(Order order)
    {
        _db.Add(order);
        await _db.SaveChangesAsync();
    }
}
```
Hỏi trước khi approve: validation và luật nghiệp vụ ở đâu (order nhận từ đâu, có phải entity bind thẳng từ request → over-posting)? Có idempotency chống tạo trùng? Transaction boundary: `SaveChanges` đã là 1 transaction; nếu cần gửi email/gọi ngoài → outbox, không gọi trong transaction. Dùng `DbContext` chung chung → nên inject `AppDbContext` cụ thể. Có cần repository không? Với EF thường **không** (DbSet đã là repository, DbContext là UoW); bọc khi Dapper/nhiều store. Thiếu `CancellationToken`, thiếu trả về id/kết quả, thiếu log/audit. Lớp này đang "anemic": logic nên ở `Order.Create(...)` hoặc handler.

**136.**
```csharp
public class CacheService
{
    private readonly Dictionary<string, object> _cache = new();
    public object Get(string key) => _cache.TryGetValue(key, out var v) ? v : null;
    public void Set(string key, object value) => _cache[key] = value;
}
```
Ý: `Dictionary` **không thread-safe** → đọc/ghi đồng thời có thể hỏng cấu trúc, vòng lặp vô hạn, exception. Không có expiration → dữ liệu cũ + **memory leak** (lớn mãi). Nhiều instance → mỗi instance một cache riêng, lệch nhau. `object` → mất type safety. Không giới hạn kích thước. Sửa: `IMemoryCache` (có expiration, size limit, thread-safe) cho cache cục bộ; **Redis/`IDistributedCache`** (hoặc `HybridCache` .NET 9) khi nhiều instance cần thống nhất; key có tenant; chống stampede (lock theo key / `GetOrCreateAsync`).

**Bài thêm (tự luyện, liên quan nghiệp vụ):**
```csharp
public decimal CalculateBalance(Order o)
{
    double total = 0;
    foreach (var l in o.Lines) total += (double)(l.Price * l.Qty);
    total = total * 1.07;                 // tax
    var paid = _db.Payments.Where(p => p.OrderId == o.Id).ToList().Sum(p => p.Amount);
    return (decimal)Math.Round(total - (double)paid, 2);
}
```
Lỗi cần tìm: `double` cho tiền (sai số) → `decimal`; thuế **hard-code 7%** (thuế phụ thuộc địa chỉ/bang, phải lấy từ snapshot của order); `ToList()` trước `Sum` → kéo hết về RAM (dùng `SumAsync` ở DB); query sync trong code lẽ ra async; không trừ refund; làm tròn mặc định là **banker's rounding** (`MidpointRounding.ToEven`) — cần quy tắc rõ; logic tính tiền nằm trong service truy cập DB trực tiếp → khó test, nên tách hàm thuần nhận dữ liệu.

### 5.4 Câu hỏi luyện
1. What does clean code mean to you? Give an example of code you cleaned up.
2. What do you look for when reviewing a pull request?
3. How do you give feedback on a PR from a more senior colleague / from the US partner?
4. How do you handle disagreement in code review?
5. Review this code (các bài trên). What would you change and why?
6. When is duplication better than the wrong abstraction?
7. How do you keep a codebase maintainable over years?
8. What makes code testable?

---

## 6. Design patterns — Khả năng: Cao (80%) — LỖ HỔNG LỚN NHẤT

Nguyên tắc: **vấn đề → pattern → ví dụ thật/Ops Hub → trade-off**. Đừng đọc định nghĩa sách.

### 6.1 Bảng pattern
| Pattern | Khi nào | Ví dụ để kể | Trade-off |
|---|---|---|---|
| **Strategy** | Nhiều thuật toán đổi được theo cấu hình | Tính giá theo loại sản phẩm; RTO provider khác nhau tính lịch trả khác nhau; Joblogic selling rate theo khung giờ/holiday | Thêm class; đáng khi có ≥ 2 biến thể thật |
| **State / state machine** | Thực thể có vòng đời, mỗi trạng thái cho phép hành động khác | Quote: Draft → Sent → Accepted/Expired; Order: Confirmed → InProduction → Ready → Scheduled → Delivered / Cancelled | Đơn giản thì enum + bảng chuyển trạng thái là đủ; State class cho khi mỗi trạng thái có nhiều hành vi |
| **Factory / Abstract Factory** | Tạo object phức tạp, chọn implementation lúc chạy | `IRtoProviderFactory.Get(companyId)`; DocGen chọn template tenant → fallback hệ thống | — |
| **Builder** | Tạo object nhiều bước/tham số | Dựng quote/test data (test data builder), `WebApplication.CreateBuilder` | — |
| **Template Method** | Các bước giống nhau, chi tiết khác | Sinh tài liệu: lấy data → chọn template → thay tag → xuất PDF | Kế thừa → cứng; có thể thay bằng composition |
| **Decorator** | Thêm hành vi ngang (log, cache, retry) không sửa class gốc | `CachedTaxRateProvider` bọc `TaxApiClient`; MediatR pipeline behavior (validation, logging); `DelegatingHandler` của HttpClient | Debug nhiều lớp bọc |
| **Adapter / Anti-corruption layer** | Tích hợp hệ ngoài có model khác | Map SKU từ configurator, payment, thuế → model nội bộ; đổi provider chỉ sửa adapter | — |
| **Facade** | Che một hệ phức tạp sau API gọn | `IKycService` che Socure (DocV, SSN, decision) | — |
| **Repository + Unit of Work** | Tách data access; UoW = 1 transaction | `DbContext` đã là UoW + repository; PlaySweeps bọc SP Dapper bằng repository | Generic `IRepository<T>` trên EF thường thừa, che mất sức mạnh LINQ |
| **Specification** | Điều kiện nghiệp vụ tái sử dụng/ghép | "RTO option eligible": giá trị tối thiểu, bang, loại sản phẩm | — |
| **Mediator / CQRS** | Tách command/query, pipeline chung | Joblogic message + handler; Replication sang Azure Search = read model | Mediator là **in-process**, không liên quan độ bền message |
| **Observer / domain event** | Một sự kiện kéo theo nhiều việc | OrderDelivered → SMS/email, cập nhật balance, audit. Joblogic: Notification/Audit subscribe event | Luồng khó lần theo; cần đặt tên event rõ |
| **Outbox** | Ghi DB + gửi message nhất quán | Ghi order + outbox row **cùng transaction**, worker gửi sau | Thêm bảng + worker; consumer phải idempotent |
| **Result type** | Lỗi nghiệp vụ là kết quả bình thường | Joblogic `OneOf<TSuccess, Error>` | Code dài hơn try/catch |
| **Singleton** | Một instance cho cả app | Qua DI (`AddSingleton`), không tự viết static; cẩn thận captive dependency | Static singleton khó test |
| **Options pattern** | Cấu hình có kiểu | `IOptions<TaxSettings>` | — |
| **Circuit breaker / Retry** | Gọi hệ ngoài không ổn định | Polly / `Microsoft.Extensions.Http.Resilience` | Retry không idempotent = nguy hiểm |

### 6.2 Câu mẫu (State)
> An order has a clear lifecycle, so I'd model it as a state machine in the domain: the Order entity exposes methods like `Confirm()`, `StartProduction()`, `ScheduleDelivery(date)`, `Cancel(reason)`, and each one checks the current status and the business rules before changing it. The UI only shows the actions that are allowed, but the rule lives in the domain, so an API call or a background job can't put the order in an invalid state. Every transition writes an audit entry with who, when and why — similar to the contract audit trail I built at Joblogic.

Code minh hoạ:
```csharp
public sealed class Order
{
    public OrderStatus Status { get; private set; }
    private readonly List<OrderEvent> _history = new();

    public Result Cancel(string reason, string userId, DateTimeOffset now)
    {
        if (Status is OrderStatus.Delivered or OrderStatus.Cancelled)
            return Result.Fail("order.cannot_cancel");
        Status = OrderStatus.Cancelled;
        _history.Add(new OrderEvent("Cancelled", reason, userId, now));
        return Result.Ok();
    }
}
```

### 6.3 Câu mẫu (Strategy cho RTO)
> Different rent-to-own providers have different rules for eligibility, terms and payment schedules. I'd define an `IRtoProvider` interface with methods like `CheckEligibility` and `BuildPaymentSchedule`, one implementation per provider, and pick it through a factory based on the company's configuration. Adding a provider then means adding a class and a configuration entry, not editing a large switch statement.

### 6.4 Câu bẫy
- "When would you NOT use a pattern?" > When there's only one way of doing it and no sign it will change. A pattern adds indirection, so I add it when the second case actually appears, not up front.
- "Is Repository over EF Core an anti-pattern?" > With EF Core I usually don't add a generic repository — DbSet already is one and DbContext is a unit of work. I add a specific repository when there's a reason: Dapper and stored procedures, multiple stores, or translating unique-key violations into domain results.
- "Singleton pattern vs singleton lifetime?" → pattern tự quản lý instance (static, khó test); lifetime do DI container quản lý.

### 6.5 Câu hỏi luyện
1. Which design patterns do you use most? Give a real example for each.
2. How would you model the order lifecycle? Which pattern?
3. How would you support several RTO providers with different rules?
4. How would you add caching to a tax-rate client without modifying it? (Decorator)
5. How do you integrate a third-party system whose model doesn't match yours? (Adapter/ACL)
6. Explain CQRS. Is it worth it here?
7. Explain the Outbox pattern. How is it different from a mediator?
8. Repository + Unit of Work with EF Core: yes or no?
9. When does a pattern become over-engineering?
10. Strategy vs State — difference?
11. Factory vs DI container — when do you need a factory?

---

## 7. Refactoring + tiếp quản code từ đối tác Mỹ — Khả năng: Cao (80%)

JD ghi thẳng "taking over from a US partner". Gần như chắc chắn có câu "2 tuần đầu".

### 7.1 Code smell hay gặp & cách sửa
| Smell | Refactoring |
|---|---|
| Method dài, controller béo | Extract Method / Extract Class → service/handler |
| `switch` theo loại lặp ở nhiều nơi | Replace Conditional with Polymorphism (Strategy) |
| Primitive obsession (`decimal price`, `string status`) | Value object `Money(amount, currency)`, enum/state |
| Logic tính tiền lặp ở UI, PDF, API | Gom về 1 domain service; PDF đọc kết quả đã tính |
| `DateTime.Now` khắp nơi | Inject `TimeProvider` (.NET 8) |
| God class / static helper | Tách theo use case, DI |
| Feature envy (method dùng dữ liệu của class khác nhiều hơn của mình) | Move Method |
| Shotgun surgery (một thay đổi phải sửa nhiều nơi) | Gom trách nhiệm |
| Comment giải thích code rối | Đổi tên, tách hàm |
| Dead code, code bị comment | Xoá (git giữ lịch sử) |
| `ToList()` sớm, N+1, query trong vòng lặp | Projection, Include, batch |
| `catch (Exception) {}` | Xử lý cụ thể + log |

### 7.2 Cách refactor an toàn (nói theo thứ tự)
1. **Characterization test** (golden master): test chụp lại hành vi hiện tại (kể cả "lạ") trước khi sửa. Ví dụ: chạy 200 quote mẫu, lưu kết quả tổng tiền, so sánh sau refactor.
2. **Bước nhỏ**, mỗi commit một thay đổi, chạy test sau mỗi bước; **tách PR refactor và PR đổi hành vi**.
3. Tạo **seam**: interface quanh phụ thuộc khó test (DB, thời gian, API ngoài) để chèn test double.
4. **Strangler fig**: phần mới viết cạnh phần cũ, chuyển dần route/feature, **feature flag** để quay lại.
5. **Branch by abstraction**: đưa interface vào trước, hai implementation song song, chuyển dần.
6. Đo trước/sau nếu refactor vì performance.
7. **Không big-bang rewrite** (rủi ro cao, mất tri thức nghiệp vụ ẩn trong code cũ).

### 7.3 "2 tuần đầu khi tiếp quản" — câu mẫu
> In the first two weeks I'd focus on understanding before changing. First, get the system running locally and through the deployment pipeline, and get access to logs and monitoring. Second, map the main business flows end to end — quote, order, contract, production, delivery — with the PM, and draw a simple architecture and data diagram. Third, ask the US partner for a knowledge-transfer session with a prepared list of questions: known bugs, risky areas, why certain decisions were made, how deployments and secrets are managed. Fourth, pick up a few small bugs so I learn the code by working in it. And I'd write down what I find as living documentation. I won't start a big rewrite; improvements go in small steps backed by tests. I did something similar at PlaySweeps when I took over the Socure KYC integration from a colleague: I studied the vendor dashboard and decision module, found that the initial prototype had wrong assumptions, and reworked it until it ran stably in production.

Danh sách câu hỏi chuẩn bị cho buổi bàn giao với partner Mỹ:
- Kiến trúc, môi trường (dev/staging/prod), cách deploy, ai giữ secret/tài khoản cloud.
- Known bugs, vùng rủi ro, phần "đừng đụng vào".
- Test hiện có, coverage, test chạy ở đâu.
- Tích hợp bên thứ ba: tài khoản, webhook, giới hạn, liên hệ.
- Job nền, cron, cách vận hành khi lỗi; runbook sự cố.
- Quyết định kiến trúc quan trọng và lý do (ADR nếu có).
- Dữ liệu: schema, migration, backup/restore, dữ liệu nhạy cảm.
- Khi nào họ còn hỗ trợ, kênh liên lạc, chênh múi giờ.

Khi tiếp quản legacy, kiểm tra kỹ thuật đầu tiên: FK có index không, `ToList()` sớm/client evaluation (EF ≤ 2), `.Result`/`.Wait()`, `DateTime.Now`, `double` cho tiền, secret trong code/config, log, test.

### 7.4 "Bug gấp trên production, code chưa có test"
> First I'd reproduce it and limit the impact — for example a feature flag or a data fix if customers are blocked. Then I'd write a test that reproduces the bug, even a narrow one, make the smallest fix that passes it, and get a review. After the hotfix, I'd add a follow-up ticket to cover that area properly and look for the root cause, not only the symptom.

### 7.5 "Code của partner chất lượng kém, bạn làm gì?"
> I'd avoid judging it before I understand the constraints they had. I'd list the problems by business risk — for example money calculations without tests come first, naming issues last — agree the priorities with the PM, and improve the risky areas in small steps alongside feature work, rather than asking for a separate rewrite project.

### 7.6 Câu hỏi luyện
1. You inherit a codebase from a US partner with no tests. What do you do in the first two weeks?
2. How do you refactor a 400-line controller action safely?
3. What's a characterization test?
4. Explain the strangler fig pattern. When would you use it here?
5. Production bug, no tests, customers blocked. Walk me through it.
6. How do you convince the PM to spend time on refactoring? (gắn với rủi ro/tốc độ giao feature, làm kèm feature, đo bằng số bug/thời gian)
7. The previous team made a design decision you disagree with. What do you do?
8. How do you document a system you're learning?
9. What code smells do you look for first?
10. Rewrite or refactor? When is a rewrite justified?

---

## 8. Nghiệp vụ Ops Hub — Khả năng: Rất cao với PO (85%), Cao với SA (60%)

Chỉ dùng phạm vi **công khai trong JD**. Nói dạng "I'd assume… and I'd confirm with the PM". SA có nền Urbanise (SaaS vận hành: tiền định kỳ, workflow bảo trì, tài liệu, đối soát ngân hàng) → rất có thể hỏi tiền, workflow, tài liệu.

### 8.1 Thuật ngữ
| Từ | Nghĩa |
|---|---|
| Shed / carport | Nhà kho / mái che xe đúc sẵn, bán qua đại lý (dealer/store) ở Bắc Mỹ |
| Quote | Báo giá: sản phẩm, kích thước, option, giá, thuế, phí giao, hết hạn |
| Finalize / lock quote | Khoá báo giá: giá và nội dung không đổi nữa (snapshot) |
| Sales order | Đơn hàng sau khi khách chấp nhận |
| Cash sale | Mua trả thẳng (có thể trả deposit trước, phần còn lại khi giao) |
| **RTO (rent-to-own)** | Thuê-mua: khách trả góp hằng tháng, đủ kỳ thì sở hữu; thường qua công ty RTO bên thứ ba duyệt (eligibility, credit check) |
| Deposit / down payment | Tiền đặt cọc |
| **Balance due** | Số còn phải trả |
| Production queue / build list | Hàng đợi sản xuất, thứ tự đóng |
| Delivery scheduling | Lên lịch giao: ngày, tài xế/xe, tuyến, cửa sổ thời gian |
| Driver app | App tài xế: lịch, xác nhận giao, ảnh, chữ ký, thu tiền |
| Inventory | Hàng có sẵn (đã đóng) để bán ngay |
| Markup vs margin | Markup = lợi nhuận / giá vốn; margin = lợi nhuận / giá bán. Giá vốn 100, bán 125 → markup 25%, margin 20% |
| Sales tax (Mỹ) | Theo bang/quận/thành phố, theo địa chỉ giao; Canada: GST/PST/HST |
| Audit trail / history notes | Ai làm gì, lúc nào, trước/sau |

### 8.2 Luồng chính và dữ liệu
Quote (sản phẩm, option, giá, thuế, hết hạn) → **Finalize/Accept** (khoá giá, snapshot) → Sales Order (cash sale hoặc **RTO**) → Contract (template, chữ ký) → Production (queue, trạng thái) → Delivery (lịch, tài xế, xác nhận, ảnh, thu tiền còn lại) → Closed.
Mô hình dữ liệu gợi ý:
- `Company` (tenant) → `Store`/`Region` → `User` (role).
- `Customer`, `Product`/`Option`/`PriceList` (master data, 3NF).
- `Quote` + `QuoteLine` (**snapshot** ProductName, UnitPrice, TaxRate, phí) + `QuoteRevision`.
- `Order` (status, loại: Cash/RTO) + `OrderLine` (copy từ quote đã finalize).
- `Payment` / ledger (`OrderTransaction`: Deposit, Payment, Refund, Adjustment) → balance due tính từ ledger.
- `Contract` (template id + version, file PDF đã sinh, trạng thái ký, dữ liệu snapshot).
- `ProductionJob` (queue, vị trí, trạng thái), `Delivery` (ngày lịch + timezone, tài xế, xác nhận, ảnh).
- `AuditEntry` (entity, field, old/new, user, thời điểm UTC).

### 8.3 Tiền
- **`decimal`**, không `double`/`float` (0.1 + 0.2 ≠ 0.3 với double). DB: `DECIMAL(18,2)` (hoặc 19,4 cho đơn giá), EF `HasPrecision(18,2)`.
- **Làm tròn một chỗ**, quy tắc rõ: `Math.Round(x, 2, MidpointRounding.AwayFromZero)` (mặc định C# là **ToEven/banker's**). Làm tròn theo dòng hay theo tổng → **hỏi PO/kế toán**, khác nhau vài cent.
- **Snapshot** giá/thuế trên quote/order khi finalize; đổi bảng giá không ảnh hưởng quote đã gửi.
- **Balance due = total (gồm thuế, phí) − tổng payment đã ghi nhận + refund đã trả lại (nếu tính ngược) ± adjustment**. Tính từ **ledger chỉ ghi thêm** (append-only), không lưu một con số rồi cộng trừ tay → tránh lệch. Nếu cần lưu số dư để query nhanh: cập nhật trong **cùng transaction** với ledger + job đối soát.
- **Trả góp (RTO)**: chia kỳ làm tròn, **kỳ cuối bù chênh lệch**; unit test: tổng các kỳ = tổng hợp đồng. Lịch trả có thể do công ty RTO tính → hỏi PO ai là nguồn sự thật.
- **Thuế** theo địa chỉ giao (không phải địa chỉ cửa hàng), có thể lấy từ API thuế bên thứ ba → cache + snapshot mức thuế vào order; khách miễn thuế (tax-exempt).
- **Thanh toán qua provider** (Stripe hoặc tương tự): webhook → xác thực chữ ký → **idempotent theo event id** → cập nhật ledger. Không tin số tiền từ client.
- **Refund / huỷ**: bút toán ngược trong ledger, không xoá payment.
- **Value object** `Money(Amount, Currency)`: cộng trừ chỉ khi cùng currency, làm tròn tập trung.

Câu mẫu:
> I'd never store the balance as a number that we add to and subtract from in different places. Payments, refunds and adjustments go into an append-only ledger, and the balance due is the order total — locked when the quote was finalized, including tax — minus the net of that ledger. Money is `decimal`, rounding happens in one place with an explicit rule, and payment webhooks are applied idempotently by event ID. That way, if a number looks wrong, we can explain every cent.

### 8.4 Thời gian / múi giờ / DST
- Lưu **instant** (đã xảy ra: created, paid, delivered-at) bằng UTC (`DateTimeOffset`/`datetime2` UTC).
- **Ngày giao dự kiến là ngày lịch**, không phải instant → `DateOnly`/SQL `date` + timezone của cửa hàng/khách (IANA, vd. `America/Chicago`). Không lưu "nửa đêm UTC".
- Bắc Mỹ: nhiều múi giờ (ET, CT, MT, PT, Alaska, Hawaii; Arizona **không** DST) + DST (2026: bắt đầu **08/03**, kết thúc **01/11**). Tính "+N ngày" theo lịch địa phương (`TimeZoneInfo` hoặc NodaTime), không cộng 24h × N.
- Bug kinh điển: lưu `2026-11-02 00:00` giờ địa phương thành UTC rồi hiển thị ở múi giờ khác → lệch 1 ngày; cộng 24h qua ngày đổi giờ → lệch 1 giờ, có thể nhảy ngày.
- Hiển thị: server trả UTC (ISO 8601 có `Z`) cho instant, trả `yyyy-MM-dd` cho ngày lịch; frontend hiển thị theo timezone của **cửa hàng** (không phải trình duyệt) cho dữ liệu vận hành.
- Test: `TimeProvider` giả (`FakeTimeProvider`) với ngày DST, cuối tháng, năm nhuận, 23:30 ở Pacific (= hôm sau UTC).
- "Hết hạn quote sau 30 ngày" → 30 ngày lịch theo timezone cửa hàng, hết hạn lúc cuối ngày địa phương.

Câu mẫu:
> A delivery date is a calendar date, not an instant, so I'd store it as a date plus the store's time zone, and only convert to UTC for actual timestamps like "delivered at". Off-by-one-day bugs usually come from storing local midnight as UTC and then rendering it in another zone, or from adding 24 hours across a DST change.

### 8.5 Tài liệu PDF / hợp đồng / chữ ký
- Template theo công ty (tenant) → fallback template hệ thống; tag thay thế (Joblogic `@@Tag@@`).
- Tài liệu **đã ký/đã phát hành phải bất biến**: lưu file PDF đã sinh + **phiên bản template** + **snapshot dữ liệu** + hash file. Đổi template chỉ ảnh hưởng tài liệu mới.
- Sinh PDF ở **background worker** nếu chậm (202 + trạng thái); cache theo checksum dữ liệu (Joblogic DocGen); file lưu **S3**, tải bằng **presigned URL** ngắn hạn sau khi kiểm tra quyền.
- **Escape** ký tự đặc biệt (`&`, `<`, ký tự Unicode, emoji) khi đưa dữ liệu vào template/HTML; font hỗ trợ ký tự; kiểm tra layout với dữ liệu dài (tên dài, nhiều dòng).
- Rich text (T&C) → **sanitize HTML** trước khi render (XSS).
- Thư viện .NET: QuestPDF, iText, Aspose, Playwright/Chromium HTML→PDF, DinkToPdf. Joblogic dùng Xceed DocX + Aspose.Words.
- E-signature: lưu ai ký, lúc nào, IP/thiết bị, hash tài liệu tại thời điểm ký; nhiều trang/nhiều bên ký.

Câu mẫu:
> Once a contract is signed, it's a legal record, so it must never be regenerated from current data. I'd store the generated PDF in S3 together with the template version and a snapshot of the data used, plus a hash. If the company updates its template, only new contracts use it. If a customer disputes a contract a year later, we show exactly the file they signed, and the audit trail shows who sent it and when it was signed.

### 8.6 Production & delivery

Bối cảnh: shed (nhà kho gỗ/kim loại) được **đóng theo đơn** ở xưởng rồi chở bằng xe chuyên dụng (xe kéo/xe "mule") tới sân nhà khách. Vòng đời sau khi order được xác nhận: **vào hàng đợi sản xuất → đóng → kiểm tra → lên lịch giao → giao + xác nhận → (thu nốt tiền)**. Mỗi bước có một nhóm người dùng khác: quản lý xưởng, thợ, điều phối giao hàng, tài xế, khách. Đây là phần "vận hành", PO rất hay hỏi tình huống ở đây. Chi tiết ShedPro thật mình chưa biết, nên khi trả lời hãy nói "I'd assume… and confirm with the PO".

Tóm tắt 5 ý:
- Production queue: thứ tự đóng có thể kéo-thả thủ công → lưu `Position` (số thực/khoảng trống hoặc rank) + optimistic concurrency khi hai người cùng sắp xếp.
- Trạng thái sản xuất cập nhật từ xưởng (có thể qua tablet) → audit.
- Delivery: ràng buộc (xe chở tối đa N đơn/ngày, vùng giao, cửa sổ thời gian, điều kiện mặt bằng). Chống đặt quá → atomic UPDATE bộ đếm hoặc `UPDLOCK` trên dòng (xe, ngày) (`notes/03`).
- Driver app: có thể offline → dữ liệu trên máy là bản chụp; văn phòng đổi lịch → push + đồng bộ lại (giống RedeployRequired ở Joblogic); xác nhận giao + ảnh + chữ ký + thu tiền → idempotent khi app retry.
- Thông báo khách: SMS/email khi lên lịch, trước ngày giao, khi giao xong; tôn trọng opt-out; gửi qua queue, idempotent.

#### 8.6.1 Production queue: lưu thứ tự kéo-thả

**Vấn đề.** Quản lý xưởng kéo đơn A lên trên đơn B (gấp, khách VIP, thiếu vật tư thì đẩy xuống). Cần lưu thứ tự sao cho: (1) di chuyển 1 đơn không phải ghi lại cả 500 dòng, (2) hai người cùng sắp xếp không làm hỏng thứ tự.

**Ba cách lưu thứ tự** (đi từ đơn giản lên):

| Cách | Di chuyển 1 đơn | Nhược điểm |
|---|---|---|
| Số nguyên liên tiếp 1,2,3… | UPDATE mọi dòng giữa vị trí cũ và mới (O(n)) | Nhiều dòng bị khoá, dễ deadlock khi 2 người cùng kéo |
| Số có khoảng trống (1000, 2000, 3000) hoặc `decimal`: chèn vào giữa = trung bình hai bên | Ghi **1 dòng** | Sau nhiều lần chèn vào cùng một chỗ thì hết khoảng (1000 → 1500 → 1250…) → cần **rebalance** (đánh lại 1000, 2000…) |
| Rank dạng chuỗi (LexoRank kiểu Jira, "fractional indexing") | Ghi 1 dòng, sinh chuỗi nằm giữa hai chuỗi | Phức tạp hơn, cần thư viện; chỉ đáng khi danh sách rất dài và kéo liên tục |

Với xưởng shed (vài chục tới vài trăm đơn đang chờ mỗi xưởng), **số có khoảng trống + rebalance** là đủ. Nói được "I'd pick the simplest one that fits the size" là điểm Senior.

```csharp
public class ProductionJob
{
    public Guid Id { get; set; }
    public Guid PlantId { get; set; }          // mỗi xưởng một hàng đợi
    public Guid OrderId { get; set; }
    public decimal Position { get; set; }      // DECIMAL(20,10)
    public ProductionStatus Status { get; set; }
    public byte[] RowVersion { get; set; } = default!; // SQL Server rowversion
}

// Client gửi: "đặt job X nằm giữa beforeId và afterId" (không gửi số Position)
public async Task MoveAsync(Guid jobId, Guid? beforeId, Guid? afterId, byte[] rowVersion)
{
    var job = await _db.ProductionJobs.SingleAsync(j => j.Id == jobId);
    _db.Entry(job).Property(j => j.RowVersion).OriginalValue = rowVersion;

    decimal? prev = beforeId is null ? null :
        await _db.ProductionJobs.Where(j => j.Id == beforeId).Select(j => (decimal?)j.Position).SingleAsync();
    decimal? next = afterId is null ? null :
        await _db.ProductionJobs.Where(j => j.Id == afterId).Select(j => (decimal?)j.Position).SingleAsync();

    job.Position = (prev, next) switch
    {
        (null, null) => 1000m,
        (null, var n) => n!.Value - 1000m,      // lên đầu
        (var p, null) => p!.Value + 1000m,      // xuống cuối
        var (p, n) => (p!.Value + n!.Value) / 2 // chèn giữa
    };

    try { await _db.SaveChangesAsync(); }
    catch (DbUpdateConcurrencyException)
    {
        throw new ConflictException("Queue changed, please refresh"); // → HTTP 409
    }
    // nếu khoảng cách (next - prev) < 0.0001 → đẩy job nền rebalance cho PlantId này
}
```

Điểm cần nói:
- **Client gửi ý định ("đặt giữa A và B"), không gửi con số** → server tự tính, tránh client cũ ghi đè.
- **Optimistic concurrency** (`rowversion` / EF `IsRowVersion()`): người thứ hai lưu bản cũ → `DbUpdateConcurrencyException` → trả **409 Conflict**, UI tải lại hàng đợi. Chọn optimistic vì xung đột hiếm (vài người sắp xếp), không cần giữ khoá trong lúc người dùng kéo.
- Mức chặt hơn: concurrency theo **cả hàng đợi** (một cột `QueueVersion` trên bảng `Plant`, tăng mỗi lần sắp xếp), vì A kéo job 1 và B kéo job 2 cùng lúc có thể đều "thành công" nhưng kết quả không phải điều ai muốn. Hỏi PO mức nào đủ.
- Realtime: sau khi lưu, đẩy sự kiện qua **SignalR** tới các màn hình khác đang mở hàng đợi xưởng đó → giảm 409.
- Index `(PlantId, Status, Position)` để lấy hàng đợi theo thứ tự.

Câu mẫu:
> For a drag-and-drop production queue I'd store a sortable position with gaps, so moving one job means updating one row: the new position is the midpoint between its new neighbours, and a background job rebalances when the gaps get too small. The client sends "put job X between A and B", not a number. Each save checks a row version, so if two managers reorder at the same time, the second one gets a 409 and a refreshed queue instead of silently overwriting the first. I'd push the change over SignalR so other screens stay in sync. If the queue were thousands of items reordered constantly, I'd look at a string rank like Jira's LexoRank, but I'd start simple.

#### 8.6.2 Trạng thái sản xuất từ xưởng + audit

**Vấn đề.** Thợ/quản lý xưởng cập nhật trạng thái bằng tablet (thường dùng chung, đeo găng tay, wifi xưởng chập chờn): `Queued → InProgress → Built → QualityChecked → ReadyForDelivery` (có thể có `OnHold`, `Cancelled`). Văn phòng và khách cần biết đơn đang ở đâu; khi có tranh chấp ("ai đánh dấu xong khi chưa sơn?") cần truy vết.

**Thiết kế:**
- **State machine rõ ràng**, chuyển trạng thái chỉ qua method của entity, không cho set thẳng `Status`. Chuyển sai (Queued → Delivered) → lỗi 409/422.
- Mỗi lần chuyển ghi **audit**: ai, lúc nào (UTC), từ trạng thái nào sang trạng thái nào, ghi chú/ảnh, thiết bị nào. Với tablet dùng chung → đăng nhập nhanh bằng **PIN theo người** để audit có nghĩa (hỏi PO).
- Chuyển trạng thái phát **domain event** (`JobBuilt`) → bước tiếp (cho phép lên lịch giao, báo khách) chạy qua **outbox** để không mất sự kiện khi DB commit mà gửi message lỗi.
- Bấm 2 lần / wifi chập chờn retry → chuyển trạng thái phải **idempotent**: đã `Built` mà nhận lại "mark Built" → trả OK, không ghi audit lần 2.

```csharp
public void MarkBuilt(Guid userId, DateTimeOffset now, string? note)
{
    if (Status == ProductionStatus.Built) return;              // retry → không làm gì
    if (Status != ProductionStatus.InProgress)
        throw new InvalidTransitionException(Status, ProductionStatus.Built);

    var from = Status;
    Status = ProductionStatus.Built;
    BuiltAt = now;
    _history.Add(new ProductionStatusChange(Id, from, Status, userId, now, note));
    AddDomainEvent(new JobBuilt(Id, OrderId));                 // → outbox
}
```

Audit lưu ở đâu: bảng `ProductionStatusChange` (append-only) là đủ cho lịch sử trạng thái; audit chung mọi field có thể dùng EF `SaveChangesInterceptor` (Joblogic lưu audit ở MongoDB). Không cần event sourcing cả hệ thống, nói được lý do là điểm cộng.

Câu mẫu:
> I'd model production status as an explicit state machine, so the only way to change it is through methods like `MarkBuilt`, which reject invalid transitions. Every transition writes an append-only history row with who, when in UTC, from and to, and an optional note or photo. Shop-floor tablets are often shared, so I'd ask the PO whether staff sign in with a quick PIN; otherwise the audit says "tablet 3" and that's not very useful in a dispute. Transitions are idempotent, because flaky Wi-Fi means the same tap can arrive twice, and the "job built" event goes through an outbox so scheduling and customer notifications are never lost.

#### 8.6.3 Lên lịch giao: ràng buộc + chống đặt quá (overbooking)

**Ràng buộc thực tế** (hỏi PO cái nào cần ngay, cái nào để sau):
- **Năng lực**: xe/tài xế chở tối đa N chuyến/ngày (shed to, mỗi chuyến 1–2 cái), có thể theo **kích thước** (shed 12x24 cần xe/thiết bị riêng).
- **Vùng giao**: theo ZIP/khoảng cách từ xưởng; ngoài vùng tính thêm phí theo dặm.
- **Cửa sổ thời gian**: sáng/chiều; khách phải có mặt hay không.
- **Điều kiện mặt bằng** (site readiness): nền đã san phẳng, lối vào đủ rộng, không vướng dây điện/cây → checklist trước giao; không đạt → giao lại, có phí.
- **Thứ tự phụ thuộc**: chỉ lên lịch khi `ReadyForDelivery` (hoặc dự kiến xong trước ngày giao) và **đã trả đủ tiền / RTO đã duyệt** (hỏi PO).
- Ngày giao là **ngày lịch + timezone xưởng** (xem 8.4).

**Chống đặt quá: bản chất là race condition "check-then-act".** Hai điều phối viên cùng thấy xe A ngày 05/11 còn 1 chỗ (2/3), cùng bấm lưu → 4/3. Đọc `COUNT(*)` rồi mới INSERT là sai, kể cả trong transaction ở mức Read Committed (cả hai đều đọc được 2).

Cách 1: **atomic UPDATE bộ đếm** (đơn giản, nhanh nhất). Có bảng `TruckDay(TruckId, Date, Capacity, Booked)`:

```csharp
await using var tx = await _db.Database.BeginTransactionAsync();

var rows = await _db.Database.ExecuteSqlInterpolatedAsync($@"
    UPDATE TruckDay SET Booked = Booked + 1
    WHERE TruckId = {truckId} AND Date = {date} AND Booked < Capacity");

if (rows == 0)
    throw new ConflictException("Truck is full on that day");   // → 409, UI gợi ý ngày khác

_db.Deliveries.Add(new Delivery(orderId, truckId, date, window));
await _db.SaveChangesAsync();
await tx.CommitAsync();
```

Câu `UPDATE ... WHERE Booked < Capacity` kiểm tra và tăng trong **một câu lệnh**; SQL Server giữ khoá ghi trên dòng đó tới hết transaction → người thứ hai phải chờ, sau đó điều kiện sai → 0 dòng. Huỷ/dời lịch → `Booked - 1` trong cùng transaction. Dòng `TruckDay` chưa có → tạo trước (job sinh lịch 60 ngày tới) hoặc `MERGE`/insert bắt lỗi unique.

Cách 2: **khoá dòng cha bằng `UPDLOCK`** khi ràng buộc phức tạp hơn một con số (tổng kích thước, cửa sổ thời gian không chồng nhau):

```sql
BEGIN TRAN;
SELECT * FROM TruckDay WITH (UPDLOCK, HOLDLOCK)
WHERE TruckId = @truckId AND Date = @date;   -- người thứ 2 chờ ở đây
-- đọc các Delivery của (xe, ngày), kiểm tra luật trong C#, rồi INSERT
COMMIT;
```

`UPDLOCK` để hai người không cùng đọc rồi cùng ghi; `HOLDLOCK` giữ tới cuối transaction (và khoá cả phạm vi nếu dòng chưa tồn tại). Transaction phải **ngắn** (không gọi API ngoài bên trong).

Cách 3: **rowversion trên `TruckDay`** (optimistic): đọc, kiểm tra luật, tăng `Booked`, lưu; xung đột → retry hoặc 409. Hợp khi ít tranh chấp.

Không dùng: `lock` trong C# (nhiều instance thì vô dụng), nâng cả transaction lên `Serializable` (deadlock nhiều), distributed lock Redis (DB đã có sẵn khoá, thêm Redis chỉ thêm điểm hỏng; Hiệp dùng RedLock ở Quest Engine vì ở đó không có một dòng DB chung để khoá).

Cách xác nhận bug có thật: test tích hợp bắn 10 request song song vào xe còn 1 chỗ (`Task.WhenAll`) với DB thật (Testcontainers) → đúng 1 thành công, 9 nhận 409. Trên production: query đếm `Delivery` theo (xe, ngày) > `Capacity`.

Câu mẫu:
> Overbooking is a classic check-then-act race: two dispatchers both see one slot left and both save. Counting in the application doesn't fix it, even inside a transaction. I'd keep a capacity row per truck per day and book with a single conditional update — `SET Booked = Booked + 1 WHERE Booked < Capacity` — in the same transaction as inserting the delivery. If zero rows were updated, the truck is full and we return a 409 with other dates. If the rules get richer, like total shed size or time windows, I'd lock that truck-day row with `UPDLOCK, HOLDLOCK`, check the rules and insert, keeping the transaction short. I'd prove it with an integration test that fires ten parallel bookings at the last slot and expects exactly one success.

#### 8.6.4 Driver app offline + đồng bộ lại

**Vấn đề.** Tài xế đi vùng nông thôn Mỹ, mất sóng. App phải chạy offline: xem lộ trình hôm nay, chụp ảnh, lấy chữ ký, ghi nhận thanh toán, rồi đồng bộ khi có mạng. Dữ liệu trên máy là **bản chụp** tại lúc tải; văn phòng có thể đổi lịch, đổi địa chỉ, huỷ đơn sau đó.

**Luồng xuống (văn phòng → máy):**
- Mỗi delivery có `Version` (tăng mỗi lần sửa). App lưu bản chụp + version vào SQLite trên máy.
- Văn phòng đổi lịch → tăng version, gửi **push** (FCM/APNS) "lộ trình đã đổi" → app có mạng thì kéo lại (pull) các delivery có version mới. Push chỉ là **tín hiệu**, không chứa dữ liệu, không đảm bảo tới → app vẫn kéo định kỳ và khi mở app.
- Thay đổi quan trọng với delivery đã giao cho tài xế → đánh dấu cần xác nhận lại (giống cờ **RedeployRequired** Hiệp làm ở Joblogic: hạn mức đổi sau khi visit đã deploy xuống thiết bị kỹ thuật viên, nên phải deploy lại). Văn phòng thấy "tài xế chưa nhận bản mới" → gọi điện.
- Chỉ tải phần thay đổi (delta theo version / `updatedSince`); dữ liệu tham chiếu thì so hash (Joblogic tính **library hash** để thiết bị chỉ tải lại thư viện đã đổi).

**Luồng lên (máy → server) và idempotency:**
- Mỗi hành động trên máy (xác nhận giao, thu tiền) sinh **`ClientOperationId` (GUID) ngay trên máy**, lưu vào hàng đợi outbox của app, gửi lại tới khi server trả thành công.
- Server lưu id đã xử lý (unique index) → nhận lại lần 2 thì trả kết quả cũ, **không thu tiền 2 lần** (cùng mẫu với Pragmatic idempotency của Hiệp).
- Ảnh gửi riêng, lớn: upload thẳng lên S3 bằng **presigned URL**, có thể resume; bản ghi xác nhận tham chiếu tới key ảnh.
- Ghi **thời điểm thực tế trên máy** (`OccurredAt`, kèm GPS) tách khỏi thời điểm server nhận (`ReceivedAt`), vì đồng bộ có thể muộn vài giờ.

**Xung đột** (văn phòng huỷ đơn trong khi tài xế đang offline giao xong): không có công thức chung, phải hỏi PO. Nguyên tắc: **sự kiện thực tế ngoài đời thắng** (shed đã nằm ở sân khách thì ghi nhận đã giao), nhưng tạo **cảnh báo cho văn phòng xử lý** thay vì máy tự gộp âm thầm. So version: lệnh từ máy mang `BaseVersion`; khác version hiện tại → đưa vào danh sách cần người xem.

```csharp
[HttpPost("deliveries/{id}/complete")]
public async Task<IActionResult> Complete(Guid id, CompleteDeliveryRequest req)
{
    var existing = await _db.ProcessedOperations.FindAsync(req.ClientOperationId);
    if (existing is not null) return Ok(existing.Result);       // retry → kết quả cũ

    var delivery = await _db.Deliveries.SingleAsync(d => d.Id == id);
    var outcome = delivery.Complete(req.OccurredAt, req.SignatureKey, req.PhotoKeys, req.BaseVersion);
    // outcome = Completed hoặc CompletedWithConflict (đơn đã bị huỷ/đổi) → tạo task cho văn phòng

    _db.ProcessedOperations.Add(new ProcessedOperation(req.ClientOperationId, outcome));
    await _db.SaveChangesAsync();   // cùng transaction; unique key chặn 2 request song song
    return Ok(outcome);
}
```

Thu tiền tại chỗ: tốt nhất qua thiết bị/SDK của payment provider (Stripe Terminal…), tiền thật do provider xác nhận qua webhook; app chỉ ghi "đã nhận séc/tiền mặt" kèm ảnh → kế toán đối soát. Không để app offline tự quyết định số dư.

Câu mẫu:
> I'd treat what's on the driver's phone as a snapshot with a version number. When the office reschedules, we bump the version and send a push, but the push is only a hint; the app also pulls changes whenever it's online, and the office can see which drivers haven't picked up the latest version. It's the same idea as the "redeploy required" flag I built at Joblogic, where engineers' devices held a copy of the visit. Going the other way, every action on the phone gets an operation ID created on the device, and the server stores processed IDs, so a retry after a dropped connection never records a delivery or a payment twice. If the office cancelled an order that the driver had already delivered offline, I wouldn't merge it silently: the real-world event wins, and we raise a task for the office.

#### 8.6.5 Thông báo khách (SMS/email)

**Khi nào gửi:** đã lên lịch giao (ngày + cửa sổ giờ), nhắc trước 1–2 ngày (nhắc chuẩn bị mặt bằng), "tài xế đang trên đường" (tuỳ), đã giao xong (kèm ảnh, link hoá đơn/số dư), đổi lịch/huỷ.

**Thiết kế:**
- Gửi **qua queue/background**, không gọi Twilio/SendGrid trong request lên lịch: provider chậm/lỗi không được làm hỏng việc lưu lịch. Sự kiện `DeliveryScheduled` → outbox → worker gửi.
- **Idempotent**: key = `(DeliveryId, NotificationType, ScheduleVersion)`, unique index trên bảng `NotificationLog`. Queue at-least-once gửi lại message → kiểm tra log, không nhắn khách 2 lần. Đổi lịch → version mới → tin mới hợp lệ.
- **Nhắc trước ngày giao**: job định kỳ quét delivery ngày mai **theo timezone của khách/xưởng**, gửi trong giờ hợp lý (không nhắn 6 giờ sáng); trước khi gửi kiểm tra lại lịch còn đúng không (đã dời thì bỏ).
- **Opt-out / đồng ý**: Mỹ có luật **TCPA** (SMS cần đồng ý), trả lời **STOP** phải ngừng (Twilio tự xử lý STOP và báo lại) → lưu trạng thái đồng ý theo kênh; email marketing khác email giao dịch. Mình không phải luật sư → "check with the PO/legal", nhưng biết từ khoá là điểm cộng.
- Template theo tenant (tên công ty bán shed, logo), số điện thoại theo định dạng **E.164** (`+1…`).
- Retry có backoff khi provider lỗi tạm thời; lỗi vĩnh viễn (số sai) → ghi lại, hiện cho văn phòng; dead-letter queue.
- Lưu lịch sử gửi (đã gửi, đã tới, thất bại từ webhook trạng thái của provider) → hỗ trợ trả lời "tôi không nhận được tin".

```csharp
public async Task Handle(DeliveryScheduled e, CancellationToken ct)
{
    var key = $"{e.DeliveryId}:{NotificationType.Scheduled}:{e.ScheduleVersion}";
    if (await _db.NotificationLogs.AnyAsync(n => n.Key == key, ct)) return;   // đã gửi

    var customer = await _customers.GetAsync(e.CustomerId, ct);
    if (!customer.SmsConsent) return;                                          // tôn trọng opt-out

    var msgId = await _sms.SendAsync(customer.PhoneE164, _templates.Render(e), ct);
    _db.NotificationLogs.Add(new NotificationLog(key, msgId, _time.GetUtcNow()));
    await _db.SaveChangesAsync(ct);   // unique index trên Key chặn worker song song
}
```

Lưu ý trung thực: giữa "đã gửi SMS" và "đã ghi log" vẫn có khe nhỏ (crash đúng lúc đó → gửi lại 1 lần). Gửi tin nhắn ra ngoài không thể exactly-once tuyệt đối; giảm bằng cách ghi log trạng thái `Sending` trước, hoặc truyền idempotency key cho provider nếu provider hỗ trợ. Nói được giới hạn này là mức Senior.

Câu mẫu:
> Notifications are a side effect, so they shouldn't be able to break scheduling. The scheduling transaction writes an event to an outbox, and a worker sends the SMS or email. The queue delivers at least once, so each message has a key — delivery, notification type and schedule version — with a unique index, so a redelivered message doesn't text the customer twice, but a reschedule still sends a new one. Reminders run per the customer's time zone at a sensible hour, and re-check the schedule just before sending. We store consent per channel and honour STOP replies, which matters in the US under TCPA. Strictly speaking, sending to an external provider can't be exactly-once, so I'd aim for "at most one duplicate in a rare crash" and log every send for support.

#### 8.6.6 Câu hỏi luyện + tự kiểm tra (Mid vs Senior)

1. *Two managers reorder the production queue at the same time. What happens?*
   Mid: "dùng transaction". Senior: đặt tên lost update, rowversion → 409 + refresh, SignalR, cân nhắc version theo cả hàng đợi.
2. *How would you prevent overbooking a delivery truck?*
   Mid: "kiểm tra số lượng trước khi lưu". Senior: gọi tên check-then-act race, atomic conditional UPDATE / `UPDLOCK`, vì sao `lock` C# và Serializable không ổn, test song song chứng minh.
3. *The office reschedules a delivery while the driver is offline.* → version + push là tín hiệu + pull + cảnh báo khi tài xế chưa nhận, xung đột cho người xử lý.
4. *The driver app retried and the payment was recorded twice. How do you fix and prevent it?* → idempotency key sinh trên máy, unique index, script sửa dữ liệu có audit, báo PO số đơn bị ảnh hưởng.
5. *A customer says they got the delivery SMS three times.* → at-least-once queue không có khoá idempotent; thêm `NotificationLog` unique key; kiểm tra log provider; nói về giới hạn exactly-once.
6. *How do you know who marked a shed as built?* → state machine + bảng history append-only + đăng nhập PIN trên tablet dùng chung.
7. *What would you ask the PO before building delivery scheduling?* → năng lực tính theo chuyến hay kích thước, vùng giao và phí, có yêu cầu trả đủ tiền trước giao không, site readiness, ai được dời lịch, thông báo khách những lúc nào, giao lại có phí không.

### 8.7 Inventory
- Hàng có sẵn bán ngay; trạng thái Available → Reserved (đang có quote/order giữ) → Sold. Chống bán 2 lần: atomic UPDATE `WHERE Status='Available'` hoặc rowversion.
- Giữ chỗ có hạn (reservation expiry) → job nền giải phóng.

### 8.8 Multi-tenant settings
Mỗi công ty bán shed là một tenant (có store/region bên trong): cấu hình thuế, template, quy trình, RTO provider được bật, feature theo gói. Cô lập dữ liệu → section 17.

### 8.9 Tích hợp bên thứ ba (phạm vi chung)
Payment provider, API thuế, công ty RTO, configurator 3D/website bán hàng, SMS/email, kế toán (QuickBooks…), Zapier/webhook ra ngoài. Nguyên tắc → section 22.

### 8.10 Câu hỏi luyện (domain)
1. Walk me through how a quote becomes a delivered order. What data changes at each step?
2. A customer paid a deposit, then the quote was revised. How do you keep the balance due correct?
3. Balance due is wrong for some orders. How do you investigate and fix? (xem 9.2)
4. Prices go up after a quote was sent. What happens to the quote?
5. How would you store money and handle rounding?
6. How do you calculate a rent-to-own payment schedule so the total matches exactly?
7. Delivery dates show one day off for some customers. Why, and how do you fix it?
8. How do you store and display dates across North American time zones?
9. A contract was signed and then the template changed. A customer disputes it a year later. What do you show?
10. PDF generation takes 10 seconds and sometimes breaks with special characters. How do you fix it?
11. Two dealers try to sell the same inventory unit at the same time. What happens?
12. The driver app is offline when the office reschedules a delivery. How do you handle it?
13. How would you prevent overbooking a delivery truck?
14. How would you model order statuses and who can change them?
15. How would you add a new RTO provider?
16. What would you ask the PM before building "cancel order"?
17. How do you make sure every change to an order is traceable?
18. Sales tax: whose address, when is it locked, what if the rate changes?
19. Markup vs margin — what's the difference? Which would the dealer see?
20. How would you design an owner/customer portal that shows payments and balance? (Urbanise có owner portal — dễ bị hỏi)

---

## 9. Câu hỏi PO: làm rõ yêu cầu, edge case, ưu tiên — Khả năng: Rất cao (85%)

🟢 Nối value: **Driven by Customer Success** (xem mục tiêu của khách như của mình, khách nội bộ gồm cả PM), **1% Improvement** (từng phân đoạn thay vì phiên bản hoàn hảo, linh hoạt khi đổi yêu cầu), **Enjoy Problem Solving** (80/20, biết hỏi giúp), **Be Accountable** (báo sớm, chính trực).
Khung: **làm rõ (hỏi lại) → đề xuất phương án nhỏ giao trước → edge case → đo kết quả**. PO đánh giá: hiểu "vì sao", hỏi đúng câu, giao tiếp rõ, không tự ý làm thêm, chịu trách nhiệm.

### 9.1 Bảng tình huống
| Câu hỏi | Ý chính |
|---|---|
| Quote đã gửi, bảng giá tăng | Quote là snapshot có hạn; giữ giá tới hết hạn; muốn cập nhật thì tạo **revision** mới, khách thấy so sánh. Hỏi PO chính sách |
| Balance due sai ở một số đơn | Lấy danh sách đơn sai, tìm điểm chung (có refund? đổi thuế? sửa đơn sau deposit? làm tròn?), so ledger vs số lưu, sửa công thức + **script sửa dữ liệu có audit**, test hồi quy, báo khách bị ảnh hưởng |
| Huỷ đơn khi đã vào sản xuất | Hỏi: phí huỷ? hoàn deposit bao nhiêu? sản phẩm dở thành inventory? ai được duyệt? thông báo ai? RTO contract huỷ thế nào? có giới hạn thời gian? |
| Ngày giao lệch 1 ngày | Section 8.4 |
| Yêu cầu mơ hồ | Hỏi "vấn đề người dùng là gì", viết acceptance criteria + ví dụ cụ thể (Given/When/Then), mock nhanh, xác nhận lại trước khi code |
| Đổi yêu cầu giữa sprint | Nêu ảnh hưởng (thời gian, rủi ro), để PO chọn đổi phạm vi; không âm thầm làm thêm |
| Feature lớn | Cắt **lát dọc** (vertical slice), feature flag, giao bản tối thiểu dùng được trước ("1% improvements") |
| Không đồng ý với PO | Đưa dữ liệu/rủi ro, đề xuất phương án thay thế; PO quyết về giá trị, dev chịu trách nhiệm về cách làm; quyết xong thì cam kết |
| Ưu tiên bug vs feature | Theo tác động: tiền sai / dữ liệu sai / khách bị chặn trước; còn lại vào backlog có mức ưu tiên |
| Ước lượng | Chia nhỏ, nêu giả định và rủi ro, khoảng (range) thay vì một con số, cập nhật sớm khi lệch |
| Trễ deadline | Báo sớm, nêu nguyên nhân, đề xuất cắt phạm vi hoặc lùi ngày, không im lặng |
| Khách yêu cầu tính năng chỉ cho họ | Hỏi vấn đề gốc; có thể giải bằng cấu hình chung theo tenant thay vì code riêng |
| Feature đã release mà không ai dùng | Đo (analytics), hỏi người dùng, cải thiện hoặc gỡ |
| PO muốn làm nhanh, bạn thấy rủi ro kỹ thuật | Nêu rủi ro cụ thể (mất tiền, mất dữ liệu), đề xuất phương án nhỏ an toàn, ghi lại nợ kỹ thuật có ticket |

### 9.2 Câu mẫu "balance due sai"
> First I'd get the list of affected orders and look for what they have in common — refunds, a tax change, an edit after the deposit, or a rounding difference. I'd compare the stored balance with what the payment ledger says, find the rule that's wrong, and write a failing test for it. Then I'd fix the calculation, and correct the affected orders with a reviewed script that writes audit entries, so we can explain every change. Finally I'd tell the PM how many customers were affected, so support can contact them if needed.

### 9.3 Câu mẫu "yêu cầu mơ hồ"
> I'd start by asking what problem the user has, not how the screen should look. Then I'd write acceptance criteria with two or three concrete examples, including the awkward ones — a partial payment, a cancelled order, a different time zone — and confirm them with you before I start. If it's still unclear, I'd build the smallest version behind a feature flag and get feedback early.

### 9.4 Câu mẫu "làm việc với PM"
> I like being involved early, when a feature is still a problem rather than a spec, because that's when edge cases are cheap to find. At Joblogic, the spend-limit feature looked simple until we walked through real scenarios — later visits and data already on engineers' devices. At PlaySweeps, the client designed the quest formulas and I clarified the requirements with them before writing the technical design.

### 9.5 Edge case checklist (dùng cho mọi feature PO hỏi)
- Null / rỗng / rất lớn / số âm / 0.
- Trùng (double click, retry, webhook gửi 2 lần).
- Đồng thời (2 người sửa, 2 đại lý bán cùng một hàng).
- Thời gian (múi giờ, DST, cuối tháng, hết hạn, quá khứ).
- Tiền (làm tròn, refund, trả quá, tiền tệ, thuế đổi).
- Trạng thái (huỷ giữa chừng, sửa sau khi khoá, quay lại bước trước).
- Quyền (ai được làm, tenant khác, store khác).
- Tích hợp lỗi (bên thứ ba chậm/sập/trả sai).
- Dữ liệu cũ (record tạo trước khi có feature → migration/backfill).
- Thông báo (gửi ai, gửi mấy lần, opt-out).
- Báo cáo/audit (ai cần thấy thay đổi này).

### 9.6 Câu hỏi luyện (PO)
1. How do you work with a product manager?
2. A requirement is unclear. What do you do?
3. The requirement changes in the middle of the sprint. What do you do?
4. How do you break a large feature into deliverable pieces?
5. You disagree with a product decision. What do you do?
6. How do you prioritise bugs against new features?
7. How do you estimate? What if you're wrong?
8. You'll miss a deadline. When and how do you tell me?
9. A customer reports wrong numbers. Walk me through your response.
10. What would you ask me before building "cancel order" / "reschedule delivery" / "partial refund"?
11. How do you know a feature you shipped was successful?
12. What does "1% improvements" mean to you? Give an example.
13. Tell me about a time you found an edge case nobody had thought of.
14. How do you explain a technical problem to a non-technical person?
15. Give an example of taking ownership beyond your task.

---

## 10. Behavioral STAR (tiếng Anh) — Khả năng: Cao (75%)

🟢 Bộ câu chuyện theo từng core value (và bảng câu chuyện × value) nằm ở `notes/S-seadev-culture.md` mục 3 và 5 — dùng chung cho cả vòng tech.
STAR: **Situation** (1–2 câu) → **Task** (1 câu) → **Action** (nhiều nhất, dùng "I") → **Result** (con số, hậu quả) → bài học. 60–90 giây.

### 10.1 Bộ câu chuyện
| Câu hỏi | Chất liệu | Ghi chú |
|---|---|---|
| Inherited a system / hard to maintain (Q141) | **Socure KYC**: tiếp quản từ đồng nghiệp, tự đọc dashboard/decision module, prototype client có giả định sai, sửa đến khi ổn định | Kể rõ giả định sai là gì **[Hiệp điền chi tiết]** |
| Led a feature end to end | **Quest Engine V2**: TDD, Cosmos, Redis lock, idempotency claim, lên prod | Có thể nói số project/ticket |
| Hardest production bug / on-call (Q137) | Incident điều tra bằng App Insights + Loki + Splunk | **[Hiệp điền: 1 vụ cụ thể, triệu chứng, công cụ, nguyên nhân, fix, con số]** |
| Bug không tái hiện ở local (Q142) | Dùng Splunk BI event để dựng lại hành trình user | **[Hiệp điền]** |
| Performance problem (Q138) | Tối ưu fetch/cache AVA config | **[Hiệp điền con số trước/sau]** |
| Edge case from understanding business | **Job Spend Limit** (visit 2+, RedeployRequired) | Câu mẫu ở 2.2 |
| Disagreement with a technical decision (Q140) | **[Hiệp điền]** — gợi ý: lock vs DB constraint, sync vs async reward | Kết: đưa dữ liệu, chấp nhận quyết định chung |
| Incident caused by a design decision (Q139) | **[Hiệp điền]** — gợi ý: mirror balance ghi giá trị tuyệt đối | Nói bài học, không đổ lỗi |
| Working remotely with a foreign team | PLAYSTUDIOS (Mỹ): Slack hằng ngày, họp technical design; Joblogic (UK): code review Azure DevOps | Chênh múi giờ, giao tiếp async |
| Learning quickly | Go + AWS (KMS, S3, SES) ở Altar; Rive với designer nước ngoài | JD: "learn quickly and adapt" |
| Proactive improvement / 1% | Exponential rate limiting cho API nhạy cảm; tối ưu cache AVA | |
| Mentoring / leading | Lead nhóm 4 intern ở Astraler; review PR feature mình lead | |
| Failure / mistake | **[Hiệp điền]** — chọn lỗi thật, nhỏ, đã rút kinh nghiệm | Không chọn lỗi làm mất tiền khách lớn |
| Tight deadline | **[Hiệp điền]** | |
| Conflict with a colleague | **[Hiệp điền]** | Tập trung vào vấn đề, không vào người |
| Handover from client with good feedback | Altar: client phản hồi tốt khi bàn giao | |

### 10.2 Mẫu Socure (điền chi tiết thật trước khi dùng)
> **S:** At PlaySweeps we needed identity verification for US players, using Socure — document checks, SSN verification and manual review. The first integration had been started by a colleague, based on a prototype from the client. **T:** I took over the integration and had to get it working reliably in production. **A:** I didn't know Socure, so I studied their dashboard and decision module and compared what the vendor actually returned with what the prototype assumed. I found the prototype's assumptions were wrong [Hiệp điền: ví dụ cụ thể], so I reworked the flow, handled the different decision outcomes explicitly, and tested the edge cases with the client's team. **R:** The KYC flow then ran stably in production for all US players. **Lesson:** when taking over an integration, verify the vendor's real behaviour instead of trusting the existing code.

### 10.3 Tiếng Anh — lỗi hay mắc
- **-s ngôi 3**: "it depends", "the service calls", "the user pays".
- Không "is depend", không "will be encountered" (bị động thừa) → "we'll hit this problem".
- Dùng thì quá khứ khi kể: "I built", "we found", "it ran".
- Câu ngắn, mỗi câu một ý. Khi chưa nghe rõ: "Sorry, could you repeat the last part?" / "Just to make sure I understand, you're asking about…".
- Khi cần nghĩ: "That's a good question — let me think for a second."
- Khi không biết: "I haven't used that directly, but here's how I'd approach it…"

### 10.4 Câu hỏi luyện
1. Tell me about the most difficult production bug you investigated.
2. Tell me about a performance problem you solved.
3. Tell me about a production incident caused by a design decision.
4. Tell me about a time you disagreed with a technical decision.
5. Tell me about a system you inherited that was difficult to maintain.
6. Tell me about a bug you couldn't reproduce locally.
7. Tell me about a feature you led from design to release.
8. Tell me about a mistake you made and what you learned.
9. Tell me about working with a team in another time zone.
10. Tell me about a time you learned a new technology quickly.
11. Tell me about a time you improved something nobody asked you to.
12. Tell me about a time you had to push back on a deadline or requirement.

---

## 11. C# & .NET nền tảng — Khả năng: Cao (65%)

SA không khai C# nhưng là vị trí C# → có thể hỏi nhanh vài câu nền để lọc. Trả lời 30 giây mỗi câu, có ví dụ.

### 11.1 OOP & kiểu dữ liệu
- **4 nguyên lý OOP**: Encapsulation (giấu trạng thái, chỉ đổi qua method có luật — `Order.Cancel()`), Abstraction (interface che chi tiết — `IPaymentProvider`), Inheritance (tái sử dụng/đa hình, dùng tiết kiệm), Polymorphism (cùng lời gọi, hành vi khác theo kiểu — Strategy).
- **Class vs object**: khuôn vs thực thể.
- **Value type vs reference type**: value (struct, int, decimal, DateTime, enum) chứa dữ liệu trực tiếp, copy khi gán; reference (class, string, array, delegate) chứa tham chiếu tới heap. "Value type luôn nằm trên stack" là **sai** (field của class nằm trên heap).
- **class vs struct**: struct cho giá trị nhỏ, bất biến (`Money` có thể là `readonly record struct`); tránh struct lớn/mutable.
- **record**: so sánh theo giá trị, bất biến (`init`), `with` expression; hợp DTO, value object, message. `record struct` (C# 10).
- **const vs readonly**: const là hằng compile-time (nhúng vào assembly gọi), readonly gán trong constructor (runtime). `static readonly` cho object.
- **Access modifiers**: public, private, protected, internal, protected internal, private protected, `file` (C# 11).
- **abstract class vs interface**: abstract có state + code chung, kế thừa đơn; interface là hợp đồng, đa kế thừa, có default method (C# 8). Chọn interface cho DI/test; abstract khi có code chung thật.
- **override / virtual / new**: virtual cho phép ghi đè, override ghi đè (đa hình), `new` che giấu (không đa hình — gọi qua kiểu cha thì chạy bản cha).
- **Overloading vs overriding**: cùng tên khác tham số (compile-time) vs ghi đè ở lớp con (runtime).
- **Nullable**: `int?` (`Nullable<T>`) và **nullable reference types** (`string?`, bật `<Nullable>enable`) — cảnh báo compile, không phải runtime.
- **sealed**: chặn kế thừa (hiệu năng nhỏ + rõ ý đồ).
- **static class / extension method**: extension là static method gọi như instance (`IServiceCollection.AddXxx`, LINQ).
- **Boxing/unboxing**: value type → object (cấp phát heap). Tránh trong vòng lặp nóng, collection không generic (`ArrayList`).
- **Generics**: type-safe, không boxing; constraint `where T : class, new()`. Covariance `out`/contravariance `in` (`IEnumerable<out T>`).
- **ref / in / out**: ref truyền tham chiếu (đọc+ghi, phải khởi tạo), out (phải gán trong method), in (chỉ đọc, tránh copy struct lớn).
- **Delegate / event / Func / Action**: delegate là kiểu con trỏ hàm; event là delegate chỉ class chủ được invoke; `Func<T,TResult>`, `Action<T>`, `Predicate<T>`. Lambda, closure (bắt biến — bẫy vòng lặp cũ).
- **Pattern matching**: `is`, `switch` expression, property pattern `{ Status: OrderStatus.Delivered }`, relational `> 100`, list pattern (C# 11).
- **Primary constructor** (C# 12): `class OrderService(AppDbContext db)`; tham số không phải readonly field.
- **Modern C#**: `required` members, raw string literal, collection expressions `[1, 2, 3]` (C# 12), file-scoped namespace, global using, top-level statements.
- **string**: bất biến; nối nhiều lần dùng `StringBuilder`; so sánh `StringComparison.OrdinalIgnoreCase`; `string.Equals` vs `==`.
- **Equals / GetHashCode**: override cả hai cùng nhau; dùng làm key Dictionary.
- **Exceptions**: `throw;` giữ stack trace (khác `throw ex;`); custom exception khi caller cần bắt riêng; exception filter `catch (X e) when (...)`; `finally`/`using`.

### 11.2 Collections & LINQ
- **Array vs List<T>**: cố định vs động. **Dictionary** O(1) tra theo key; **HashSet** tập không trùng; `ConcurrentDictionary` khi đa luồng.
- **IEnumerable / ICollection / IList / IReadOnlyList**: duyệt / + Count, Add / + index. Trả `IReadOnlyList<T>` cho API nội bộ.
- **yield return**: iterator lười, sinh từng phần tử.
- **LINQ deferred execution**: query chỉ chạy khi tiêu thụ (`ToList`, `First`, `Count`, `foreach`); dùng nhiều lần → chạy nhiều lần.
- **IEnumerable vs IQueryable**: `IQueryable` + `Expression` → provider dịch sang SQL; `IEnumerable` + `Func` → chạy trong RAM. `AsEnumerable()`/`ToList()` sớm → kéo cả bảng (`notes/03`).
- `First` vs `FirstOrDefault` vs `Single`; `Any()` thay `Count() > 0`; `Select` vs `SelectMany`; `GroupBy`.

### 11.3 Runtime, GC, IDisposable
- **CLR**: chạy IL, JIT compile sang mã máy, quản lý bộ nhớ (GC), type safety, exception. **.NET Core/.NET 5+** cross-platform; .NET Framework chỉ Windows. .NET 8 là LTS (11/2023 – 11/2026), .NET 10 LTS (11/2025).
- **GC thế hệ**: Gen 0 (mới, dọn thường xuyên) → Gen 1 → Gen 2 (sống lâu); **LOH** (> 85 KB) dọn cùng Gen 2, dễ phân mảnh. Server GC vs Workstation GC. GC dọn **managed memory**, không dọn tài nguyên unmanaged (file, socket, connection).
- **IDisposable / using**: giải phóng tài nguyên ngay (connection về pool, file handle). `await using` cho `IAsyncDisposable`. Finalizer chỉ là lưới an toàn. DI container dispose Scoped/Transient `IDisposable` khi hết scope.
- **Memory leak trong .NET**: event handler không gỡ, static collection lớn mãi, cache không giới hạn, captive dependency giữ DbContext, timer. Điều tra: `dotnet-counters` (gc-heap-size, gen-2 count), `dotnet-gcdump`/`dotnet-dump` (đếm object, chuỗi giữ tham chiếu).
- **Span<T>/Memory<T>**: thao tác vùng nhớ không cấp phát (biết khái niệm).

### 11.4 Câu hỏi luyện
1. Value type vs reference type? Where do they live?
2. class vs struct vs record — when each?
3. Abstract class vs interface?
4. `override` vs `new`?
5. What does `IDisposable` do and how is it different from garbage collection?
6. How does the GC work? What's the LOH?
7. What's boxing? Why avoid it?
8. IEnumerable vs IQueryable? What's deferred execution?
9. `const` vs `readonly`?
10. What are nullable reference types?
11. Delegates vs events? Func vs Action?
12. What's new in recent C# versions that you use?
13. `throw` vs `throw ex`?
14. How would you find a memory leak in a .NET service?
15. Why `decimal` for money? (độ chính xác thập phân, 28–29 chữ số, chậm hơn double nhưng đúng)

---

## 12. Async / concurrency / thread pool — Khả năng: Cao (60%) — Đã học ✅ (`notes/01`)

### 12.1 Ý chốt
- `await` I/O **không giữ thread**; trong lúc chờ 0 thread bị chiếm (IOCP/epoll). Async **tăng throughput, không giảm latency** một request (100 thread, chờ DB 200 ms: sync ~500 req/s, async có thể ~20.000 req/s).
- **Task ≠ Thread**: Task là "lời hứa có kết quả"; thread là luồng OS (~1 MB stack).
- **Async vs concurrency vs parallelism**: async = không chặn khi chờ; concurrency = nhiều việc tiến triển xen kẽ; parallelism = chạy cùng lúc trên nhiều core (`Parallel.ForEach`, PLINQ — cho CPU-bound).
- **`.Result`/`.Wait()`** (sync-over-async): chặn thread + cần thêm thread cho continuation → **thread-pool starvation** (ASP.NET Core) hoặc **deadlock** (có SynchronizationContext: ASP.NET cũ, WPF). `GetAwaiter().GetResult()` vẫn chặn.
- **Starvation**: latency tăng vọt, **CPU thấp**, pool bơm thêm ~1–2 thread/giây. Xác nhận: `dotnet-counters` (ThreadPool Queue Length), `dotnet-stack`/`dotnet-dump` (stack nằm trong `.Result`). Tạm: `SetMinThreads`. Gốc: async all the way.
- **SynchronizationContext**: nơi continuation chạy tiếp (UI thread). ASP.NET Core **không có** → `ConfigureAwait(false)` chủ yếu cần cho thư viện.
- **Quên await**: mất exception, DbContext bị dispose, "second operation" race, mất việc khi shutdown. Việc nền → `Channel` + `BackgroundService` hoặc queue/outbox.
- **`async void`**: exception làm **crash process**; chỉ dùng cho event handler.
- **CancellationToken**: truyền suốt chuỗi gọi (`HttpContext.RequestAborted`), dừng việc khi client huỷ/timeout.
- **`Task.WhenAll` vs await tuần tự**: song song khi các việc độc lập; **không** dùng chung một DbContext (throw "second operation") → mỗi task một context (`IDbContextFactory`); cẩn thận cạn connection pool.
- **Race condition**: nhiều luồng đọc-sửa-ghi trạng thái chung. Trong process: `lock`, `SemaphoreSlim` (async), `Interlocked`, `ConcurrentDictionary`. Trong DB: atomic UPDATE, rowversion. Nhiều instance: DB constraint, distributed lock (Redis) là cuối cùng.
- `lock` không dùng được với `await` bên trong → `SemaphoreSlim.WaitAsync`.
- **ValueTask**: giảm cấp phát khi thường hoàn thành đồng bộ; chỉ await một lần.
- **IAsyncEnumerable** + `await foreach`: stream dữ liệu lớn.

### 12.2 Câu hỏi luyện
1. What happens when you `await` a database call? Is a thread blocked?
2. Why is `.Result` dangerous in ASP.NET Core?
3. What is thread-pool starvation, and how do you confirm it?
4. Task vs Thread?
5. Async vs concurrency vs parallelism?
6. When do you use `Task.WhenAll`? What's the trap with DbContext?
7. What happens if you forget to await?
8. Why avoid `async void`?
9. How do you use CancellationToken in a Web API?
10. How do you protect shared state across threads? Across instances?
11. Does `ConfigureAwait(false)` matter in ASP.NET Core?

---

## 13. ASP.NET Core: DI, middleware, filter, exception — Khả năng: Cao (65%) — Đã học ✅ (`notes/01`, `notes/02`)

### 13.1 DI
- **Lifetime**: Singleton (1 cho cả app — cache, config, HttpClient factory), Scoped (1 mỗi request — DbContext, unit of work), Transient (mỗi lần resolve — service nhẹ, không state).
- Scope tạo đầu request, **Dispose** cuối request.
- **Captive dependency**: Singleton giữ Scoped (DbContext) → context sống cả process: không thread-safe ("second operation"), change tracker phình, dữ liệu cũ. Sửa: đổi lifetime hoặc `IServiceScopeFactory`/`IDbContextFactory`. Phòng: `ValidateScopes` + `ValidateOnBuild`.
- **Quy tắc**: không inject service sống ngắn hơn vào service sống dài hơn.
- **Constructor injection vs service locator** (`IServiceProvider.GetService` khắp nơi): service locator giấu phụ thuộc, khó test → chỉ dùng ở chỗ hạ tầng (factory, middleware).
- `BackgroundService` là Singleton → tạo scope mỗi lần xử lý để lấy DbContext.
- Keyed services (.NET 8): `AddKeyedScoped<IRtoProvider, ProviderA>("A")`.
- PlaySweeps dùng **Autofac**; built-in DI đủ cho đa số.

### 13.2 Pipeline, middleware, filter
- Kestrel → middleware lồng nhau → endpoint; response đi ngược. Không gọi `next` = short-circuit.
- Thứ tự chuẩn: ExceptionHandler → HSTS/HttpsRedirection → Static files → Routing → CORS → **Authentication → Authorization** → RateLimiter → endpoints. AuthZ trước AuthN → "token đúng mà vẫn 401".
- **"Middleware lo HTTP, Filter lo Action"**: middleware cho mọi request (exception, correlation id, auth, rate limit); filter chỉ cho action MVC, thấy action + tham số đã bind (validation, audit, permission).
- Filter order: Authorization → Resource → (model binding) → Action → Exception → Result. Endpoint filter cho Minimal API.
- Middleware class là singleton → inject Scoped qua tham số `InvokeAsync`.

### 13.3 Exception handling & logging
- Global: `UseExceptionHandler` + `IExceptionHandler` (.NET 8) + `AddProblemDetails`; 500 không lộ chi tiết; kèm `traceId`.
- "Exception cho chuyện bất ngờ, Result cho chuyện bình thường".
- Log 4xx là Warning, 5xx là Error + alert. Structured logging (Serilog/`ILogger` với template `{OrderId}`), correlation id.

### 13.4 Cấu hình & khác
- `appsettings.json` → `appsettings.{Environment}.json` → biến môi trường → secret store (User Secrets local; AWS Secrets Manager/Parameter Store prod). **Options pattern** `IOptions/IOptionsSnapshot/IOptionsMonitor`.
- Health checks: `/health/live` (process sống) vs `/health/ready` (DB, phụ thuộc sẵn sàng).
- Minimal API vs Controller: minimal gọn cho API nhỏ; controller cho app lớn có filter, convention.
- `IHostedService`/`BackgroundService` cho việc nền; graceful shutdown qua `stoppingToken`.
- Rate limiting built-in (.NET 7+): fixed window, sliding, token bucket, concurrency.
- Output caching / response caching.

### 13.5 Câu hỏi luyện
1. Explain Singleton, Scoped, Transient with real examples.
2. What's a captive dependency? How do you detect and fix it?
3. Explain the request pipeline. Why does middleware order matter?
4. Middleware vs filter — where would you put audit logging / permission check / correlation ID?
5. How do you handle exceptions globally in a Web API?
6. How do you manage configuration and secrets across environments?
7. How do you run background work in ASP.NET Core?
8. Liveness vs readiness health check?
9. Minimal API or controllers?

---

## 14. ASP.NET MVC — Khả năng: Cao (60%) — ❌ chưa học

JD ghi "ASP.NET MVC và/hoặc Web API"; codebase Ops Hub có thể là MVC. Hiệp có kinh nghiệm thật ở Joblogic (20 view `.cshtml`, 27 controller, Razor + jQuery + Vue nhúng).

### 14.1 Kiến thức
| Chủ đề | Cần nói được |
|---|---|
| MVC flow | Routing → controller action → model binding → validation → action chạy → `ViewResult` → Razor render HTML → response |
| Routing | Conventional (`{controller}/{action}/{id?}`) vs attribute (`[Route("quotes/{id}")]`); Areas cho module lớn |
| Model binding | Nguồn: route, query, form, body (`[FromBody]` chỉ một lần), header; bind vào **ViewModel**, không bind thẳng entity |
| **Over-posting / mass assignment** | Form gửi thêm `IsApproved=true` hoặc `Price=1` → bind vào entity → bị sửa. Chặn: ViewModel chỉ có field cho phép, map tay; tránh `[Bind]` dài, tránh `TryUpdateModelAsync` không giới hạn |
| Validation | DataAnnotations (`[Required]`, `[Range]`) / FluentValidation; `ModelState.IsValid`; **luôn validate server** (client-side chỉ là UX); trả lại view với lỗi |
| **Anti-forgery (CSRF)** | Cookie auth → trình duyệt tự gửi cookie → site lạ có thể POST thay user. `<form>` tag helper tự thêm token; `[ValidateAntiForgeryToken]` hoặc `AutoValidateAntiforgeryToken` toàn cục. API bearer token thì không cần; AJAX gửi token qua header |
| **PRG** (Post-Redirect-Get) | POST xong `RedirectToAction` → F5 không submit lại (chống double submit order); `TempData` để hiện thông báo |
| Filters | Authorization → Resource → Action → Exception → Result; permission (Joblogic `[Permission(PROJECT_DOWNLOAD)]`), audit, transaction |
| ViewModel vs ViewBag/ViewData | ViewModel có kiểu (nên dùng); ViewBag dynamic, dễ lỗi |
| Layout, partial view, **view component**, **tag helper** | Tái sử dụng UI; view component có logic + DI riêng (vd. widget balance); tag helper thay HTML helper |
| Razor | `@model`, `@if`, `@foreach`, `asp-for`, `asp-validation-for`; **tự encode** `@value` |
| **XSS** | Nguy hiểm khi `Html.Raw` (rich text T&C) → sanitize (HtmlSanitizer); CSP header |
| Optimistic concurrency trong MVC | Gửi `RowVersion` qua hidden field, gán `OriginalValue` khi lưu → `DbUpdateConcurrencyException` → báo người dùng |
| Auth | Cookie authentication, `[Authorize(Roles/Policy)]`, policy-based authorization, resource-based (`IAuthorizationService`) |
| MVC vs Web API | MVC trả HTML (server render), API trả JSON; ASP.NET Core gộp: `Controller` (có view) vs `ControllerBase` + `[ApiController]` (tự validate → 400, binding suy luận) |
| Razor Pages | Mô hình page-based (PageModel), hợp form CRUD đơn giản |
| ASP.NET MVC 5 (.NET Framework) vs ASP.NET Core MVC | Cũ: `System.Web`, IIS, Global.asax, không DI built-in; mới: cross-platform, middleware, DI built-in. Codebase partner có thể còn MVC 5 → biết để migrate dần |
| Bundling, static files | `wwwroot`, cache-busting `asp-append-version` |

### 14.2 Câu mẫu
> In Joblogic's back-office, pages are Razor views with Vue components embedded for the interactive parts. Controllers stay thin: they bind to a view model, check permissions with an attribute filter, then send a message to the backend service and map the result. I never bind directly to entities, to avoid over-posting, and all POST forms use the anti-forgery token because it's cookie-authenticated.

### 14.3 Câu hỏi luyện
1. Walk me through what happens when a user submits a form in ASP.NET MVC.
2. What is over-posting and how do you prevent it?
3. What is CSRF? Why does MVC need anti-forgery tokens but a bearer-token API doesn't?
4. What is the Post-Redirect-Get pattern?
5. Client-side vs server-side validation?
6. ViewModel vs ViewBag?
7. Partial view vs view component?
8. How do you prevent XSS when showing rich-text terms and conditions?
9. How would you handle two users editing the same order form?
10. MVC 5 vs ASP.NET Core MVC — how would you migrate an old MVC 5 app?
11. When would you render with Razor and when with React?
12. How do you do authorization per action and per resource?

---

## 15. EF Core / SQL / transaction / index / migration — Khả năng: Cao (70%) — Đã học ✅ (`notes/03`)

### 15.1 EF Core
- **DbContext** = unit of work + change tracker + connection; Scoped; không thread-safe.
- **Tracking vs AsNoTracking**: tracking để sửa (snapshot → DetectChanges → UPDATE đúng cột đổi); `AsNoTracking` cho đọc. **Projection** `Select` vào DTO là tốt nhất cho đọc.
- **N+1**: lazy loading hoặc query trong vòng lặp → `Include`, projection, batch `Contains`. Phát hiện: đếm số SQL mỗi request (log `Database.Command`, MiniProfiler).
- `AsSplitQuery` khi Include nhiều collection (tích Descartes).
- **Optimistic concurrency**: `[Timestamp] byte[] RowVersion` → `DbUpdateConcurrencyException` → 409/412.
- **Transaction**: `SaveChanges` đã là transaction; tự mở `BeginTransactionAsync` khi nhiều SaveChanges/trộn SQL thô; giữ ngắn, **không gọi HTTP/email trong transaction** (outbox); `EnableRetryOnFailure` → bọc bằng `CreateExecutionStrategy`.
- `ExecuteUpdate/ExecuteDelete` (EF7+): cập nhật hàng loạt không qua tracker (bỏ qua interceptor/audit).
- Interceptor: audit, set session context (Joblogic), soft delete.
- Global query filter: `HasQueryFilter(x => x.TenantId == _tenant.Id && !x.IsDeleted)`.
- Owned types / value object (`Money`), value converter, `HasPrecision`.
- Compiled query, `ToQueryString()` để xem SQL.
- EF Core ≥ 3 throw khi không dịch được LINQ (EF ≤ 2 âm thầm client-eval → kiểm tra khi tiếp quản).
- EF6 vs EF Core: EF6 (`System.Data.Entity`) chạy được trên .NET 8 nhưng không phát triển thêm; EF Core nhanh hơn, có tính năng mới. Joblogic còn EF6.
- **Dapper**: micro-ORM, viết SQL, map nhanh; bẫy: nối chuỗi (SQL injection), quên truyền transaction, `IN` > 2.100 tham số, `nvarchar` vs `varchar` mất index seek.

### 15.2 SQL
- **Normalization** (1NF–3NF) cho master data; **snapshot/denormalize** cho dữ liệu giao dịch đã thoả thuận (QuoteLine lưu giá tại thời điểm báo).
- **JOIN**: INNER, LEFT, RIGHT, FULL, CROSS; **PK**, FK, UNIQUE, CHECK.
- **Index**: clustered (bảng xếp theo key) vs nonclustered (key + clustered key); **composite** theo thứ tự Equality → Sort → Range; **INCLUDE** để covering; FK **không tự có index** (EF migration thì có); index làm ghi chậm hơn.
- Seek vs scan vs key lookup; khi nhiều dòng, scan có thể thắng.
- **Isolation**: Read Uncommitted (dirty read), Read Committed (mặc định SQL Server; Azure SQL bật **RCSI**), Repeatable Read, Serializable, Snapshot. Anomaly: dirty read, non-repeatable read, phantom, lost update. Không nâng cả transaction lên Serializable; khoá đúng dòng (`UPDLOCK, HOLDLOCK`) hoặc atomic UPDATE. **NOLOCK** không dùng cho số liệu tiền.
- **Deadlock**: hai transaction khoá chéo; SQL Server chọn victim (lỗi 1205) → lock theo thứ tự cố định, transaction ngắn, retry.
- **Query chậm**: Query Store (top theo tổng duration) → `sys.dm_exec_requests` (blocking, wait type) → actual execution plan → sửa (index, viết lại, statistics) → đo `SET STATISTICS IO, TIME ON`.
- **Parameter sniffing**: plan cache theo tham số lần đầu → lúc nhanh lúc chậm. Sửa: `OPTION(RECOMPILE)` cho query hiếm, `OPTIMIZE FOR UNKNOWN`, index tốt hơn.
- `CONVERT_IMPLICIT` (sai kiểu tham số) mất seek.
- **Connection pooling**: Dispose = trả về pool (mặc định 100); cạn do không dispose, transaction dài, starvation; `pods × MaxPoolSize ≤ max_connections`.
- Window function (`ROW_NUMBER`, `SUM() OVER`), CTE — hữu ích cho báo cáo.
- Soft delete (`IsDeleted`) + filtered index; archive.
- Partitioning: chỉ nhanh khi lọc theo cột partition; switch/drop thay DELETE lớn.
- Read replica cho báo cáo (độ trễ replication).

### 15.3 Migration an toàn
- **Expand → Migrate (backfill theo lô) → Contract**, mỗi bước một deploy, tương thích ngược (rolling deploy chạy song song bản cũ/mới).
- NOT NULL: thêm NULL → backfill → đổi NOT NULL. Đổi tên cột: thêm cột mới, ghi cả hai, chuyển đọc, xoá cũ. Index lớn: `ONLINE = ON`. Update hàng loạt: chia lô (tránh lock escalation ~5.000 dòng).
- Không `Database.Migrate()` lúc startup ở prod (nhiều instance chạy cùng lúc); dùng **migration bundle** / script idempotent (`dotnet ef migrations script --idempotent`) chạy ở pipeline; Dapper → DbUp/Flyway.
- Backup trước migration lớn; rollback plan.

### 15.4 Câu hỏi luyện
1. Tracking vs AsNoTracking? When would you project to a DTO?
2. What's the N+1 problem? How do you detect it?
3. How does optimistic concurrency work in EF Core? What do you return to the client?
4. When do you need an explicit transaction? What shouldn't happen inside one?
5. A query got 20× slower overnight. What do you do?
6. Explain clustered vs nonclustered index. How do you choose column order in a composite index?
7. What isolation level does SQL Server use by default? What's RCSI?
8. What is parameter sniffing?
9. How do you add a NOT NULL column to a large table without downtime?
10. When would you denormalize? Why snapshot prices on an order?
11. EF Core vs Dapper — when each?
12. What causes connection-pool exhaustion?
13. How do you prevent SQL injection with Dapper?
14. How would you design the schema for quotes, orders and payments?
15. How would you find missing indexes when taking over a database?

---

## 16. Concurrency dữ liệu, idempotency, double submit — Khả năng: Cao (60%) — Đã học ✅

### 16.1 Ý chốt (đây là chỗ Hiệp hay mất điểm)
- **Lost update**: đọc-sửa-ghi trong bộ nhớ app. Chuẩn: **atomic UPDATE** `UPDATE ... SET Qty = Qty - 1 WHERE Id=@id AND Qty >= 1` (kiểm tra rowcount).
- Thứ tự ưu tiên: **atomic UPDATE / UNIQUE constraint → optimistic concurrency (rowversion) → pessimistic lock (UPDLOCK) → distributed lock (Redis)** cuối cùng.
- **Check-then-act** là lỗi: "SELECT xem có chưa, chưa thì INSERT" → hai request cùng qua check. Luôn nói: **"INSERT with a UNIQUE constraint in the same transaction"**; bắt lỗi 2627/2601 → coi là trùng.
- **Idempotency key ≠ concurrency control**: key chống retry của **cùng** yêu cầu; atomic UPDATE chống các yêu cầu **khác nhau** chạy đồng thời.
- Trùng request → **replay response cũ**, không trả lỗi.
- Key chọn đúng độ mịn: transaction reference của provider (không phải roundId); `(playerId, questId, period)` cho thưởng lặp.
- Giữ key: API client ~24h; ledger tiền giữ vĩnh viễn.
- Redis lock không có **fencing token** → process bị dừng lâu vẫn ghi sau khi lock hết hạn → DB phải là trọng tài cuối.
- Double submit trên web: disable nút + PRG (MVC) + Idempotency-Key (API) + UNIQUE ở DB.

### 16.2 Câu mẫu
> The database should decide who wins a race, not application code. For a one-off action like creating an order from a quote, I'd put a unique constraint on the quote ID in the orders table and insert in the same transaction as the rest of the work, so a double click or a retry simply hits the constraint and we return the order that already exists. For updates like stock or capacity, I'd use an atomic conditional UPDATE and check the row count. A distributed lock is my last resort, because it doesn't protect you if a process pauses past the lock's expiry.

### 16.3 Câu hỏi luyện
1. Two requests try to decrement the same inventory at the same time. What happens and how do you fix it?
2. The same webhook arrives twice. How do you make sure the payment is applied once?
3. A background job sometimes processes the same item twice. Why and how do you fix it?
4. The service works with one instance but fails with five. What could be wrong? (in-memory cache/lock/state, scheduled job chạy 5 lần, session cục bộ, file cục bộ)
5. Optimistic vs pessimistic locking — when each?
6. When would you use a distributed lock? What's wrong with Redis locks?
7. Your API receives the same request twice. What do you do?
8. How do you prevent a user from submitting an order twice?

---

## 17. Multi-tenant SaaS — Khả năng: Trung bình–Cao (60%) — Đã học ✅ (`notes/J-multitenant-deep.md`)

### 17.1 Ý chốt
- Mô hình: **Silo** (DB/tenant) – **Bridge** (schema/tenant) – **Pool** (chung bảng, cột TenantId) – **Shard** (pool chia nhiều DB). Trade-off: cô lập/chi phí/vận hành.
- Tenant context lấy từ **token/claim đăng nhập**, không từ tham số client gửi; đi theo mọi message, job, cache key, file path.
- Lớp phòng thủ: middleware resolve tenant → global query filter (EF) hoặc RLS/view (DB) → FK kèm TenantId → cache key có tenant → S3 prefix theo tenant → test với 2 tenant.
- Joblogic: shard theo tenant (ShardKey ở License DB), `SESSION_CONTEXT('TenantId')` đặt mỗi lần mở connection, đọc qua **view `dbo`** lọc tenant, ghi bị **RLS block predicate** chặn, PK/FK `(TenantId, Id)`, Depot là phạm vi con trong tenant.
- Cấu hình theo tenant (thuế, template, quy trình), **feature theo gói** (Joblogic: 60+ AppModule; FeatureManagement + TargetingFilter theo tenant).
- **Noisy neighbor**: đo theo tenant (metric có tag tenant), rate limit theo tenant, tách tenant lớn sang shard riêng, replica cho báo cáo, job nền chia lô theo tenant.
- Migration nhiều shard: expand → deploy → contract theo đợt.
- Job nền: quét tenant hợp lệ → fan-out message theo tenant.
- Di chuyển tenant giữa shard: copy → khoá ghi ngắn → copy phần chênh → đổi mapping → xoá cache mapping mọi instance.

### 17.2 Câu mẫu
> At Joblogic, tenant isolation was enforced in the database, not just in application code. When a connection opens, an interceptor sets the tenant ID in SQL Server's session context; the application reads through views that filter by it, and row-level security block predicates stop writes to another tenant's rows. Primary and foreign keys include the tenant ID, so a job can't point to another tenant's customer. For the Ops Hub I'd at least use an EF Core global query filter plus tenant-aware cache keys and S3 prefixes, and add tests that run with two tenants.

### 17.3 Câu hỏi luyện
1. How would you isolate tenant data? Pros and cons of database-per-tenant vs shared tables?
2. A customer sees another company's order. How do you investigate and prevent it?
3. One big tenant slows everyone down. What do you do?
4. How do you roll out a schema change across all tenants?
5. How do you support per-tenant configuration and features by plan?
6. Where does the tenant ID come from in a request? Why not from the URL?
7. How do background jobs know which tenant they're working for?

---

## 18. Unit test / integration test — Khả năng: Cao (65%) — ❌ chưa ôn, có kinh nghiệm thật

Bằng chứng: PlaySweeps ~200 file test **xUnit + Moq**; Joblogic **MSTest + AutoFixture + AutoMocker** (test audit handler, selling rate, SchedulerController); EIM **Jest** (~3 file — nói ít). Nói đúng tên framework từng nơi.

### 18.1 Kiến thức
- **Unit test**: test một đơn vị logic, cô lập, nhanh, không I/O. **Integration test**: nhiều thành phần thật (DB, HTTP pipeline). **E2E**: qua UI/hệ thống thật.
- **Test pyramid**: nhiều unit (domain, tính tiền, state machine, ngày giờ) → ít integration (`WebApplicationFactory` + DB thật bằng **Testcontainers**) → rất ít E2E (Playwright).
- **Test tốt (FIRST)**: Fast, Independent, Repeatable, Self-validating, Timely. Một hành vi mỗi test; tên `Method_Scenario_ExpectedResult`; Arrange–Act–Assert; không logic phức tạp trong test.
- **Test double**: dummy, stub (trả dữ liệu cố định), fake (implement đơn giản, vd. in-memory), mock (kiểm tra được gọi thế nào), spy.
- **Mock gì**: phụ thuộc ngoài (HTTP, email, clock, queue, payment). **Không mock**: domain object, value object; **không mock `DbContext`/`IQueryable`** để test query (dùng DB thật); EF InMemory provider không giống SQL thật (không transaction, không constraint) → SQLite in-memory hoặc Testcontainers.
- **Thời gian**: `TimeProvider` + `FakeTimeProvider` (.NET 8).
- **Test data builder** / AutoFixture để tạo object; tránh fixture dùng chung bị sửa.
- **Parameterized**: xUnit `[Theory]` + `[InlineData]`/`[MemberData]`; MSTest `[DataRow]`; NUnit `[TestCase]`.
- **Assertion**: FluentAssertions (chú ý license v8) hoặc Shouldly.
- **Test legacy**: characterization test trước, tạo seam, rồi refactor.
- **Coverage**: chỉ là chỉ số phụ; quan trọng là luật nghiệp vụ rủi ro có test. Mutation testing (Stryker) để đo chất lượng test.
- **TDD** (Red–Green–Refactor): dùng khi luật rõ (tính tiền, lịch trả góp).
- **Contract test** cho API giữa FE–BE/partner (Pact) — biết khái niệm.
- **Flaky test**: do thời gian, thứ tự, dữ liệu dùng chung, mạng → cô lập, fake clock, dữ liệu riêng mỗi test.
- Test trong CI: chạy mỗi PR, chặn merge khi fail.

### 18.2 Ví dụ
```csharp
public class BalanceDueTests
{
    [Theory]
    [InlineData(1000.00, 200.00, 0.00, 800.00)]
    [InlineData(1000.00, 1000.00, 0.00, 0.00)]
    [InlineData(1000.00, 1100.00, 100.00, 0.00)] // overpaid then refunded
    public void BalanceDue_NetsPaymentsAndRefunds(decimal total, decimal paid, decimal refunded, decimal expected)
    {
        var order = OrderBuilder.WithTotal(total).Paid(paid).Refunded(refunded).Build();
        order.BalanceDue.Should().Be(expected);
    }

    [Fact]
    public void RtoSchedule_LastInstallmentAbsorbsRounding()
    {
        var schedule = RtoSchedule.Create(total: 1000m, months: 3);
        schedule.Installments.Sum(i => i.Amount).Should().Be(1000m);
        schedule.Installments.Last().Amount.Should().Be(333.34m);
    }
}
```
Integration test API:
```csharp
public class QuotesApiTests(ApiFactory factory) : IClassFixture<ApiFactory>
{
    [Fact]
    public async Task Finalize_Twice_ReturnsConflict()
    {
        var client = factory.CreateClient();
        var id = await factory.SeedDraftQuoteAsync();
        (await client.PostAsync($"/quotes/{id}/finalize", null)).StatusCode.Should().Be(HttpStatusCode.OK);
        (await client.PostAsync($"/quotes/{id}/finalize", null)).StatusCode.Should().Be(HttpStatusCode.Conflict);
    }
}
```

### 18.3 Câu mẫu
> I focus unit tests on business rules where bugs cost money — pricing, balance due, state transitions, date calculations — because those are pure logic and fast to test. For data access and integrations I prefer a few integration tests against a real database rather than mocking EF, since mocked queries give false confidence. At PlaySweeps I wrote unit tests with xUnit and Moq, around two hundred test files across the features I worked on; at Joblogic the team used MSTest with AutoFixture.

### 18.4 Câu hỏi luyện
1. What makes a good unit test?
2. Unit vs integration test? What does your test pyramid look like?
3. What do you mock and what don't you mock?
4. Should you mock DbContext? Is the EF InMemory provider good for tests?
5. How do you test code that depends on the current time?
6. How do you add tests to legacy code with no tests?
7. How do you test a payment webhook handler?
8. What's TDD? Do you use it?
9. Is 100% coverage a good goal?
10. How do you deal with flaky tests?
11. What would you unit test in the quote → order flow?

---

## 19. Frontend (React/TS/JS/HTML/CSS) + hợp đồng FE–BE + UX — Khả năng: Trung bình–Cao (60%)

SA **gốc frontend**: React, TypeScript, HTML5, CSS, UX/UI, Front-end (pass LinkedIn assessment). JD: frontend là điểm cộng. Hiệp có thật: PlaySweeps React 18 + Redux (~340 commit), EIM React + TanStack Query + Ant Design, Altar React 18 + Redux, admin Vue 3 + Pinia, Joblogic Razor + jQuery + Vue nhúng, Next.js storefront.
**Thái độ:** không nói "frontend chỉ là phụ"; thể hiện nghĩ cho người dùng cuối.

### 19.1 JavaScript / TypeScript
- `let`/`const` vs `var` (block scope vs function scope, hoisting); `==` vs `===`; closure; `this`; arrow function.
- **Event loop**: call stack, microtask (Promise) chạy trước macrotask (setTimeout); JS đơn luồng. So với .NET: Node dùng event loop + libuv; .NET dùng thread pool + async I/O — cả hai đều không chặn khi chờ I/O.
- Promise, `async/await`, `Promise.all` vs `allSettled`; xử lý lỗi `try/catch`.
- TypeScript: `interface` vs `type`, union, generic, `unknown` vs `any`, `strict` mode, utility types (`Partial`, `Pick`, `Omit`, `Record`), type narrowing, discriminated union (hợp với ProblemDetails/Result).
- Module ES, bundler (Vite, webpack), tree shaking.

### 19.2 React
- Component, props, state; **hooks**: `useState`, `useEffect` (dependency array, cleanup), `useMemo`, `useCallback`, `useRef`, `useContext`, custom hook.
- Re-render khi state/props đổi; `key` trong list (không dùng index khi list đổi thứ tự); `React.memo`.
- **State**: local state → lift state up → Context → Redux/Zustand cho global UI state. **Server state** khác client state → **TanStack Query** (cache, refetch, invalidate sau mutation, retry, stale time). Redux Toolkit/RTK Query.
- **Form**: React Hook Form + Zod/Yup; hiển thị lỗi theo field từ ProblemDetails.
- **Optimistic update** + rollback khi lỗi.
- Performance: code splitting (`React.lazy`), virtualized list (danh sách lớn như production queue), debounce search, tránh re-render thừa.
- React 18: concurrent rendering, automatic batching, `Suspense`. React 19 / Server Components (biết khái niệm), Next.js SSR/SSG.
- Testing: React Testing Library, Jest/Vitest, Playwright cho E2E.

### 19.3 HTML/CSS/UX
- Semantic HTML (`<button>` không phải `<div onClick>`), **accessibility** (label cho input, alt cho ảnh, keyboard navigation, contrast, ARIA khi cần).
- CSS: box model, flexbox, grid, responsive (media query, mobile-first), specificity; CSS modules / Tailwind / styled-components; design system (Ant Design, MUI).
- UX từ góc backend: **loading / empty / error state**, thông báo lỗi dễ hiểu (không hiện stack), xác nhận hành động nguy hiểm (huỷ đơn), **undo** khi có thể, phân trang/infinite scroll, timezone hiển thị theo cửa hàng, định dạng tiền theo locale (`Intl.NumberFormat`), không cho submit 2 lần.

### 19.4 Hợp đồng FE–BE & bảo mật frontend
- OpenAPI → sinh TypeScript types/client (openapi-typescript, NSwag). DTO ổn định, versioning.
- Validation hai phía: FE để UX nhanh, **BE là nguồn sự thật**.
- **Token**: ưu tiên **HttpOnly + Secure + SameSite cookie** (JS không đọc được → giảm rủi ro XSS lấy token) + CSRF protection; localStorage dễ bị XSS đánh cắp. SPA có thể dùng BFF (backend-for-frontend) giữ token phía server.
- **CORS**: chỉ mở origin cần, không `*` khi có credentials. CORS không phải cơ chế bảo mật cho server, chỉ là chính sách trình duyệt.
- XSS: React tự escape; nguy hiểm `dangerouslySetInnerHTML` → sanitize (DOMPurify); CSP header.
- Thao tác chậm: 202 + poll hoặc SignalR/WebSocket push (trạng thái sinh PDF, cập nhật production board realtime).
- File upload lớn: upload thẳng lên S3 bằng presigned URL, backend chỉ cấp URL + xác nhận.

### 19.5 Razor MVC vs React SPA
| | Razor (server render) | React SPA |
|---|---|---|
| Hợp | Form nội bộ, CRUD, ít tương tác, SEO | Màn hình tương tác cao: production board kéo-thả, lịch giao hàng, cấu hình sản phẩm |
| Ưu | Đơn giản, một codebase, auth cookie sẵn | UX mượt, tách FE/BE, tái sử dụng API cho mobile |
| Nhược | Tương tác phức tạp phải thêm JS | Thêm build pipeline, state, bảo mật token, SEO |
| Thực tế | Joblogic dùng Razor + Vue nhúng cho phần tương tác | PlaySweeps, EIM dùng React |

### 19.6 Câu hỏi luyện
1. How do you manage server state vs UI state in React?
2. When does a React component re-render? How do you avoid unnecessary re-renders?
3. `useEffect` — common mistakes?
4. Where do you store the auth token in a SPA and why?
5. What is CORS? Is it a security feature?
6. How do you prevent XSS in React?
7. How would you build a drag-and-drop production queue that two people may edit at once?
8. How do you show validation errors from the API on a form?
9. How would you design the UI/API around a 10-second PDF generation?
10. When would you choose Razor over React?
11. What makes a good error message for users?
12. How do you make a page accessible?
13. JavaScript event loop vs .NET thread pool?
14. TypeScript `interface` vs `type`? `any` vs `unknown`?
15. How would you display dates and money for stores in different time zones?

---

## 20. CI/CD, deploy, release an toàn — Khả năng: Trung bình–Cao (60%) — ❌ ĐIỂM YẾU

SA tự khai **CI/CD** ở vai trò hiện tại. Kinh nghiệm thật của Hiệp: làm việc **trong** pipeline do DevOps sở hữu; từng **sửa config Jenkins/Helm values**; Joblogic dùng Azure DevOps (PR, nhánh uat) + Sonar. **Không** nhận đã dựng pipeline. (Nếu Hiệp từng tự viết YAML pipeline nào, bổ sung vào đây.)

### 20.1 Khái niệm
- **CI** (Continuous Integration): merge thường xuyên vào nhánh chính, mỗi lần build + test tự động.
- **Continuous Delivery**: luôn ở trạng thái deploy được, bước lên prod bấm tay. **Continuous Deployment**: tự động lên prod khi pass.
- **Artifact**: build **một lần**, promote cùng artifact qua môi trường (dev → staging → prod), không build lại.
- **Environment config** tách khỏi artifact (12-factor): biến môi trường, Secrets Manager/Parameter Store.

### 20.2 Pipeline chuẩn cho .NET trên AWS
1. **PR build**: `dotnet restore` → `dotnet build -c Release` → `dotnet test` (unit + integration với Testcontainers) → `dotnet format --verify-no-changes`, analyzer (warning as error), scan dependency (`dotnet list package --vulnerable`), SonarQube/SAST; **bắt buộc pass mới merge** (branch protection, required review).
2. **Main build**: build Docker image (multi-stage, image runtime nhỏ), tag theo **commit SHA**, đẩy lên **ECR**; tạo migration bundle (`dotnet ef migrations bundle`) hoặc script idempotent.
3. **Deploy dev/staging** tự động: chạy migration (expand) → deploy app (ECS Fargate/Elastic Beanstalk/App Runner) → smoke test.
4. **Deploy prod** (duyệt tay hoặc tự động): migration → rolling hoặc **blue/green** (ECS + CodeDeploy) có health check → theo dõi error rate/latency (CloudWatch alarm) → tự rollback nếu alarm.
5. **Sau deploy**: smoke test, dashboard, thông báo Slack.
- Công cụ: GitHub Actions, AWS CodePipeline/CodeBuild/CodeDeploy, Azure DevOps, Jenkins, GitLab CI — nguyên lý như nhau. IaC: Terraform, AWS CDK, CloudFormation.

Ví dụ GitHub Actions rút gọn (để hiểu cấu trúc, không nói là đã từng viết):
```yaml
on:
  pull_request:
  push: { branches: [main] }
jobs:
  build-test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: actions/setup-dotnet@v4
        with: { dotnet-version: '8.0.x' }
      - run: dotnet restore
      - run: dotnet build -c Release --no-restore
      - run: dotnet test -c Release --no-build
  deploy:
    if: github.ref == 'refs/heads/main'
    needs: build-test
    runs-on: ubuntu-latest
    environment: staging
    steps:
      - run: echo "build image, push to ECR, run migration bundle, update ECS service"
```

### 20.3 Chiến lược phát hành & rollback
- **Rolling**: thay dần instance; bản cũ và mới chạy song song → API + DB phải tương thích ngược.
- **Blue/green**: dựng môi trường mới, chuyển traffic một lần, rollback = chuyển lại.
- **Canary**: chuyển % nhỏ traffic, đo, tăng dần.
- **Feature flag**: deploy code tắt, bật dần theo tenant/user; **tách deploy khỏi release**; rollback = tắt flag. Dọn flag cũ.
- **Rollback có migration**: nhờ **expand/contract**, rollback app không cần rollback DB (schema mới vẫn tương thích bản cũ). Không viết migration phá huỷ (drop cột) cùng release dùng nó.
- **Hotfix**: nhánh hotfix từ tag prod hoặc fix trên main + cherry-pick; vẫn đi qua pipeline (nhanh hơn, không bỏ test).
- **Zero-downtime**: graceful shutdown (xử lý xong request đang chạy, `stoppingToken`), readiness probe, connection draining ở load balancer.

### 20.4 Chất lượng trong pipeline
- Unit + integration test, coverage gate hợp lý, static analysis, secret scanning, dependency scanning, container image scanning (ECR scan).
- Code review bắt buộc, branch protection.
- DORA metrics: deployment frequency, lead time for changes, change failure rate, time to restore.

### 20.5 Câu trả lời trung thực mẫu
> I haven't owned a pipeline end to end; in my previous teams DevOps owned it and I worked inside it: I've edited Jenkins and Helm configuration for my services, and I own the parts a developer should — tests that run in the pipeline, backward-compatible migrations, feature flags, and checking metrics after a release. If I set one up for the Ops Hub, I'd build one image per commit, promote the same image through environments, run migrations as a separate expand/contract step, and keep rollback to a single action.

### 20.6 Câu hỏi luyện
1. Walk me through the pipeline from a merged PR to production.
2. Continuous delivery vs continuous deployment?
3. Why build once and promote the same artifact?
4. How do you run database migrations in a pipeline? Why not at app startup?
5. A release breaks production and included a migration. How do you roll back?
6. Blue/green vs rolling vs canary?
7. What's a feature flag? How does it help release safely?
8. What checks should block a merge?
9. How do you manage secrets in CI/CD?
10. How do you ship a hotfix quickly without skipping safety?
11. What have you done with CI/CD yourself? (trả lời trung thực 20.5)
12. How do you achieve zero-downtime deployment?
13. What's infrastructure as code? Have you used it?

---

## 21. AWS (map từ Azure) — Khả năng: Trung bình–Cao (60%)

SA có AWS (AgilityIO), JD ghi AWS/cloud. Kinh nghiệm thật: Azure (PlaySweeps, Joblogic); AWS **KMS, S3, SES** trên project Go (Altar).

### 21.1 Bảng map
| Nhu cầu | AWS | Azure (đã dùng) | Ghi chú |
|---|---|---|---|
| Chạy web app container | **ECS Fargate** / App Runner / EKS | App Service / AKS | Fargate không quản lý server |
| Chạy web app PaaS | Elastic Beanstalk | App Service | |
| Function | **Lambda** (.NET 8 runtime, giới hạn 15 phút) | Azure Functions | Cold start |
| Queue | **SQS** Standard (at-least-once, không đảm bảo thứ tự) / **FIFO** (thứ tự theo message group, dedup 5 phút) | Service Bus queue (session) | Visibility timeout, DLQ (redrive policy) |
| Pub/sub | **SNS** (+ SQS fan-out) / **EventBridge** (rule, schedule) | Service Bus topic, Event Grid | |
| DB quan hệ | **RDS** SQL Server / PostgreSQL / **Aurora** | Azure SQL | Multi-AZ, read replica, automated backup, PITR |
| NoSQL | DynamoDB / DocumentDB | Cosmos DB / Mongo | |
| Cache | ElastiCache (Redis/Valkey) | Azure Cache for Redis | |
| File | **S3** + presigned URL, lifecycle, versioning, SSE-KMS | Blob + SAS | Bucket private, Block Public Access |
| Secret | **Secrets Manager** (xoay vòng) / SSM **Parameter Store** / **KMS** (khoá mã hoá) | Key Vault | |
| Quyền | **IAM role** (task role cho ECS, execution role cho Lambda), least privilege | Managed Identity + RBAC | Không để access key trong code |
| Monitoring | **CloudWatch** Logs/Metrics/Alarms + **X-Ray** (hoặc OpenTelemetry → ADOT) | App Insights | |
| Email / SMS | **SES** / SNS SMS / Pinpoint | SendGrid / Twilio | |
| API gateway / LB | API Gateway, **ALB**, CloudFront (CDN), WAF | API Management, Front Door, App Gateway | |
| Lịch chạy job | EventBridge Scheduler | Timer trigger | |
| Mạng | VPC, subnet public/private, security group, NAT gateway | VNet, NSG | DB ở private subnet |
| CI/CD | CodePipeline / CodeBuild / CodeDeploy, ECR | Azure DevOps, ACR | |
| IaC | CloudFormation / CDK / Terraform | ARM / Bicep / Terraform | |
| Auth người dùng | Cognito | Entra ID / B2C | |
| Search | OpenSearch | Azure AI Search | |
| Cấu hình động / feature flag | AppConfig | App Configuration | |

### 21.2 Kiến trúc tham khảo Ops Hub trên AWS
- Route 53 → CloudFront (static React) + **ALB** → **ECS Fargate** (ASP.NET Core API/MVC, ≥ 2 task ở 2 AZ, auto scaling theo CPU/request).
- **RDS SQL Server Multi-AZ** (+ read replica cho báo cáo), **ElastiCache Redis** (cache, rate limit).
- **S3** (PDF hợp đồng, ảnh giao hàng; private, presigned URL, versioning, lifecycle).
- **SQS** (+ DLQ) cho việc nền: sinh PDF, gửi email/SMS, đồng bộ bên thứ ba; worker là ECS service hoặc Lambda.
- **SNS/EventBridge** cho event fan-out; EventBridge Scheduler cho job định kỳ (nhắc thanh toán, hết hạn quote).
- **Secrets Manager** cho connection string/API key; **IAM task role**; KMS mã hoá.
- **CloudWatch** logs + alarms, **X-Ray**/OpenTelemetry tracing.
- SES email, SNS/Pinpoint SMS.
- Webhook từ bên thứ ba: API Gateway hoặc ALB → endpoint → ghi SQS → xử lý async.

### 21.3 Kiến thức hay hỏi
- **SQS visibility timeout**: message bị ẩn khi đang xử lý; quá hạn chưa xoá → hiện lại → xử lý lần 2 → consumer idempotent; nhận quá `maxReceiveCount` → DLQ.
- **SQS vs SNS vs EventBridge**: queue (1 consumer group, kéo) vs pub/sub (đẩy tới nhiều subscriber) vs event bus có rule lọc/định tuyến + schedule.
- **Lambda vs ECS**: Lambda cho việc ngắn, theo sự kiện, tải không đều (≤ 15 phút, cold start); ECS cho API chạy liên tục, việc dài, cần kiểm soát runtime.
- **S3 presigned URL**: URL có chữ ký, hết hạn ngắn, cấp quyền GET/PUT một object mà không lộ credential; backend kiểm tra quyền trước khi cấp.
- **IAM**: user (người) vs role (service đảm nhận, credential tạm thời); policy least privilege; không hard-code key.
- **RDS Multi-AZ** (sẵn sàng, failover tự động) vs **read replica** (scale đọc, có độ trễ).
- **Availability Zone vs Region**.
- Chi phí: NAT gateway, data transfer, CloudWatch logs có thể tốn; Fargate Spot/Savings Plans.
- .NET SDK: `AWSSDK.S3`, `AWSSDK.SQS`, `Amazon.Extensions.Configuration.SystemsManager`, `AWS.Logger`/Serilog sink, `Amazon.Lambda.AspNetCoreServer`.

### 21.4 Câu mẫu
> Most of my production cloud work was on Azure, and I've used AWS directly for KMS, S3 and SES on a Go project. The concepts map closely — Service Bus to SQS and SNS, Functions to Lambda, Key Vault to Secrets Manager, App Insights to CloudWatch and X-Ray — so I'd expect to be productive quickly and I'd learn the team's specific setup first.

### 21.5 Câu hỏi luyện
1. How would you host this .NET app on AWS?
2. SQS vs SNS vs EventBridge?
3. What's the SQS visibility timeout? What happens if processing takes longer?
4. Lambda or ECS for the PDF generator? For the main API?
5. How do you let a user download a private file from S3 securely?
6. Where do secrets live? How does the app get AWS credentials?
7. Multi-AZ vs read replica?
8. How would you monitor the system on AWS?
9. What AWS services have you actually used?
10. How would you make the system survive an AZ failure?
11. How would you receive webhooks reliably on AWS?

---

## 22. Tích hợp bên thứ ba & resilience — Khả năng: Trung bình (55%)

Ops Hub có nhiều tích hợp (payment, thuế, RTO provider, configurator, SMS/email). SA từ Urbanise (tích hợp ngân hàng) có thể hỏi.

### 22.1 Webhook vào
1. **Xác thực chữ ký** (HMAC, so sánh constant-time, kiểm timestamp chống replay) — giống Pragmatic hash.
2. **Lưu raw event** (bảng inbox, UNIQUE event id).
3. **Trả 2xx nhanh** (provider có timeout ngắn, sẽ retry).
4. Xử lý **async** (queue), **idempotent** theo event id; xử lý được **sai thứ tự** (kiểm tra version/timestamp, trạng thái hiện tại).
5. Màn hình/bảng **integration errors** để vận hành xem và retry tay (mapping SKU sai…).
6. Job **đối soát** định kỳ với API provider (Joblogic: đối soát Stripe hằng ngày) để bắt event bị mất.

### 22.2 Gọi ra ngoài
- **Timeout** cho mọi lời gọi (mặc định HttpClient 100s là quá dài).
- **Retry** có exponential backoff + jitter, **chỉ cho lỗi tạm thời** (5xx, 408, 429, timeout) và **chỉ khi thao tác idempotent** (hoặc có idempotency key của provider).
- **Circuit breaker**: lỗi liên tục → mở mạch, fail nhanh, thử lại sau → bảo vệ hệ thống mình và provider.
- **Bulkhead**: giới hạn số lời gọi đồng thời tới một provider để không ăn hết thread/connection.
- **Fallback / graceful degradation**: API thuế sập → dùng mức thuế cache gần nhất và đánh dấu "cần xác nhận"; RTO provider sập → lưu yêu cầu "pending", xử lý lại sau, báo người dùng.
- .NET: `IHttpClientFactory` + `Microsoft.Extensions.Http.Resilience` (`AddStandardResilienceHandler`) / Polly v8.
- **Anti-corruption layer**: adapter dịch model ngoài → model nội bộ; lỗi provider → lỗi nghiệp vụ rõ.
- Log + correlation id + metric theo provider (latency, error rate).
- Rate limit của provider → hàng đợi, batch.
- Secret của provider ở Secrets Manager, xoay vòng.

### 22.3 Câu mẫu
> For outgoing calls I always set a timeout, retry only transient errors with exponential backoff and jitter, and only when the operation is idempotent or I can pass the provider an idempotency key. A circuit breaker stops us from hammering a provider that's down. For the user, the request isn't lost: we save it as pending and process it when the provider recovers. For incoming webhooks, I verify the signature, store the raw event with a unique event ID, return 200 quickly and process it asynchronously, so a retried or out-of-order webhook can't apply a payment twice.

### 22.4 Câu hỏi luyện
1. The RTO provider API is down for 30 minutes during business hours. What does the user see? What happens to pending requests?
2. An external API is occasionally slow. How do you protect your system?
3. Explain retry, timeout, circuit breaker and bulkhead.
4. Why must every external HTTP call have a timeout?
5. When is retrying dangerous?
6. How do you receive webhooks reliably? What if they arrive out of order?
7. How do you know if you missed a webhook?
8. How do you integrate a provider whose data model doesn't match yours?
9. How do you test an integration with a third-party API?
10. What is graceful degradation? Give an example here.

---

## 23. Messaging, background job, outbox, caching — Khả năng: Trung bình (50%)

### 23.1 Messaging
- **Vì sao queue**: tách tải (san đỉnh), việc chậm ra khỏi request, retry, tách hệ thống.
- **At-least-once** (phổ biến) → message có thể đến 2 lần → **consumer idempotent**. At-most-once (có thể mất). Exactly-once thực tế = at-least-once + idempotent.
- **DLQ**: message lỗi quá N lần → hàng chờ chết → alert, xem, sửa, đẩy lại.
- **Competing consumers** (nhiều worker chia việc một queue) vs **pub/sub** (mỗi subscriber nhận một bản).
- **Thứ tự**: Service Bus session / SQS FIFO message group theo key (vd. orderId) — một consumer mỗi lúc cho cùng key. SessionId **không** chống trùng.
- **Poison message**: luôn lỗi → DLQ, không retry vô hạn.
- **Transactional Outbox**: ghi dữ liệu nghiệp vụ + bản ghi outbox **trong cùng transaction**; relay đọc outbox gửi đi (at-least-once) → consumer idempotent. Giải quyết "lưu DB xong, gửi message thì crash" (hoặc ngược lại). **Không phải Mediator** (MediatR là in-process).
- **Inbox**: bên nhận lưu message id đã xử lý (UNIQUE) để chống trùng.
- **Saga**: chuỗi transaction cục bộ + **compensation** khi một bước lỗi (orchestration vs choreography). Ví dụ: tạo order → giữ inventory → thu deposit; thu tiền lỗi → nhả inventory, huỷ order.
- **Distributed transaction (2PC)**: tránh trong microservices (khoá lâu, phụ thuộc coordinator) → outbox + saga.
- Thư viện .NET: MassTransit, NServiceBus, Wolverine, Rebus.

### 23.2 Background job trong ASP.NET Core
- `BackgroundService` + `Channel<T>` cho việc nội bộ đơn giản (mất khi restart nếu không bền).
- Bền / định kỳ: **Hangfire**, Quartz.NET, hoặc queue (SQS) + worker, EventBridge Scheduler.
- Mỗi lần xử lý tạo **scope** mới (DbContext Scoped).
- Nhiều instance → job định kỳ chạy N lần → khoá phân tán/leader election hoặc scheduler trung tâm; job **idempotent**.
- Graceful shutdown qua `stoppingToken`.

### 23.3 Caching
- **Vì sao**: giảm latency, giảm tải DB/API ngoài. **Cái giá**: dữ liệu cũ, invalidation khó, bộ nhớ.
- **Cache-aside** (đọc cache → miss thì đọc DB → ghi cache) là phổ biến; write-through; TTL.
- **Cục bộ** `IMemoryCache` (nhanh, mỗi instance riêng) vs **phân tán** Redis/`IDistributedCache` (chung) vs **HybridCache** (.NET 9: L1 + L2 + chống stampede).
- **Cache stampede**: key hết hạn, ngàn request cùng đi DB → lock theo key/single-flight, TTL có jitter, refresh trước hạn.
- **Invalidation**: xoá key khi dữ liệu đổi (event), hoặc TTL ngắn; nhiều instance cục bộ → pub/sub để xoá.
- **Key có tenant** (`tenant:{id}:taxrate:{zip}`).
- **Không cache**: số dư, trạng thái thanh toán cần chính xác; dữ liệu nhạy cảm không mã hoá.
- Cache nên cho Ops Hub: bảng giá/catalog, mức thuế theo zip (TTL), cấu hình tenant, template.
- HTTP caching: `Cache-Control`, ETag/304, CDN cho static.

### 23.4 Câu hỏi luyện
1. Why use a message queue? What problems does it introduce?
2. What's at-least-once delivery? How do you handle duplicates?
3. What's a dead-letter queue? What do you do with messages in it?
4. Explain the Outbox pattern. What problem does it solve?
5. Explain the Saga pattern with an order example.
6. Competing consumers vs pub/sub?
7. How do you keep message ordering per order?
8. How would you implement a background worker in ASP.NET Core?
9. A scheduled job runs on every instance. How do you make it run once?
10. How would you cache data in a multi-instance API?
11. What's a cache stampede and how do you prevent it?
12. What would you cache in the Ops Hub, and what would you never cache?

---

## 24. Security — Khả năng: Trung bình (50%) — ❌ chưa học (Buổi 7)

### 24.1 OWASP API Top 10 (2023) — nói được 5–6 cái với ví dụ Ops Hub
1. **Broken Object Level Authorization (BOLA/IDOR)**: `GET /orders/123` không kiểm tra order thuộc tenant/store của user → **kiểm tra quyền theo resource** mọi lần, không chỉ đăng nhập. Rủi ro số 1 của SaaS multi-tenant.
2. **Broken Authentication**: token yếu, không hết hạn, không rate limit login → MFA, khoá tạm/exponential backoff (PlaySweeps).
3. **Broken Object Property Level Authorization**: lộ field nhạy cảm trong response / cho sửa field không được phép (over-posting) → DTO riêng.
4. **Unrestricted Resource Consumption**: không giới hạn page size, upload, rate → limit.
5. **Broken Function Level Authorization**: user thường gọi được endpoint admin → policy theo role/permission.
6. **Unrestricted access to sensitive business flows**: bot spam đặt hàng/quote → rate limit, CAPTCHA.
7. **SSRF**: server fetch URL do user gửi (vd. ảnh từ URL) → whitelist.
8. **Security misconfiguration**: CORS `*`, lỗi lộ stack trace, header bảo mật thiếu.
9. **Improper inventory management**: API cũ/không tài liệu vẫn chạy.
10. **Unsafe consumption of APIs**: tin dữ liệu từ bên thứ ba mà không validate.
Thêm (web): **SQL injection** (luôn parameterize; Dapper `@param`; không nối chuỗi), **XSS** (encode output, sanitize rich text, CSP), **CSRF** (anti-forgery token với cookie auth, SameSite).

### 24.2 AuthN / AuthZ
- **Authentication** = bạn là ai; **Authorization** = bạn được làm gì. 401 vs 403.
- **Cookie** (server-side session/ticket, hợp MVC, cần CSRF protection) vs **JWT bearer** (stateless, hợp API/mobile; khó thu hồi → hết hạn ngắn + refresh token xoay vòng; không lưu dữ liệu nhạy cảm trong payload vì chỉ base64).
- **OAuth 2.0** (uỷ quyền) / **OpenID Connect** (đăng nhập, id token); Authorization Code + PKCE cho SPA/mobile.
- ASP.NET Core: `[Authorize]`, **policy-based** (`RequireClaim`, requirement + handler), **resource-based** (`IAuthorizationService.AuthorizeAsync(user, order, "CanEdit")`).
- **RBAC** (role) vs permission chi tiết (Joblogic: permission mapping) vs ABAC (thuộc tính: store, region).
- Multi-tenant: tenant từ claim, không từ request.

### 24.3 Lưu password & dữ liệu nhạy cảm
- Password: **hash chậm có salt** — Argon2id, bcrypt, PBKDF2 (ASP.NET Core Identity `PasswordHasher` dùng PBKDF2). Không MD5/SHA256 thuần, không mã hoá hai chiều.
- Dữ liệu nhạy cảm (SSN, thông tin tín dụng của khách RTO): mã hoá at rest (KMS, TDE, Always Encrypted), in transit (TLS), **không log**, mask khi hiển thị, giới hạn quyền xem, giữ tối thiểu. Thẻ thanh toán → để provider giữ (tokenization), mình không lưu số thẻ (PCI DSS).
- Secret: không trong code/git; Secrets Manager; xoay vòng; secret scanning.

### 24.4 Bảo vệ API khỏi lạm dụng
- Rate limiting theo user/IP/API key/tenant (fixed/sliding window, token bucket) ở gateway hoặc app (.NET `AddRateLimiter`), lưu counter ở Redis khi nhiều instance; trả 429 + `Retry-After`.
- Exponential backoff cho login/OTP (PlaySweeps), CAPTCHA, WAF, giới hạn kích thước request/page size, timeout.

### 24.5 File upload
Kiểm tra loại file (magic bytes, không tin extension), giới hạn kích thước, quét virus, lưu S3 private với tên ngẫu nhiên, không thực thi, presigned URL để tải.

### 24.6 Câu hỏi luyện
1. What are the most common security risks in a backend API? Give examples here.
2. Authentication vs authorization?
3. How do you stop a user from seeing another company's order? (BOLA)
4. Cookie vs JWT? How do you revoke a JWT?
5. How should passwords be stored?
6. How do you prevent SQL injection, XSS and CSRF?
7. How do you protect sensitive customer data (SSN, credit information)?
8. How do you protect a public API from abuse?
9. How do you handle file uploads securely?
10. Where do you store secrets?

---

## 25. Observability, debug sự cố, performance — Khả năng: Trung bình (50%)

### 25.1 Ba trụ cột
- **Logs**: sự kiện rời rạc, structured (JSON, template `{OrderId}`), có correlation/trace id, tenant id, user id; **không log** secret/PII. Mức: Debug/Info/Warning/Error/Critical.
- **Metrics**: số liệu tổng hợp theo thời gian (request rate, error rate, latency p50/p95/p99, queue length, CPU, memory, thread pool). **RED** (Rate, Errors, Duration) cho service; **USE** (Utilization, Saturation, Errors) cho tài nguyên.
- **Traces**: đường đi của một request qua nhiều service (span); W3C `traceparent`; **OpenTelemetry**.
- Công cụ đã dùng: **Application Insights, Grafana Loki, Splunk** (PlaySweeps); AWS: CloudWatch + X-Ray.
- **Alert** theo triệu chứng người dùng (error rate, latency SLO), không theo mọi thứ; runbook đi kèm.
- **SLI/SLO/SLA**: chỉ số / mục tiêu nội bộ / cam kết hợp đồng.

### 25.2 Quy trình điều tra sự cố (nói theo khung)
1. **Tác động**: ai bị, bao nhiêu, từ khi nào (dashboard, alert). Có cần giảm tác động ngay (rollback, tắt feature flag, scale)?
2. **Thay đổi gần đây**: deploy, config, migration, traffic, provider.
3. **Khoanh vùng**: endpoint nào, tenant nào, instance nào; trace một request chậm.
4. **Xác nhận nguyên nhân** bằng dữ liệu (log, metric, query plan, dump).
5. **Xử lý tạm** → **xử lý gốc** → **phòng ngừa** (test, alert, runbook) → postmortem không đổ lỗi.

### 25.3 Tình huống kinh điển
| Tình huống | Hướng điều tra |
|---|---|
| API đột nhiên chậm | Trace → thời gian ở DB/HTTP ngoài/app? DB: Query Store, blocking, plan đổi (parameter sniffing), statistics; app: thread pool starvation (`dotnet-counters`), GC; ngoài: latency provider |
| Prod 10s, local 500ms | Khối lượng dữ liệu khác (index, plan), mạng (DB khác region), cấu hình (log level, pool), tải đồng thời, cold start, provider thật chậm |
| CPU cao | `dotnet-counters` → `dotnet-trace` (flame graph): vòng lặp nóng, regex, serialize lớn, GC nhiều (cấp phát nhiều), lock contention |
| Memory tăng mãi | `dotnet-counters` (gc-heap-size, gen2) → `dotnet-gcdump`/`dotnet-dump` so 2 thời điểm: cache không giới hạn, static list, event handler, captive DbContext |
| Latency cao, CPU thấp | **Thread-pool starvation** (`.Result`) hoặc chờ I/O/lock/connection pool |
| Lỗi chỉ ở một tenant | Dữ liệu đặc biệt, cấu hình tenant, dữ liệu lớn (noisy neighbor) |
| Không tái hiện local | Log/trace theo correlation id, dựng lại hành trình (PlaySweeps: Splunk BI event), dữ liệu prod (ẩn danh), feature flag/cấu hình khác |
| Trả về bản ghi trùng | JOIN nhân dòng, phân trang offset không ổn định (sort không xác định), retry tạo trùng (thiếu UNIQUE) |

### 25.4 Performance
- Đo trước khi tối ưu (BenchmarkDotNet cho code, load test k6/JMeter cho API).
- Thứ tự hay gặp: query/index → N+1 → payload lớn (projection, phân trang, nén) → cache → async/parallel hợp lý → scale.
- Response compression, `AsNoTracking`, keyset pagination, tránh `ToList()` sớm, stream file lớn.

### 25.5 Câu hỏi luyện
1. What should a backend service log? What should it never log?
2. Logs vs metrics vs traces?
3. An API suddenly becomes slow. Walk me through your investigation.
4. An endpoint takes 10 s in production but 500 ms locally. Why?
5. CPU is high on a .NET service. What do you check?
6. Memory keeps growing. How do you find the leak?
7. How would you make the Ops Hub observable enough to debug an incident?
8. Tell me about an incident you handled on call.
9. What do you alert on?

---

## 26. System design nhỏ — Khả năng: Trung bình (40%)

Khung 45 phút (rút gọn 15–20 phút nếu hỏi trong vòng tech):
1. **Làm rõ yêu cầu** (chức năng + phi chức năng: số tenant, số đơn/ngày, độ trễ, độ chính xác tiền).
2. **Ước lượng** con số (vd. 500 công ty × 20 đơn/ngày = 10k đơn/ngày ≈ 0,1 đơn/giây trung bình → tải thấp, rủi ro là **đúng** chứ không phải **nhanh**).
3. **API + mô hình dữ liệu**.
4. **Kiến trúc** (sơ đồ), luồng chính.
5. **Điểm khó**: concurrency, idempotency, thời gian, tiền, lỗi tích hợp.
6. **Vận hành**: monitor, scale, bảo mật, test.
7. **Trade-off** và cái sẽ làm sau.

### 26.1 Đề 1: Lên lịch giao hàng (delivery scheduling)
- Yêu cầu: chọn ngày giao, tài xế/xe, tối đa N đơn/xe/ngày, vùng giao, thông báo khách, driver app xác nhận.
- Dữ liệu: `Delivery(OrderId UNIQUE, Date date, StoreTimeZone, TruckId, DriverId, Status, Window)`, `TruckDayCapacity(TruckId, Date, Booked, Max)`.
- Chống overbook: `UPDATE TruckDayCapacity SET Booked = Booked + 1 WHERE TruckId=@t AND Date=@d AND Booked < Max` (rowcount = 0 → hết chỗ), cùng transaction với tạo Delivery.
- Đổi lịch: giải phóng chỗ cũ + giữ chỗ mới trong một transaction; event → push driver app + SMS khách (outbox).
- Thời gian: `date` + timezone cửa hàng; DST.
- Driver app offline: version số cho delivery, đồng bộ lại, xung đột → văn phòng thắng + báo tài xế.

### 26.2 Đề 2: Lịch trả góp RTO
- Input: tổng, số kỳ, phí ban đầu, ngày bắt đầu, provider.
- Sinh lịch: chia đều làm tròn 2 số, **kỳ cuối bù**; ngày đến hạn theo lịch (ngày 31 → cuối tháng); lưu snapshot lịch trong contract.
- Strategy theo provider; provider có thể là nguồn sự thật → mình chỉ lưu bản sao + đối soát.
- Thanh toán từng kỳ qua webhook → ledger, idempotent; trễ hạn → job nhắc (EventBridge Scheduler), phí trễ theo luật provider.
- Test: tổng = hợp đồng, tháng 2, năm nhuận, DST không ảnh hưởng ngày lịch.

### 26.3 Đề 3: Sinh tài liệu PDF (quote/contract/invoice)
- API: `POST /orders/{id}/documents` → 202 + job id; `GET /documents/{id}` → trạng thái + presigned URL.
- Worker (SQS → ECS/Lambda): lấy document model đã tính (domain lo nghiệp vụ), chọn template tenant → fallback hệ thống, render (QuestPDF/HTML→PDF), lưu S3 (`tenant/{id}/orders/{id}/...`), cập nhật trạng thái.
- Cache theo checksum dữ liệu + template version; tài liệu đã ký bất biến (hash).
- Lỗi ký tự đặc biệt: escape, font Unicode; test với dữ liệu xấu.
- Scale: nhiều worker, giới hạn đồng thời; DLQ cho job lỗi.

### 26.4 Đề 4: Notification (email/SMS khi trạng thái đơn đổi)
- Domain event (OrderScheduled, OrderDelivered) → outbox → queue → notification service → chọn kênh theo cấu hình tenant + opt-in khách → template → SES/SNS/Twilio.
- Idempotent theo (eventId, recipient, channel); retry backoff; DLQ; log trạng thái gửi (delivered/bounced).
- Giờ yên lặng theo timezone khách; rate limit theo provider.

### 26.5 Đề 5: Payment API / ghi nhận thanh toán
- `POST /orders/{id}/payments` với Idempotency-Key → tạo payment intent ở provider → webhook xác nhận → ledger → cập nhật balance due.
- Không tin client; số tiền tính từ server; trạng thái Pending → Succeeded/Failed; đối soát hằng ngày.
- Chất liệu thật: Pragmatic wallet, Nexus, Stripe ở Joblogic Payment service.

### 26.6 Đề khác trong question bank (biết khung)
Rate limiter đa instance (Redis sliding window/token bucket, Lua script atomic), order processing, file upload service (presigned PUT, quét virus, metadata), URL shortener (ít liên quan).

### 26.7 Câu hỏi luyện
1. Design delivery scheduling with truck capacity limits.
2. Design an RTO payment schedule and payment tracking.
3. Design PDF document generation for quotes and contracts.
4. Design notifications when an order's status changes.
5. Design a payment API.
6. Design a rate limiter for a multi-instance API.
7. How would you design the system for 10× more companies?

---

## 27. Git — Khả năng: Trung bình (40%) — ❌ dễ, 15 phút

- **Workflow**: feature branch → PR → review → merge vào main; trunk-based (nhánh ngắn, feature flag) vs GitFlow (develop/release/hotfix). Joblogic: Azure DevOps PR + nhánh uat; PlaySweeps: review chéo PR.
- **merge vs rebase**: merge giữ lịch sử thật (merge commit); rebase viết lại commit lên đầu nhánh mới → lịch sử thẳng. **Không rebase/force-push nhánh chung.** `--force-with-lease` an toàn hơn `--force` trên nhánh của mình.
- **Squash merge**: gộp PR thành 1 commit trên main.
- **revert vs reset**: `revert` tạo commit đảo ngược (an toàn cho nhánh đã push/prod); `reset` dời con trỏ (chỉ dùng local). `reset --soft/--mixed/--hard`.
- **cherry-pick**: lấy một commit sang nhánh khác (hotfix sang release branch).
- **Conflict**: hiểu cả hai thay đổi, hỏi tác giả nếu cần, chạy test sau khi giải.
- `git stash`, `git bisect` (tìm commit gây lỗi bằng nhị phân), `git blame` (hiểu ngữ cảnh, không để đổ lỗi), `git reflog` (cứu commit "mất"), tag cho release.
- Commit message rõ (imperative, giải thích vì sao), commit nhỏ có ý nghĩa; Conventional Commits.
- `.gitignore`, không commit secret (nếu lỡ: xoay secret ngay, xoá lịch sử là phụ).
- Branch protection, required reviewers, CI pass.

Câu hỏi luyện:
1. Merge vs rebase — when each?
2. How do you undo a commit that's already in production?
3. How do you ship a hotfix to a release branch?
4. You committed a secret. What do you do?
5. How do you find which commit introduced a bug? (`git bisect`)
6. What branching strategy do you prefer and why?
7. How do you resolve a conflict in a file you don't own?

---

## 28. Agile/Scrum, estimate, làm việc remote với Mỹ — Khả năng: Trung bình (55%)

- **Scrum**: sprint (1–2 tuần), sprint planning, daily stand-up (đã làm gì, sẽ làm gì, vướng gì), sprint review/demo, retrospective, backlog refinement. Vai trò: PO (giá trị, ưu tiên), Scrum Master (quy trình), Dev team (cách làm).
- **Kanban**: luồng liên tục, giới hạn WIP — hợp team vận hành/bảo trì.
- **User story** "As a [role], I want [x] so that [y]" + **acceptance criteria** (Given/When/Then); **INVEST**.
- **Estimate**: story point (độ phức tạp tương đối, planning poker) vs giờ; velocity; nêu giả định, chia nhỏ, spike cho việc chưa rõ.
- **Definition of Ready / Done**: DoD = code + test + review + deploy staging + tài liệu/monitoring.
- **Tech debt**: ghi ticket, dành % mỗi sprint, gắn với rủi ro/tốc độ.
- PlaySweeps: Scrum + Jira (~354 ticket WIN-xxxx).
- **Remote với Mỹ** (chênh ~11–15 giờ với Việt Nam tuỳ múi giờ và DST): giao tiếp **async** viết rõ (bối cảnh, câu hỏi cụ thể, phương án đề xuất để họ chỉ cần chọn), gom câu hỏi trước giờ trùng nhau, ghi lại quyết định, demo bằng video/ảnh, không để bị chặn: làm phần khác trong lúc chờ, nêu giả định rõ.
- Câu mẫu:
> With a 12-hour gap, I try to make every message self-contained: the context, the specific question, and my proposed option, so the PM can just say yes or pick another option when they wake up. While I wait, I keep working on parts that don't depend on the answer, and I write down my assumption so it's easy to adjust. At PlaySweeps I worked daily with the PLAYSTUDIOS team in the US over Slack and joined technical design meetings in the overlap hours.

Câu hỏi luyện:
1. Describe your Scrum process in your last team.
2. How do you estimate a story? What if the estimate is wrong?
3. What's your Definition of Done?
4. How do you handle tech debt in sprints?
5. How do you work with a team 12 hours behind?
6. What makes a good user story / acceptance criteria?
7. What do you do in a retrospective when something went badly?

---

## 29. Câu hỏi ngược cho interviewer — Khả năng được mời hỏi: Rất cao (95%)

Chọn 2–3 câu mỗi người, đừng hỏi những gì JD đã ghi.

Cho SA:
1. What does the current architecture of the Ops Hub look like — monolith or services, MVC or a React front end — and which parts are you most concerned about after the handover from the US partner?
2. What does the CI/CD and release process look like today, and what would you most like to improve first?
3. Who owns the API contract between the front end and the back end, and how are changes coordinated?
4. Is the plan to keep building on the existing codebase or to gradually modernise parts of it?
5. How is testing set up today, and what level of coverage do the critical money flows have?
6. What would you most like a new developer to improve in the codebase in the first three months?
7. How are architecture decisions made between Seadev and the US partner?

Cho PO:
1. What are the biggest pain points your customers report in the Ops Hub right now?
2. How do you and the developers work together — how early am I involved in shaping a feature?
3. What would a successful first three months look like for this role?
4. How do you measure whether a feature was successful?
5. What's on the roadmap for the next six months?

Gắn core value (dùng được cho cả SA/PO):
- How do 1% improvements usually happen in this team — can a developer just propose a small refactor or process change?
- When something goes wrong in production, how does the team handle it — what does "coach, not police" look like in practice?

Chung (cuối buổi):
- What are the next steps in the process?
- Is there anything in my background you'd like me to clarify?

Tránh: lương/phúc lợi ở vòng tech (để HR), câu hỏi lộ ra là đã đọc release notes nội bộ của ShedPro, câu hỏi về hồ sơ cá nhân interviewer.

---

## 30. Checklist trước giờ phỏng vấn + lỗi hay mắc

### 30.1 Một ngày trước
- [ ] Đọc lại section 1, 2 (pitch, câu chuyện), nói to 2 lần.
- [ ] Điền hết các chỗ **[Hiệp điền]** (incident on-call, Socure chi tiết, lương, bất đồng, sai lầm).
- [ ] Đọc bảng 0.2, xem lướt "Câu hỏi luyện" của mọi section.
- [ ] Chuẩn bị giấy/bảng trắng (vẽ kiến trúc), nước, tai nghe; test mic/camera nếu online.
- [ ] Mở sẵn CV (bản đã gửi) để khớp chính xác.

### 30.2 Lỗi Hiệp hay mắc — tự nhắc
- Check-then-act → luôn nói "**INSERT with a UNIQUE constraint in the same transaction**" hoặc atomic UPDATE.
- Trùng request → **replay response cũ**, không trả lỗi.
- Message liên quan tiền/hợp đồng **không được mất** → outbox / at-least-once + idempotent.
- Nhầm **Outbox với Mediator** (mediator là in-process).
- Nêu **trade-off** (sync vs async, monolith vs service), không trả lời một chiều.
- Sự cố: **tên vấn đề + công cụ điều tra + xử lý tạm + xử lý gốc + phòng ngừa**.
- Đưa **con số** (2M+ player, ~150 project, ~1.330 commit, ~200 file test, ~30 service, 10 loại chi phí).
- Diễn đạt chính xác cơ chế (vd. thread pool **bơm thread chậm**, không phải "tạo quá nhiều thread").
- Chọn key idempotency đúng độ mịn.
- Tiếng Anh: "-s" ngôi 3, không "is depend", tránh bị động thừa.
- Không nhắc chi tiết nội bộ ShedPro; không chê code Joblogic; nói đúng công nghệ thật (EF6, MSTest, Vue, Jenkins/Helm config).
- Không nói quá về CI/CD, AWS, microservice architecture.
- Interviewer gốc frontend → tôn trọng UX, không coi nhẹ FE.
- Không biết thì nói thật + cách tiếp cận (= value **Be Accountable / chính trực**).
- Khi kể sự cố/bất đồng: **coach, not police**, không đổ lỗi, không nói xấu người khác (value **Love our People**).

### 30.3 Trong phòng
- Nghe hết câu hỏi, hỏi lại nếu chưa rõ ("Just to make sure…").
- Trả lời ngắn trước (1–2 câu), rồi hỏi "Would you like me to go deeper into X?".
- Vẽ khi nói kiến trúc.
- Ghi chú câu hỏi để hỏi ngược.

---

## 31. Phụ lục

### 31.1 Bảng con số của Hiệp
| Số | Ý nghĩa |
|---|---|
| ~4 năm | Kinh nghiệm (từ 07/2022) |
| 2M+ | Registered players PlaySweeps |
| ~150 | Project trong backend PlaySweeps |
| ~1.330 | Commit backend của Hiệp (nhiều nhất team) |
| ~340 | Commit web React của Hiệp |
| ~200 | File test xUnit + Moq |
| ~354 | Ticket Jira |
| 3 | TDD đã viết (Quest Engine V2, Banner System, CRM Direct-Target Offers) |
| ~30 | Service (Azure Functions) ở Joblogic |
| ~139 | Commit Joblogic |
| 4 | Feature lớn ở Joblogic |
| 10 | Loại chi phí trong Cost Breakdown |
| 39 / 46 / 26 | Module / entity / migration ở EIM |
| 4 | Intern Hiệp lead ở Astraler |

### 31.2 Câu tiếng Anh hữu dụng
- "Let me make sure I understand the question…"
- "There are two options here, and the trade-off is…"
- "In my last project we did X; for the Ops Hub I'd assume Y and confirm with the PM."
- "I haven't used that directly, but here's how I'd approach it."
- "The short answer is…, and the reason is…"
- "If I had to pick one, I'd go with… because…"
- "What I'd do differently next time is…"
- "That's a good point — I hadn't considered that. In that case I'd…"

### 31.3 Thuật ngữ nhanh (EN → VI)
idempotent (gọi nhiều lần cùng kết quả) · race condition (tranh chấp) · lost update (mất cập nhật) · optimistic concurrency (khoá lạc quan) · backfill (điền dữ liệu cũ) · expand/contract (mở rộng rồi thu gọn schema) · characterization test (test chụp hành vi) · strangler fig (thay dần) · seam (điểm chèn) · noisy neighbor (tenant gây ồn) · graceful degradation (suy giảm êm) · circuit breaker (ngắt mạch) · dead-letter queue (hàng chờ chết) · outbox (hộp thư đi) · ledger (sổ cái) · snapshot (bản chụp) · balance due (số còn nợ) · down payment / deposit (đặt cọc) · installment (kỳ trả góp) · eligibility (đủ điều kiện) · audit trail (dấu vết kiểm toán) · feature flag (cờ tính năng) · rollback (quay lui) · blue/green (hai môi trường xanh/lục) · canary (thả dần) · presigned URL (URL ký sẵn).

### 31.4 Đối chiếu JD → section (kiểm tra không sót)
| Yêu cầu JD | Section |
|---|---|
| ≥ 4 năm C#/.NET, .NET Core | 1.2, 11, 12, 13 |
| ASP.NET MVC và/hoặc Web API | 13, 14, 4 |
| AWS / cloud | 21, 20 |
| HTML/CSS/JS, React/Angular/Vue | 19 |
| Design patterns + refactoring | 6, 7 |
| Clean, testable, well-structured code; architectural patterns; stable & scalable | 3, 5, 18 |
| Readable, maintainable code | 5, 7 |
| Git | 27 |
| Agile | 28, 9 |
| RESTful API | 4 |
| Unit test | 18 |
| English | 10.3, 31.2 |
| Tiếp quản code partner Mỹ | 7, 28 |
| Leading new feature development | 2.1 (Quest Engine), 9, 10 |
| Performance, quality, long-term maintainability | 25, 5, 15 |
| Learn quickly and adapt | 1.3, 10 |
| Hiểu nghiệp vụ, làm sát PM, "1% improvements", accountable | 8, 9, 10 |
| 5 core values (1% Improvement, Customer Success, Problem Solving, Accountable, Love People & Communities) | `S-seadev-culture.md`; nối ở 1.3, 9, 10, 29 |
| Quoting, sales orders, RTO contracts, production tracking, delivery scheduling | 8, 26 |
| Profile SA: Software Architecture, CI/CD, AWS, REST, Clean Coding, React/TS, UX | 3, 20, 21, 4, 5, 19 |
| Nền SA từ Urbanise: tiền định kỳ, workflow, tài liệu, tích hợp ngân hàng, owner portal | 8.3, 6 (State), 8.5, 22, 8.10 câu 20 |
