# SEADEV — hồ sơ Solution Architect có thể phỏng vấn (Khiet Vo)

Ngày tra cứu: 2026-10-23. Chỉ thông tin nghề nghiệp công khai. Bổ sung cho `notes/S-seadev-interview-kit.md`.

## 1. Lý lịch

| Thông tin | Nguồn |
|---|---|
| **Software Architect tại Seadev** (từ 04/2025, Đà Nẵng) | LinkedIn (Hiệp dán), ZoomInfo |
| **Web Developer tại AgilityIO** (outsourcing web/mobile cho startup Mỹ, có DevOps AWS) | LinkedIn |
| **2 vị trí tại Urbanise** (SaaS Úc cho quản lý chung cư/strata và facilities: trust accounting, phí định kỳ, workflow bảo trì, tài liệu, tích hợp ngân hàng) | LinkedIn, ZoomInfo |
| Không tìm thấy GitHub, blog, talk | — |

### Skill tự khai trên LinkedIn (Hiệp dán, 2026-10-23)
- **Gắn với vai trò hiện tại ở Seadev:** Software Architecture, **CI/CD**.
- **Gắn với AgilityIO:** **AWS**; được đồng nghiệp endorse Front-end (đã pass LinkedIn Skill Assessment, 7 endorsement), Full-Stack, Web Development.
- **Gắn với Urbanise + 1 công ty khác:** React.js, TypeScript, HTML5, CSS, UX, UI Design, Front-end, Back-End Web Development, **REST**, **Clean Coding**, JSOM, Web Applications, Agile.
- Khác: Node.js, Problem Solving, Critical Thinking.

### Đọc profile này thế nào
- Đây là người **gốc frontend / full stack JavaScript–TypeScript** đi lên architect. Danh sách **không có C#, .NET, SQL**. Có thể họ vẫn biết .NET (đang là SA cho dự án C#), nhưng điểm mạnh tự khai là React/TS, REST, clean code, CI/CD, AWS.
- **JSOM** = SharePoint JavaScript Object Model (API phía client của SharePoint). Chỉ cần biết nó là gì, gần như không bị hỏi.
- Hệ quả: họ sẽ ít soi sâu nội tại CLR/EF Core, mà soi **ranh giới API giữa FE và BE**, **chất lượng code**, **pipeline triển khai**, **AWS**, và **trải nghiệm người dùng** do quyết định backend gây ra.

## 2. Mảng có khả năng bị đào sâu (xếp theo độ ưu tiên)

