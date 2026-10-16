# Plan ôn Joblogic cho SEADEV (3 buổi)

Người phỏng vấn: Solution Architect + PO. Mỗi buổi: học ngắn → user tự nói (tiếng Anh) → chấm → chốt câu trả lời.

## Buổi 1 — Hệ thống (cho SA)
Mục tiêu: vẽ và giải thích kiến trúc trong 2 phút.
1. Tổng thể: web, portal, mobile, API → ~30 service Azure Functions → SQL shard, MongoDB, Redis, Blob, Service Bus.
2. Multi-tenant: shard theo tenant, middleware chọn shard + chặn tenant hết hạn, lọc TenantId, job nền fan-out theo tenant.
3. Giao tiếp: HTTP (query), queue (command), topic (event); OneOf thay exception; idempotency.
4. Gói đăng ký & phân quyền: module theo tenant, feature flag, RBAC 3 loại user.
5. Azure → AWS.
Đầu ra: pitch kiến trúc 2 phút + trả lời 3 câu SA.

## Buổi 2 — 4 feature đã làm (cho SA + PO)
Mỗi feature theo khung: **vấn đề → nghiệp vụ → thiết kế → edge case → kết quả**.
1. Project Cost Breakdown: estimated vs actual, variance, profit/margin, đa tiền tệ.
2. Customer Contract: gắn hợp đồng, ẩn/hiện theo gói, audit có version, DocX tags (Previously Claimed).
3. Selling Rate Times & Holidays: giá theo khung giờ/ngày lễ, pay band.
4. Job Spend Limit: hạn mức theo visit, event → thông báo back-office, Customer Portal, permission, redeploy.
Đầu ra: mỗi feature 1 câu chuyện 60–90 giây.

## Buổi 3 — Business & PO + mock
1. Thuật ngữ: markup vs margin, deposit/balance due, cumulative invoicing, approval limit, audit trail, subscription tier.
2. Nối kinh nghiệm sang phạm vi JD (quote → order → RTO contract → production → delivery) dưới dạng giả định + câu hỏi làm rõ.
3. Câu hỏi PO: làm rõ yêu cầu, edge case, thay đổi phạm vi, làm việc từ xa.
4. Mock 30 phút (SA + PO), chấm và sửa.
Đầu ra: bộ câu trả lời cuối + 3 câu hỏi ngược cho interviewer.
