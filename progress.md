# Tiến độ training

| Buổi | Chủ đề | Trạng thái | Ghi chú |
|---|---|---|---|
| 1 | Async, concurrency, DI | 🟡 Đang học | Async/await, `.Result`, thread-pool starvation, race condition, atomic UPDATE, Nexus, queue: **xong** (xem `notes/01-async-concurrency.md`). **Còn lại:** DI lifetimes và captive dependency, `Task.WhenAll` với DbContext, câu chuyện idempotency Pragmatic |
| 2 | ASP.NET Core pipeline và API design | ⬜ | |
| 3 | Data: EF Core, SQL, transaction | ⬜ | Một phần isolation, lock đã gặp ở buổi 1 |
| 4 | Caching, messaging, outbox, saga | ⬜ | Đã bàn sơ về queue (Service Bus vs Redis) |
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
  - Tiếng Anh nói (đang học PTE).

## Bài tập đang chờ user trả lời (Buổi 1)
1. `QuestCacheService` là Singleton nhưng inject `AppDbContext` (Scoped): chuyện gì xảy ra, sửa thế nào?
2. Endpoint lobby lấy game, balance, quest (độc lập nhau): viết code với `Task.WhenAll`. Nếu dùng chung một DbContext thì sao?
3. Kể cách xử lý idempotency cho callback Pragmatic: key, lưu ở đâu, giữ bao lâu, trả về gì khi trùng.
4. Quest reward nên xử lý đồng bộ hay qua Service Bus? Nếu qua queue, `SessionId` là gì, và chặn cộng thưởng 2 lần thế nào?
