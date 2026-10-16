# Plan ôn Joblogic cho SEADEV (3 buổi)

Người phỏng vấn: Solution Architect + PO. Mỗi buổi: học ngắn → user tự nói (tiếng Anh) → chấm → chốt câu trả lời.

## Buổi 1 — Hệ thống (cho SA)
Mục tiêu: vẽ và giải thích kiến trúc trong 2 phút.
1. Tổng thể: web, portal, mobile, API → ~30 service Azure Functions → SQL shard, MongoDB, Redis, Blob, Service Bus.
2. Multi-tenant: shard theo tenant, middleware chọn shard + chặn tenant hết hạn, lọc TenantId, job nền fan-out theo tenant.
3. Giao tiếp: HTTP (query), queue (command), topic (event); OneOf thay exception; idempotency.
4. Gói đăng ký & phân quyền: module theo tenant, feature flag, RBAC 3 loại user.
5. Azure → AWS.
Bài toán thực tế (SA):
- Một tenant thấy dữ liệu của tenant khác — điều tra và phòng ngừa thế nào?
- Một tenant lớn làm chậm cả hệ thống (noisy neighbor) — xử lý ra sao?
- Message bị xử lý 2 lần → gửi 2 email/tạo 2 bản ghi — sửa thế nào?
- Thêm một tính năng chỉ cho gói cao cấp — thiết kế gating ở đâu?
Đầu ra: pitch kiến trúc 2 phút + trả lời 4 bài toán.

## Buổi 2 — 4 feature đã làm (cho SA + PO)
Mỗi feature theo khung: **vấn đề → nghiệp vụ → thiết kế → edge case → kết quả**.
1. Project Cost Breakdown: estimated vs actual, variance, profit/margin, đa tiền tệ.
2. Customer Contract: gắn hợp đồng, ẩn/hiện theo gói, audit có version, DocX tags (Previously Claimed).
3. Selling Rate Times & Holidays: giá theo khung giờ/ngày lễ, pay band.
4. Job Spend Limit: hạn mức theo visit, event → thông báo back-office, Customer Portal, permission, redeploy.
Bài toán thực tế (gắn với feature):
- Báo cáo lợi nhuận hiển thị sai/chậm với project lớn — điều tra thế nào?
- Đổi template hợp đồng/hoá đơn nhưng tài liệu đã ký phải giữ nguyên — làm sao?
- Giá theo khung giờ: ca làm vắt qua nửa đêm / ngày lễ / múi giờ khác — tính thế nào?
- Đơn đã giao cho người ở hiện trường (thiết bị) rồi văn phòng sửa — xử lý ra sao?
- Hai người cùng sửa một bản ghi — chặn ghi đè thế nào?
Đầu ra: mỗi feature 1 câu chuyện 60–90 giây + trả lời bài toán.

## Buổi 3 — Business & PO + mock
1. Thuật ngữ: markup vs margin, deposit/balance due, cumulative invoicing, approval limit, audit trail, subscription tier.
2. Nối kinh nghiệm sang phạm vi JD (quote → order → RTO contract → production → delivery) dưới dạng giả định + câu hỏi làm rõ.
3. Câu hỏi PO: làm rõ yêu cầu, edge case, thay đổi phạm vi, làm việc từ xa.
4. Bài toán thực tế (PO + phạm vi JD):
   - Quote đã gửi khách thì bảng giá thay đổi — xử lý thế nào?
   - Số tiền còn phải trả (balance due) sai với một số đơn — tiếp cận ra sao?
   - Huỷ đơn khi đã vào sản xuất — cần hỏi PO những gì?
   - Ngày giao hàng lệch một ngày do múi giờ/DST — nguyên nhân và cách sửa?
   - Tiếp quản codebase từ đối tác: 2 tuần đầu bạn làm gì? Sửa bug gấp khi chưa có test thì sao?
   - Yêu cầu mơ hồ / đổi giữa sprint — bạn làm gì?
5. Mock 30 phút (SA + PO), chấm và sửa.
Đầu ra: bộ câu trả lời cuối + 3 câu hỏi ngược cho interviewer.
