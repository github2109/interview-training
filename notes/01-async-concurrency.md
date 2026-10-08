# Buổi 1 — Async & concurrency (tóm tắt)

## 1. Async/await
- `await` I/O **không tạo thread**. Thread được trả về pool; lúc chờ, **0 thread bị chiếm** (OS theo dõi qua IOCP/epoll). Khi I/O xong, một thread rảnh bất kỳ chạy continuation.
- Task là object "sẽ có kết quả", không phải thread. Thread là luồng thật của OS, tốn khoảng 1 MB stack.
- Async **tăng throughput, không giảm latency** của một request. Ví dụ: 100 thread, mỗi request chờ DB 200 ms. Sync phục vụ được khoảng 500 req/s; async có thể lên khoảng 20.000 req/s. Mỗi request vẫn mất khoảng 205 ms.
- ASP.NET Core: không bọc `Task.Run` quanh code của request.

> "Async doesn't make a single request faster — it frees the thread while waiting, so the same server handles far more concurrent requests."

## 2. Không await / sync I/O / `.Result`
- **Quên await (fire-and-forget):** mất exception (client vẫn nhận 200), DbContext bị dispose, lỗi "second operation on context", sai thứ tự, mất việc khi shutdown. Việc nền thì đưa vào Channel/BackgroundService hoặc queue (Outbox), không fire-and-forget.
- **`async` nhưng không có await:** chạy đồng bộ (warning CS1998).
- **`async` nhưng gọi API sync** (`First()`, `File.ReadAllText`): vẫn chặn thread. Phải "async all the way".
- **Trả Task không await** thì hợp lệ, trừ khi có `using`, `try/catch`, `finally`.
- **`.Result` (sync-over-async):** chặn thread gọi bằng wait handle, và continuation cần thêm một thread khác, nên **một thao tác chiếm 2 thread**. Môi trường có SynchronizationContext (ASP.NET cũ, WPF) bị deadlock. ASP.NET Core không deadlock nhưng bị **thread-pool starvation**. `GetAwaiter().GetResult()` vẫn chặn, chỉ khác là exception không bị bọc.

## 3. Thread-pool starvation
- Triệu chứng: latency tăng vọt, **CPU thấp**, DB bình thường, số thread tăng chậm từng chút.
- Cơ chế: các thread bị chặn nên công việc xếp hàng; pool chỉ **bơm thêm khoảng 1–2 thread mỗi giây**.
- Xác nhận: `dotnet-counters` (ThreadPool Queue Length tăng), `dotnet-dump`/`dotnet-stack` (nhiều stack nằm trong `.Result`/`.Wait`).
- Chữa tạm: `ThreadPool.SetMinThreads`. Chữa tận gốc: async all the way, CancellationToken, timeout.

## 4. HttpClient
Dùng `IHttpClientFactory`/typed client (tránh cạn socket), đặt timeout bằng linked CTS, `EnsureSuccessStatusCode`, `ReadFromJsonAsync`, resilience handler.

## 5. Concurrency khi cập nhật balance
- **Lost update** xảy ra khi đọc-sửa-ghi trong bộ nhớ ứng dụng (định nghĩa của Microsoft).
- **Chuẩn:** `UPDATE ... SET Balance = Balance - @x WHERE Id=@id AND Balance >= @x`. Exclusive lock được giữ tới commit ở **mọi isolation level** (Microsoft Learn); người cập nhật thứ hai chờ rồi **đánh giá lại WHERE** trên bản đã commit (PostgreSQL docs, có ví dụ accounts.balance); DDIA ch.7 gọi đây là "atomic write operations".
- Idempotency key (UNIQUE index) chống **retry của cùng một yêu cầu**; atomic UPDATE chống **các yêu cầu khác nhau chạy đồng thời**. Hai thứ khác nhau.
- Khi nào cần thêm: logic nhiều bước thì dùng `UPDLOCK` hoặc rowversion; cần kiểm toán thì dùng ledger chỉ ghi thêm; nhiều dòng thì lock theo thứ tự và retry khi deadlock; hot row thì cân nhắc batch hoặc queue.
- Thứ tự ưu tiên: atomic UPDATE, rồi optimistic concurrency, rồi distributed lock.

## 6. Thực tế PlaySweeps (để kể khi phỏng vấn)
- Sweeps Coin do **Nexus** sở hữu: gửi **delta + TransactionId GUID**; stored procedure của Nexus kiểm tra idempotency (bảng giao dịch đã xử lý) rồi kiểm tra số dư và cập nhật, **không dùng queue**, dựa vào lock của SQL. Lưu ý: cần UNIQUE trên TransactionId để chặn trùng khi hai request đến đồng thời.
- Bảng SQL `PlayerBalances` là bản sao, ghi **giá trị tuyệt đối** (`SetPlayerBalanceChange_v0_2`). Rủi ro bản sao bị cũ khi response về không theo thứ tự → cần kiểm tra version/sequence.
- Lock Redis ở BE: spin theo (player, game) với `TryLock` fail-fast; deposit/redemption theo transaction; PrizeOut theo player.
- Điểm yếu nên tự nêu: đọc balance **trước** khi lấy lock; lock chưa bao hết mọi luồng ghi; Redis lock không có fencing token; procedure chỉ cảnh báo khi phát hiện lệch.

> "Sweeps Coin was owned by Nexus. We sent deltas with a unique transaction ID; Nexus ran an idempotency check and an atomic funds check-and-update in one DB transaction, so concurrent spin and claim applied correctly in any order. The weak spot was our SQL mirror storing absolute balances — I'd add a sequence check and always do funds checks against Nexus."

## 7. Queue cho balance?
- Single-writer theo player là pattern hợp lệ, nhưng **không** dùng cho callback ví đồng bộ (provider cần kết quả ngay).
- Queue phù hợp: thưởng, đồng bộ, thông báo, đối soát. Với dữ liệu tiền, chọn **Service Bus** (bền, có sessions FIFO theo player, DLQ, duplicate detection) thay vì Redis. Consumer vẫn phải idempotent (at-least-once).
