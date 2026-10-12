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

## 8. DI lifetimes và captive dependency
- Scope = `IServiceScope`, tạo đầu request, **Dispose** cuối request (dispose luôn Scoped/Transient `IDisposable`).
- **Captive dependency:** Singleton giữ DbContext Scoped → context sống cả process: lỗi "second operation" (không thread-safe), **change tracker phình** (chỉ giải phóng khi Dispose/`Clear()`; `SaveChanges` chỉ chuyển sang Unchanged; `DetectChanges` chậm dần), dữ liệu cũ, hoặc `ObjectDisposedException`. Nếu chỉ `AsNoTracking` thì không leak tracker.
- Sửa: không cần Singleton thì chuyển Scoped; là **cache** thì giữ Singleton + `IDbContextFactory`/`IServiceScopeFactory`, tạo context ngắn hạn khi cache miss. Phòng ngừa: `ValidateScopes` + `ValidateOnBuild` mọi môi trường.
- Quy tắc: **không inject service sống ngắn hơn vào service sống dài hơn.** (User từng nói ngược.)
- Điều tra leak: `dotnet-counters` (gc-heap-size, gen-2), `dotnet-gcdump` (đếm `InternalEntityEntry`, chuỗi giữ tham chiếu).

## 9. `Task.WhenAll` + DbContext
- Chung một context → throw "second operation" ngay: async chạy đồng bộ tới await đầu tiên, task 2 đâm vào task 1. Bản chất: 1 context = 1 connection = 1 lệnh/lúc (một stream request/response; MARS chỉ xen kẽ); tracker không thread-safe → EF fail-fast.
- Đúng: mỗi task một context (`IDbContextFactory`, `AsNoTracking`, `await using`). 170 ms → ~85 ms. `.Result` sau `WhenAll` an toàn.
- **Không nên** khi: endpoint nóng (×3 connection/request → cạn pool), cần snapshot nhất quán (3 transaction khác nhau), DB là nút thắt, query quá nhỏ. Ưu tiên cache (danh sách game), gộp round-trip, đo trước.
- Pool: `pods_max × MaxPoolSize ≤ max_connections − dự phòng` (4×100=400 > 200 → `53300 too many clients` lúc peak/scale-out). Hoặc PgBouncer.

## 10. Idempotency callback ví (Pragmatic)
- Key = **id của giao dịch** (provider + `reference`/transaction id), không phải roundId (một round có nhiều giao dịch: bet, result, free spin, refund). Code thật có `GetByRoundIdAsync` → cần xác minh lại cách hệ thống cũ dùng.
- **Check và trừ tiền trong CÙNG transaction**; UNIQUE constraint là trọng tài. Check ngoài transaction = check-then-act → hai request trùng đều qua check; row lock chỉ xếp hàng, **cả hai vẫn trừ** → trừ 2 lần.
- Giữ key: bảng giao dịch là ledger, giữ vĩnh viễn (ít nhất ≥ cửa sổ retry + đối soát của provider), không phải "vài ngày".
- Trùng → trả **response y hệt lần đầu** (thành công, cùng transaction id, balance hiện tại), không trả lỗi (provider sẽ hiểu là thất bại → refund/khiếu nại). Kiểm tra spec provider.
- Refund đến trước bet → ghi **tombstone** (refund đã nhận cho reference X), trả thành công không đổi tiền; bet đến sau thấy tombstone thì từ chối.

> "The idempotency key is the provider's transaction reference, scoped by provider, stored with a unique constraint in the same table and the same DB transaction as the balance update — so the database, not an application-level check, decides who wins a race. A duplicate gets the original response replayed, not an error, because to the provider an error means the bet failed. Rows are kept as a permanent ledger. If a refund arrives before its bet, I store a tombstone so the late bet is rejected."

## 11. Quest reward: sync hay Service Bus?
- Reward là **cộng tiền** (không có lỗi nghiệp vụ kiểu thiếu số dư), lỗi chỉ là tạm thời → **async qua queue hợp lý**: retry, DLQ, không làm chậm/khoá request. UI hiển thị "reward pending". Sync chỉ hợp khi ví cùng DB, cần thấy số dư ngay, lưu lượng thấp. Phải nói được **trade-off**, không trả lời một chiều.
- **SessionId = playerId (walletId):** Service Bus giao message cùng session **FIFO, mỗi lúc chỉ một consumer** → không cập nhật song song ví của cùng player, giữ thứ tự. SessionId **không** chống trùng.
- Chống cộng 2 lần (at-least-once): key = `(playerId, questId, period)` (quest lặp ngày/tuần cần period); **INSERT với UNIQUE trong cùng transaction** với cộng tiền. ❌ Lại lỗi "check exists rồi mới insert". Duplicate detection của Service Bus (theo MessageId, có cửa sổ thời gian) chỉ là lớp phụ.
- Ghi DB xong rồi gửi message, crash ở giữa → **mất thưởng = mất tiền của user**, không chấp nhận được. Pattern: **Transactional Outbox** (ghi quest completed + outbox row cùng transaction; relay đọc outbox gửi đi, at-least-once → consumer idempotent). MediatR/mediator là **in-process**, không liên quan độ bền.

> "Crediting a reward can't fail for business reasons, so I'd do it asynchronously over Service Bus with retries and a DLQ, and show it as pending. The session ID is the player ID, so one player's wallet updates are processed in order by a single consumer. Delivery is at-least-once, so the consumer inserts an idempotency key — player, quest, period — with a unique constraint in the same transaction as the credit. And to avoid losing the message if we crash after saving the completion, I use a transactional outbox: the completion and the outgoing message commit together."