1. **REST API design** (giao điểm lớn nhất giữa họ và vị trí C#): naming resource, status code, pagination, versioning, error format, idempotency, concurrency bằng ETag.
2. **Clean code / refactoring / architecture**: SOLID, layering, code review, tiếp quản code partner Mỹ → kit §2, §5.
3. **CI/CD** ⚠️ **điểm yếu của Hiệp**: kinh nghiệm thật chỉ là sửa config Jenkins/Helm values, chưa tự dựng pipeline. Phải trả lời trung thực + nói được pipeline chuẩn cho .NET.
4. **AWS** → kit §9.
5. **Frontend React/TS và hợp đồng FE–BE**: Hiệp có kinh nghiệm thật (PlaySweeps React 18 + Redux, EIM React + TanStack Query + Ant Design, Joblogic MVC + React).
6. **UX thinking**: backend ảnh hưởng UX ra sao (latency, thông báo lỗi, trạng thái pending, optimistic update).
7. **Nghiệp vụ SaaS vận hành + tiền** (từ Urbanise) → kit §7, vẫn quan trọng nhưng nhiều khả năng PO hỏi nhiều hơn SA.
8. **Node.js vs .NET**: có thể so sánh event loop với thread pool → `notes/01-async-concurrency.md`.

## 3. Kiến thức cần nắm nhanh

### 3.1 REST
- Resource là danh từ số nhiều: `GET /quotes/{id}`, `POST /quotes/{id}/finalize` cho hành động nghiệp vụ không phải CRUD (chấp nhận được, nói rõ là "action endpoint").
- Status code: 200/201 (+`Location`)/204, 400 validation, 401 vs 403, 404, **409 conflict** (trạng thái không cho phép), **412 precondition failed** (ETag lệch), 422 (tuỳ team), 429, 5xx.
- Lỗi theo **ProblemDetails (RFC 9457)**, validation trả `errors` theo field để React map vào form.
- Idempotency: GET/PUT/DELETE idempotent theo định nghĩa; POST tạo tiền/đơn → header `Idempotency-Key`, lưu kết quả theo key (Pragmatic).
- Concurrency: trả `ETag` (từ `rowversion`), client gửi `If-Match` → 412 nếu người khác đã sửa.
- Pagination: offset cho bảng nhỏ/admin, **keyset (cursor)** cho danh sách lớn/production queue.
- Versioning: URL `/v1` hoặc header; ưu tiên thay đổi **additive**, không đổi nghĩa field cũ.
- Hợp đồng FE–BE: **OpenAPI** (Swashbuckle/NSwag) → sinh TypeScript client/types, tránh lệch kiểu. EIM đã dùng Swagger.

Câu mẫu:
> For the Ops Hub I'd keep the API resource-oriented, with explicit action endpoints for business transitions like finalizing a quote, because those aren't just field updates. Errors follow ProblemDetails so the React side can map validation errors to fields. Anything that moves money or creates an order accepts an idempotency key, and edits use ETags so two staff members can't silently overwrite each other. The OpenAPI spec is the contract, and we generate TypeScript types from it so frontend and backend can't drift.

### 3.2 CI/CD (pipeline chuẩn cho .NET trên AWS)
1. **PR build**: `dotnet restore` → `build` → `test` (unit + integration với Testcontainers) → lint/format, analyzer, scan dependency. Bắt buộc pass trước khi merge.
2. **Main build**: build **một artifact/Docker image duy nhất**, tag theo commit SHA, đẩy lên ECR.
3. **Deploy** cùng artifact qua các môi trường dev → staging → prod (promote, không build lại). Config/secrets theo môi trường (AWS Secrets Manager / Parameter Store), không nằm trong image.
4. **DB migration**: chạy như bước riêng trước khi deploy app (EF Core migration bundle hoặc script idempotent), theo kiểu **expand/contract** để bản cũ và mới cùng chạy được.
5. **Chiến lược phát hành**: rolling hoặc blue/green (ECS/CodeDeploy), health check, **rollback** bằng image cũ; tính năng lớn bật bằng **feature flag**.
6. **Sau deploy**: smoke test, theo dõi error rate/latency (CloudWatch), cảnh báo.
- Công cụ: GitHub Actions, AWS CodePipeline/CodeBuild, Azure DevOps, Jenkins — nguyên lý như nhau.

Câu trả lời trung thực (dùng khi bị hỏi kinh nghiệm):
> I haven't owned a pipeline end to end; in my previous teams DevOps owned it and I worked inside it: I've edited Jenkins and Helm configuration for my services, and I own the parts a developer should — tests that run in the pipeline, backward-compatible migrations, feature flags, and checking metrics after a release. If I set one up for the Ops Hub, I'd build one image per commit, promote the same image through environments, run migrations as a separate expand/contract step, and keep rollback to a single action.

(⚠️ Kiểm tra lại với Hiệp: có từng tự viết YAML pipeline nào không — career-facts ghi GitHub Actions là "không đủ bằng chứng".)

### 3.3 Frontend / UX từ góc backend
- Token: ưu tiên **HttpOnly cookie** + SameSite (chống XSS đọc token) thay vì localStorage; kèm CSRF protection. CORS chỉ mở cho origin cần.
- Server state: TanStack Query (cache, refetch, invalidate sau mutation), optimistic update có rollback khi lỗi.
- Validation hai phía: FE để UX nhanh, BE là nguồn sự thật; chung schema qua OpenAPI hoặc chia sẻ rule.
- Thao tác chậm (sinh PDF, gọi RTO provider): trả **202 Accepted** + trạng thái job, FE poll hoặc nhận push (SignalR/WebSocket), không treo request.
- MVC Razor vs React SPA: Razor hợp màn hình form nội bộ, SEO/không cần JS nặng; SPA hợp màn hình tương tác cao (production board, lịch giao hàng). Joblogic dùng cả hai.

## 4. Câu hỏi luyện

REST & hợp đồng FE–BE:
1. *"Design the API for finalizing a quote and converting it to a sales order. What endpoints, status codes and error responses?"*
2. *"Two staff members edit the same order at once. What does the API do and what does the user see?"* → ETag/If-Match, 412, UI hiện bản mới để merge.
3. *"How do you keep TypeScript types on the frontend in sync with C# DTOs?"*
4. *"How would you version this API when the US partner's mobile app still uses the old one?"*

Clean code / architecture:
5. *"Show me how you'd structure a .NET solution for this product. Where does business logic live?"* → kit §2.
6. *"What do you look for when reviewing a pull request?"* → đúng nghiệp vụ, test, đặt tên, ranh giới layer, xử lý lỗi, hiệu năng/N+1, bảo mật, migration an toàn.
7. *"Here is a 400-line controller action. How would you refactor it safely?"* → kit §5.

CI/CD & AWS:
8. *"Walk me through the pipeline from a merged PR to production."*
9. *"A release breaks production and it included a database migration. How do you roll back?"* → expand/contract nên rollback app không cần rollback DB; feature flag tắt trước.
10. *"How would you host this .NET app on AWS, and where do secrets live?"* → kit §9.

Frontend / UX:
11. *"Generating a contract PDF takes 10 seconds. How do you design the API and the UI around it?"* → 202 + job status.
12. *"Where would you store the auth token in a React app and why?"*
13. *"When would you choose Razor MVC over React for a screen?"*

Nghiệp vụ (nếu họ kéo về kinh nghiệm Urbanise):
14. *"A customer paid a deposit, then the quote was revised. How do you keep balance due correct?"* → kit §7.2.
15. *"The RTO provider API is down for 30 minutes. What happens to pending requests?"* → kit §7.6.

## 5. Câu hỏi ngược
- "What does the CI/CD and release process look like today between Seadev and the US partner?"
- "Is the frontend React, MVC, or a mix, and who owns the API contract?"
- "What would you most like a new developer to improve in the codebase in the first three months?"

**Lưu ý thái độ:** không nhắc là đã tra hồ sơ chi tiết. Họ mạnh frontend → đừng nói kiểu "frontend chỉ là phần phụ"; thể hiện mình nghĩ cho người dùng cuối.
