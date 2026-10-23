# SEADEV — hồ sơ Solution Architect có thể phỏng vấn (Khiet Vo)

Ngày tra cứu: 2026-10-23. Chỉ thông tin nghề nghiệp công khai. Bổ sung cho `notes/S-seadev-interview-kit.md`.

## 1. Tìm được gì (và độ chắc chắn)

| Thông tin | Nguồn | Độ chắc |
|---|---|---|
| Làm ở Seadev từ **04/2025**, Đà Nẵng; headline LinkedIn ghi "Software Engineer at Seadev" | Kết quả tìm kiếm trỏ tới LinkedIn `khiet-vo-538a0719b` (không mở được trang trực tiếp) | Khá chắc |
| Chức danh **Software Architect** tại Seadev, email domain `seadev.us` | ZoomInfo (trang tổng hợp, không mở được) | Trung bình |
| Từng là **Web Developer tại Urbanise** | ZoomInfo | Trung bình |
| Từng làm ở **AgilityIO** | ZoomInfo | Trung bình |

**Chưa tìm được:** danh sách skill, stack cụ thể, GitHub, blog, talk. Trùng tên với nhiều người khác (Massey University, ITD…), đã loại.
→ Để chính xác hơn, Hiệp dán phần *Experience* + *Skills* (hoặc ảnh chụp) của profile LinkedIn vào thread.

### Hai công ty cũ là gì
- **Urbanise** (ASX: UBN, Úc): SaaS đa tenant cho **quản lý strata (chung cư) và facilities management**. Strata gồm *trust accounting, levy (phí định kỳ), workflow, theo dõi bảo trì, quản lý tài liệu, báo cáo*; 2026 đang làm **tích hợp ngân hàng (NAB), owner portal có thanh toán, đối soát levy**. Khách lớn PICA ký hợp đồng 10 năm.
- **AgilityIO**: công ty outsourcing/product dev (HQ New York, văn phòng Việt Nam), làm web/mobile cho startup Mỹ, có DevOps AWS.
- **Seadev**: làm cho đối tác Mỹ (ShedPro Ops Hub).

## 2. Suy luận: người này có thể đào sâu vào đâu

> Đây là suy luận từ lý lịch công ty, **không phải** skill người đó tự khai. Stack thật của Urbanise/AgilityIO chưa xác minh.

1. **Nghiệp vụ SaaS vận hành + tiền** (nguy cơ cao nhất). Urbanise ≈ Ops Hub: đều là SaaS vận hành cho doanh nghiệp nhỏ, có tiền định kỳ, tài liệu, workflow, đối soát. Dự đoán hỏi: ledger vs số dư, làm tròn, đối soát thanh toán, idempotent webhook, tài liệu bất biến.
2. **Multi-tenant**: cô lập dữ liệu, cấu hình theo tenant, migrate schema cho nhiều tenant, noisy neighbor.
3. **Workflow / state machine**: trạng thái bảo trì (Urbanise) ↔ trạng thái quote → order → production → delivery (Ops Hub). Hỏi: chuyển trạng thái hợp lệ, audit trail, concurrency khi 2 người cùng sửa.
4. **Tích hợp bên thứ ba**: bank feed / payment / RTO provider. Retry, backoff, outbox, xử lý lỗi để vận hành retry tay.
5. **Full stack web** (khởi đầu là Web Developer): có thể hỏi cả frontend (React/Angular hoặc MVC Razor), API contract, phân trang, validation hai phía.
6. **Làm với đối tác Mỹ / outsourcing** (AgilityIO, Seadev): tiếp quản code người khác, giao tiếp async qua múi giờ, ước lượng, viết tài liệu, PR review.
7. **AWS** (AgilityIO có DevOps AWS, JD SEADEV có AWS): deploy .NET, S3 presigned URL, SQS, RDS, CloudWatch.

## 3. Câu hỏi luyện (gắn với kit)

Nghiệp vụ & tiền (kit §7.2):
1. *"A customer paid a deposit, then the quote was revised. How do you compute balance due and keep it correct?"* → ledger, snapshot giá, không cộng trừ tay.
2. *"Our bank/payment provider sends the same webhook twice and one arrives out of order. What happens in your design?"* → idempotency key theo event id, xử lý theo version/thời điểm (Pragmatic, PlaySweeps).
3. *"How would you reconcile what the system thinks was paid with what the bank actually received?"* → bảng đối soát, trạng thái matched/unmatched, job hằng ngày, màn hình xử lý tay.

Multi-tenant (kit §7.5, `J-multitenant-deep.md`):
4. *"One big tenant makes the app slow for everyone. How do you find and fix it?"*
5. *"How do you roll out a schema change safely across all tenants?"* → expand/contract, migration chạy trước, backward-compatible.

Workflow:
6. *"Model the order lifecycle. How do you stop invalid transitions and two users updating the same order?"* → state machine, optimistic concurrency (`rowversion`/`xmin`), audit log.

Tài liệu (kit §7.4):
7. *"A contract was signed, then the template changed. A customer disputes it a year later. What do you show them?"*

Tích hợp & vận hành (kit §7.6, §7.7):
8. *"The RTO provider API is down for 30 minutes during business hours. What does the user see, and what happens to pending requests?"* → outbox + retry, circuit breaker, trạng thái "pending", không mất dữ liệu.

Tiếp quản code / đối tác Mỹ (kit §5, §11):
9. *"You inherit a codebase from a US partner with no tests. What do you do in the first two weeks?"*
10. *"The US PM is 12 hours behind and the requirement is unclear. How do you avoid being blocked?"*

Full stack:
11. *"Where do you put validation, and how do you keep frontend and backend rules in sync?"*

## 4. Câu hỏi ngược có thể hỏi người này
- "Coming from a strata/FM SaaS background, which parts of Ops Hub do you see as the riskiest: money, scheduling, or integrations?" (chỉ dùng nếu họ tự giới thiệu từng làm Urbanise; đừng tỏ ra đã "điều tra" họ).
- "How is the split between Seadev and the US partner on architecture decisions?"

**Lưu ý thái độ:** không nhắc là đã tra hồ sơ chi tiết. Nếu họ kể về kinh nghiệm cũ, nối vào câu chuyện Joblogic / PlaySweeps tương ứng.
