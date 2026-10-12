# Tiến độ training

| Buổi | Chủ đề | Trạng thái | Ghi chú |
|---|---|---|---|
| 1 | Async, concurrency, DI | ✅ Xong | Async/await, `.Result`, thread-pool starvation, race condition, atomic UPDATE, Nexus, queue: **xong** (xem `notes/01-async-concurrency.md`). DI/captive dependency, `Task.WhenAll`+DbContext, connection pool, idempotency Pragmatic: **xong**. Bài 4 quest reward/outbox: lần đầu Junior–Mid, làm lại đạt Mid+ (còn thiếu: "same transaction", SessionId = thứ tự cho cùng player) |
| 2 | ASP.NET Core pipeline và API design | 🟡 Lý thuyết xong | A: Mid (vị trí correlation middleware, body stream/resource filter). B, C1, C2: user bỏ qua bài tập → **ôn lại bằng câu hỏi nhanh đầu Buổi 3**. Xem `notes/02-aspnet-pipeline-api.md` |
| 3 | Data: EF Core, SQL, transaction | ⬜ | Một phần isolation, lock đã gặp ở buổi 1 |
| 4 | Caching, messaging, outbox, saga | ⬜ | Đã bàn sơ queue, SessionId, outbox (user nhầm outbox với mediator; chấp nhận mất message) |
| 5 | Distributed systems và resilience | ⬜ | |
| 6 | Performance và observability | ⬜ | |
| 7 | Security | ⬜ | |
| 8–10 | System design (payment, rate limiter, notification…) | ⬜ | |
| 11 | Code review (câu 133–136) | 🟡 | Câu 134 (`.Result` + HttpClient) đã làm |
| 12 | Behavioral STAR (tiếng Anh) | ⬜ | Chất liệu: Socure, Quest Engine, on-call incident, Rive, Nexus balance |

## Đánh giá hiện tại
- **Mạnh:** hiểu bản chất async (0 thread chờ khi `await`, `.Result` chiếm 2 thread), tìm lỗi trong code review tốt (bài Redeem: tìm đủ 3 lỗi), hay phản biện và đào sâu.
- **Cần cải thiện:**
  - Nêu **tên vấn đề và công cụ điều tra** (dotnet-counters, dotnet-dump, App Insights) khi trả lời câu hỏi về sự cố production.
  - Diễn đạt chính xác **cơ chế** (ví dụ: thread pool *tạo thread chậm*, không phải "tạo quá nhiều thread").
  - Thứ tự ưu tiên xử lý concurrency: atomic UPDATE / rowversion trước, distributed lock sau.
  - Tiếng Anh nói (đang học PTE): hay thiếu -s ngôi 3, "is depend", "will be encountered".
  - Idempotency: hay **check ngoài transaction** (check-then-act), trả **lỗi** khi trùng thay vì replay response, chọn key quá thô (roundId).
  - **Lặp lại lỗi check-then-act** (bài 3 và bài 4): luôn nói "INSERT with UNIQUE in the same transaction".
  - Chấp nhận mất message cho luồng liên quan tiền; nhầm Mediator với Outbox.
  - Trả lời một chiều (sync vs async), chưa nêu trade-off.
  - Trả lời thiếu con số cụ thể (vd. pods × pool vs max_connections).

## Bài tập đang chờ
- User có xu hướng **bỏ qua bài tự kiểm tra** (Buổi 2: B, C1, C2, phần ôn a/b/c). Đầu Buổi 3 hỏi gọn 5 câu: middleware vs filter, 422 vs callback provider, repository với EF vs Dapper, over-posting, offset vs keyset.
- Cần user xác nhận: Sweeps có class `...Repository` + interface không, có bọc SP không (để ghi `career-facts`).
- Đầu Buổi 2: kiểm tra nhanh 3 câu: (a) check-then-act là gì, sửa sao; (b) SessionId giải quyết gì; (c) Outbox giải quyết gì.

## Lịch sử bài tập Buổi 1
Bài 1–3 xong (bài 1: Senior sau khi làm lại; bài 2: user nhờ giải; bài 3: Mid).
4. Quest reward nên xử lý đồng bộ hay qua Service Bus? Nếu qua queue, `SessionId` là gì, và chặn cộng thưởng 2 lần thế nào?
