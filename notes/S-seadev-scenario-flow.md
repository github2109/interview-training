# SEADEV — Flow phỏng vấn theo tình huống (Scenario-based) và mổ xẻ dự án

> Viết 2026-11-10 theo kinh nghiệm Hiệp kể: interviewer **không hỏi định nghĩa** (React render thế nào, Redis là gì, ACID là gì) mà (1) bắt kể **một dự án bạn tự hào** rồi mổ xẻ, (2) **bịa tình huống** và chấm điểm theo **từng bước** bạn kể.
> Giải thích bằng tiếng Việt, **câu trả lời mẫu bằng tiếng Anh**. Chỗ chỉ Hiệp mới có câu chuyện thật: **[Hiệp điền]**. Chỗ Claude không chắc chi tiết hệ thống cũ: **[Hiệp xác nhận]**. Kiến thức nền chi tiết nằm ở `notes/S-seadev-master.md` (A6 lock SQL Server, C3 idempotency, C4 Redis, C5 outbox, C9 observability), file này là **kịch bản nói**.

---

## 0. Interviewer chấm điểm thế nào

### 0.1 Họ nghe gì trong mỗi câu trả lời
Một câu tình huống kiểu "API chậm, anh debug thế nào?" không có đáp án đúng duy nhất. Họ chấm **quá trình**:

| Bước | Mid hay nói | Senior nói | Điểm họ ghi |
|---|---|---|---|
| 1. Làm rõ / đo | "Em mở code xem chỗ nào chậm" | "Chậm là bao nhiêu, p50 hay p99, từ khi nào, ai bị, endpoint nào?" | Có **dữ liệu trước khi đoán** không |
| 2. Khoanh vùng | Đoán ngay "chắc do DB" | Dùng trace chia thời gian: app / DB / HTTP ngoài / chờ tài nguyên | Có **phương pháp** không |
| 3. Gọi tên vấn đề | "Nó bị chậm" | "Đây là N+1 / lock blocking / pool exhaustion / cache stampede" | Có **vốn từ kinh nghiệm** không |
| 4. Xác nhận bằng công cụ | Không nhắc | Query Store, execution plan, `dotnet-counters`, App Insights, `sys.dm_exec_requests` | Đã **thật sự làm** chưa |
| 5. Xử lý tạm | Sửa code luôn | Giảm thiệt hại trước: rollback, tăng pool, kill query, feature flag | Có **ưu tiên khách hàng** không |
| 6. Xử lý gốc | 1 cách | 2–3 cách kèm **trade-off**, chọn một, nói vì sao | Có **tư duy thiết kế** không |
| 7. Phòng ngừa | Không nhắc | Alert, test tải, review checklist, postmortem | Có **ownership** không |

Quy tắc vàng: **mỗi bước nói một câu, rồi hỏi "Should I go deeper into this step?"**. Nói 7 bước mỗi bước 2 câu (≈2 phút) tốt hơn nói sâu 1 bước 5 phút rồi bị cắt.

### 0.2 Họ đào sâu theo kiểu "rồi sao nữa" (failure chain)
Câu tình huống luôn có chuỗi follow-up kiểu **"what if X fails?"**: lock hết hạn thì sao → Redis failover thì sao → process bị GC pause thì sao. Câu trả lời Senior luôn kết bằng: **"so the final guarantee must come from the database (unique constraint / version check), the lock or the cache is only an optimisation"**. Hiệp đã có lỗi lặp lại **check-then-act** (progress.md), nên nhớ câu thần chú: **"INSERT with a UNIQUE constraint in the same transaction."**

### 0.3 Ranh giới trung thực khi kể
- Stack thật: **SQL Server** (PlaySweeps, Joblogic), **MySQL/MariaDB** (EIM, tool), **MongoDB** (Altar), **Cosmos DB** (Quest Engine). **PostgreSQL không phải kinh nghiệm chính** → khi bị hỏi Postgres, nói: *"I've mostly used SQL Server in production, but the principle in PostgreSQL is the same — write-ahead log — and here is how it differs…"*. Nói được khác biệt là điểm cộng, nhận bừa là điểm trừ.
- PlaySweeps: "sweepstakes gaming platform", không nói casino/real-money/DAU/doanh thu. Hiệp là **feature lead**, không phải team lead.
- Azure Functions/Event Hub: Hiệp **vận hành, cấu hình**, không tự dựng.
- Không bịa số. Không có số thật thì nói "roughly" hoặc **[Hiệp điền]**.

---

## PHẦN 1 — "Tell me about a project you're proud of" và chuỗi mổ xẻ

### 1.0 Chọn dự án nào
| Dự án | Vì sao nên chọn | Rủi ro |
|---|---|---|
| **Quest Engine V2 (PlaySweeps)** ⭐ | Hiệp làm **từ TDD đến production**, có đủ chất liệu bị đào: Cosmos DB, Redis lock, idempotency claim, làm việc với client Mỹ, công thức ncalc | Bị đào RedLock/fencing token → đã chuẩn bị câu tự phản biện |
| Pragmatic Play seamless wallet | Dính tiền, idempotency, refund-trước-bet, xác thực hash → hợp tình huống "retry không dup" | Ít phần "thiết kế từ đầu" (giao thức do Pragmatic định) |
| Job Spend Limit (Joblogic) | Hợp nghiệp vụ Ops Hub, có edge case PO thích | Làm cùng đồng nghiệp, phạm vi nhỏ hơn |

→ **Mở bằng Quest Engine V2.** Khi họ chuyển sang "tiền / retry", bắc cầu sang Pragmatic + Nexus.

### 1.1 Câu mở đầu (90 giây) — học thuộc khung, không học thuộc chữ
> The project I'm most proud of is **Quest Engine V2** at PlaySweeps, a US sweepstakes gaming platform with over two million registered players, built for PLAYSTUDIOS.
>
> **Problem:** the business wanted personalised quests — missions like "spin 50 times" or "win in three different games this week" — with rewards, and they wanted to change the rules without a release. The first version couldn't do that well. [Hiệp xác nhận: V1 thiếu gì — ví dụ quest cứng trong code / không cá nhân hoá được]
>
> **My role:** I was the feature lead. I clarified the requirements with the client — they owned the reward formulas, which we evaluated with NCalc — wrote the technical design document, implemented the backend in .NET 8, and took it through to production.
>
> **Design in one breath:** game events come in, the engine finds the quests that apply to that player, updates progress stored in Cosmos DB, and when a quest is complete the player can claim the reward. Updates for the same player are serialised with a Redis lock, and the claim uses an idempotency key, so a retry or a double click can never pay twice.
>
> **Result:** it went live and [Hiệp điền: một con số / kết quả — số quest đang chạy, số claim/ngày, live ops tự tạo quest không cần release, không có sự cố trả thưởng 2 lần…].
>
> **Why I'm proud:** it was the first feature I owned end to end, from an unclear request to a running system, and I had to make real trade-offs about consistency and money-like rewards.

Mẹo: kết bằng một **móc câu** mà mình muốn bị hỏi ("trade-offs about consistency"). Interviewer thường cắn đúng móc đó.

### 1.2 Chuỗi đào sâu dự kiến (theo thứ tự hay gặp)

**F1. "Walk me through the architecture. Draw it."**
Vẽ 5 hộp: *Game events → Quest Engine API/handler → Redis (lock) → Cosmos DB (quest definitions + player progress) → Claim → Reward service (Nexus / balance) [Hiệp xác nhận đường trả thưởng]*. Thêm App Insights ở góc.
> Events from gameplay reach the engine [Hiệp xác nhận: qua HTTP từ game server hay qua Event Hub/Service Bus]. For each event we load the player's active quests, evaluate whether the event matches each quest's condition, and update progress. Quest definitions are configured by live ops; player progress is a document per player [Hiệp xác nhận: per player hay per player-quest] in Cosmos DB. When a quest completes, it becomes claimable; the claim endpoint grants the reward exactly once.

**F2. "Why Cosmos DB and not SQL Server, which you already had?"**
Senior: nói lý do + cái giá phải trả, không nói "vì nó nhanh".
> Progress is naturally a document: a player has a set of quests, each with a different shape of progress — counters, lists of distinct games, streaks. Storing that as a JSON document partitioned by player ID means one point read and one write per event, without a schema migration each time the business invents a new quest type. The cost is that Cosmos gives us no joins and no multi-document transactions across partitions, so anything that must be atomic has to live inside one player's partition, and reporting has to go elsewhere. [Hiệp xác nhận: lý do thật team chọn Cosmos — nếu do có sẵn thì nói thẳng "it was already in our platform for feature state, and it fitted because…"]

Follow-up hay gặp: *"What is your partition key and why?"* → `playerId`: mọi thao tác đều theo player, tránh cross-partition query; rủi ro **hot partition** chỉ khi một player bắn cực nhiều event — không xảy ra với người thật, có thể xảy ra với bot (→ rate limit).

**F3. "Why do you need a lock at all?"**
Bản chất: hai event của **cùng một player** đến gần như cùng lúc (2 spin trên 2 instance) → cả hai đọc progress = 49, cùng ghi 50 → mất một lượt (**lost update**).
> Two events for the same player could be processed on two instances at the same time. Both read progress 49, both write 50, and we lose one increment — a classic lost update. The lock serialises updates per player, so the second event reads 50 and writes 51.

**F4. "Is a Redis lock enough? What if the lock expires while you're still working?"** (câu Senior quan trọng nhất)
> No, and that's what I'd change if I did it again. A Redis lock is a lease with a TTL. If the holder pauses — a long GC pause, a slow Cosmos call — past the TTL, a second instance acquires the lock and both write. Redis also replicates asynchronously, so if the primary fails over right after granting a lock, the replica may not know about it. Martin Kleppmann's point about Redlock is exactly this: there's no fencing token. The fix is to make the store the arbiter: Cosmos supports optimistic concurrency with the document's ETag — we read the document with its ETag and write with an If-Match condition, so a stale writer gets 412 Precondition Failed and retries. Then the lock is only there to reduce contention, not for correctness. [Hiệp xác nhận: code có dùng ETag/If-Match không — nếu có, đổi câu thành "we also used the ETag, so…", điểm cộng lớn]

**F5. "How does the claim avoid paying twice?"**
> The claim has an idempotency key — [Hiệp xác nhận: key là gì, ví dụ playerId + questId + cycle/period]. The first claim records the key and the result atomically with marking the quest as claimed; a retry with the same key gets the stored result back instead of a second reward. The important part is that the check and the write are a single atomic operation — a conditional write or a unique key — not "read, check, then write", because two concurrent requests could both pass the check.

**F6. "The reward is credited in another service. What if you mark the quest claimed and then the credit call fails?"**
Đây là câu **dual write**. Senior đặt tên và nêu 2 hướng:
> That's a dual-write problem: two systems, no shared transaction. There are two safe orders. Either we record the claim as "pending" first, call the reward service with the same idempotency key, then mark it "completed" — and a background job retries pending claims, which is safe because the reward service deduplicates by that key. Or we write the claim and an outbox message in the same atomic write and a worker delivers it. What we must never do is credit first without a key, because a retry would pay twice. [Hiệp xác nhận: thực tế Quest Engine làm cách nào; nếu sync và không có retry job thì nói trung thực: "we called it synchronously and relied on the key for retries from the client; a reconciliation job is something I'd add"]

**F7. "How did you test it?"**
> Unit tests with xUnit and Moq around the rule evaluation and the claim rules — progress per quest type, boundaries like exactly reaching the target, expired quests, claiming twice. [Hiệp điền: số test / có integration test với Cosmos emulator không]. For concurrency, unit tests aren't enough, so [Hiệp điền: đã test song song thế nào, hoặc nói "I'd add a test that fires parallel events for one player and asserts the final count"].

**F8. "How did you know it worked in production?"**
> Application Insights for exceptions and latency of the event handler and the claim endpoint, plus BI events in Splunk so we could follow a player's journey when someone reported a missing reward. [Hiệp điền: alert nào, có dashboard không]

**F9. "What went wrong?" / "What was the hardest bug?"**
**[Hiệp điền: một chuyện thật]** — gợi ý khung: *triệu chứng (player báo thiếu thưởng / progress nhảy sai) → công cụ (Splunk hành trình, App Insights trace) → nguyên nhân → fix → phòng ngừa*. Nếu không có bug lớn, nói về **requirement mơ hồ** với client: công thức ncalc chưa rõ biên (">=" hay ">"), múi giờ reset quest hằng ngày/tuần (US có nhiều múi giờ — reset theo UTC hay theo giờ player?) [Hiệp xác nhận].

**F10. "What would you change?"**
1. DB làm trọng tài (ETag / conditional write) thay vì dựa vào lock (F4).
2. Outbox / pending + reconciliation cho trả thưởng (F6).
3. Đo và alert theo nghiệp vụ: "claim pending > 5 phút", không chỉ exception.

**F11. "Your traffic grows 10x. What breaks first?"**
> Probably the lock and the per-event read-modify-write on one player's document. Ten times the events means more lock contention per player and more RU consumption in Cosmos. I'd first measure RU per event and lock wait time. Options: process a player's events in order through a partitioned queue — a Service Bus session or an Event Hub partition keyed by player ID — so we don't need a distributed lock at all, because one consumer owns that player at a time; and batch several events into one document write. The trade-off is added latency: progress updates become eventually consistent by a second or two, which is fine for quests but not for a balance.

**F12. "How would this experience help you at SEADEV / Ops Hub?"**
> Ops Hub also turns business rules into a system — quotes, payment schedules, approvals — and money is involved. The habits carry over: clarify the rules with the business before coding, make the database guarantee correctness, make every payment-like operation idempotent, and add monitoring that speaks in business terms.

### 1.3 Câu đào sâu "bắt bài" và cách đỡ
| Họ hỏi | Ý đồ | Đỡ thế nào |
|---|---|---|
| "What exactly did *you* do vs the team?" | Kiểm tra có thổi phồng không | Tách rõ: client định công thức; Hiệp làm rõ requirement, viết TDD, code backend, release. Ai review TDD [Hiệp điền] |
| "Why NCalc and not hard-coded rules?" | Trade-off linh hoạt vs an toàn | Business đổi luật không cần release; giá: biểu thức sai chạy runtime mới lỗi → validate khi lưu config, test biểu thức, giới hạn hàm được dùng |
| "What happens if live ops configures a broken formula?" | Failure mode | Validate + dry-run khi lưu; runtime lỗi thì quest đó bị bỏ qua và log, không làm hỏng event của quest khác [Hiệp xác nhận] |
| "How long did it take, how many people?" | Ước lượng, quy mô | [Hiệp điền] |
| "If you had to do it in SQL Server?" | Hiểu cả hai | Bảng `PlayerQuestProgress (PlayerId, QuestId, Period) PK`, update atomic `SET Progress = Progress + 1 WHERE … AND Progress < Target`, bảng `QuestClaims` UNIQUE(PlayerId, QuestId, Period) → không cần Redis lock |

### 1.4 Dự án dự phòng: Pragmatic Play wallet (khi họ hỏi "something with money")
> At PlaySweeps I owned the Pragmatic Play seamless-wallet integration. In a seamless wallet the game provider holds no balance; every bet, win, refund, promo win, free spin and buy-bonus is an HTTP callback to us, and we must answer with the new balance. Three things made it hard. First, security: every callback is signed, so we verify the hash before doing anything. Second, retries: the provider retries on timeout, so every callback must be idempotent — we deduplicate on the provider's transaction reference, and if we've seen it we return the original response instead of an error. Third, ordering: a refund can arrive for a bet we never processed, or a result can arrive while the bet is still pending, so we lock the pending wager and handle those cases explicitly.

Follow-up đã có đáp án ở PHẦN 2, S5 (idempotency). Chỗ cần điền: **[Hiệp xác nhận: key thật là transaction reference hay roundId — code có `GetByRoundIdAsync`; nếu dedupe bằng roundId thì nói: "we looked up by round, and I'd make the key the provider's transaction reference, because one round can have several transactions"]**.

---
## PHẦN 2 — Tình huống (Scenario questions)

Mỗi tình huống có: **bản chất (tiếng Việt)** → **câu hỏi mở** → **trả lời mẫu theo bước** → **chuỗi follow-up** → **bảng chấm Mid/Senior**.

---

### S1. "Users say the app is slow. How do you debug it?"

**Bản chất.** Thời gian của một request chỉ có hai loại: **đang tính (CPU)** hoặc **đang chờ** (DB, lock, mạng, connection pool, thread pool). Debug performance = tìm xem thời gian **nằm ở đâu**, rồi gọi tên vấn đề. Interviewer chấm điểm việc bạn **đo trước, đoán sau**.

**Trả lời mẫu (7 bước, ~2 phút):**
> **1. Clarify and measure.** First I'd turn "slow" into numbers: which page or endpoint, how slow — p50 or p99 — since when, and for whom: everyone, one tenant, one region, mobile only? "Since yesterday's deploy" and "only at 9 a.m." point to very different causes.
>
> **2. Frontend or backend?** I'd open the browser DevTools network tab. If the API call itself takes 4 seconds, it's the backend. If the API returns in 200 ms but the page still feels slow, it's the frontend — large bundles, too many sequential requests, or heavy rendering — and I'd use the Performance tab and Lighthouse.
>
> **3. Locate the time on the backend.** I'd open a distributed trace in Application Insights for a slow request and see which span takes the time: our code, a SQL query, an external HTTP call, or a gap where nothing is happening — a gap usually means waiting for a thread or a connection.
>
> **4. Name the problem and confirm it with a tool.**
> – Many small identical queries → N+1; confirm in the trace or with EF logging.
> – One slow query → check the actual execution plan and Query Store: missing index, a scan, or a plan regression from parameter sniffing.
> – Query fast alone but slow in production → blocking; check `sys.dm_exec_requests` for `blocking_session_id` and wait types like `LCK_M_X`.
> – CPU low but everything slow → thread-pool starvation or connection-pool exhaustion; check `dotnet-counters` for thread-pool queue length and the "max pool size reached" timeout.
> – CPU high in the app → profile with `dotnet-trace`; memory climbing → `dotnet-dump` and GC counters.
>
> **5. Mitigate first.** If customers are hurting, I'd reduce the damage before the perfect fix: roll back the deploy, turn off the feature flag, kill the blocking query, or scale out if it's pure load.
>
> **6. Fix the root cause**, with trade-offs: add the right index — but indexes slow down writes; batch the N+1 into one query; cache a read-heavy result — but now we must handle invalidation; move slow work like PDF generation to a background job.
>
> **7. Prevent it.** Add an alert on p99 latency for that endpoint, a performance check in code review for queries in loops, and, for important flows, a load test before release. And I'd write a short postmortem.

**Chuỗi follow-up:**

**F1. "The CPU on the server is 5%, but requests take 8 seconds."**
> Low CPU means the request is waiting, not computing. I'd check four things in order: the database — a slow query or a lock wait; an external HTTP call without a timeout; the connection pool — if requests wait for a free connection, I'd see "timeout expired… max pool size was reached"; and the thread pool — sync-over-async like `.Result` blocks threads, the pool injects new threads slowly, and requests queue. `dotnet-counters` shows `threadpool-queue-length` growing and `threadpool-thread-count` creeping up.

**F2. "p50 is 100 ms but p99 is 6 seconds."**
> The average request is fine; a minority is slow. That usually means something specific to those requests: a large tenant with much more data, a cold cache, a plan compiled for a small parameter but used for a large one — parameter sniffing — lock waits that only happen under contention, or GC pauses. I'd filter traces to the slow ones and look for what they have in common — the same tenant, the same parameter, the same time.

**F3. "It only happens at 9 a.m. every day."**
> Time-based means a load or a job: everyone logs in, a scheduled report or batch job runs, or a cache expires at the same time for everyone. I'd overlay the slow periods with job schedules and request rate. If a nightly-style job runs during business hours and holds locks, I'd move it, chunk it into small batches, or run it against a read replica.

**F4. "It became slow right after a deploy, but the code change looks harmless."**
> I'd compare before and after in Application Insights for the same endpoint, and check for a new query or a changed query. A harmless-looking change can change the plan — for example, a parameter type mismatch like `nvarchar` against a `varchar` column causes an implicit conversion and an index scan. Query Store can show the plan change and lets me force the old plan as a quick mitigation while I fix the code. If I can't find it fast, I roll back first.

**F5. "The database CPU is at 100%."**
> I'd find the top queries by CPU in Query Store or `sys.dm_exec_query_stats`. Usually one or two queries dominate: a scan because of a missing index or a non-sargable predicate like `WHERE YEAR(CreatedAt) = 2026`, or a query called far too often — N+1 or a missing cache. Quick fix: add the index or force a good plan; root fix: rewrite the query and make it sargable.

**F6. "How do you know your fix worked?"**
> Same metric, same percentile, before and after — for example p99 for that endpoint dropped from 6 seconds to 300 ms over a full day including the 9 a.m. peak — and the logical reads of the query dropped. "It feels faster" isn't evidence.

**F7 (frontend, nếu SA gốc FE hỏi). "The API is fast but the React page is slow."**
> I'd separate loading from interacting. For loading: bundle size, number of round trips — a waterfall of requests that could run in parallel — and images; Lighthouse and the LCP metric. For interaction lag, I'd record with the React DevTools Profiler to see which components re-render and how long they take; typical causes are a large list without virtualisation, state stored too high so one keystroke re-renders the whole page, or new object references every render that break memoisation. I measure first, then fix the component that actually costs time.

**Chuyện thật để gắn:** **[Hiệp điền: một lần debug chậm thật — gợi ý tối ưu fetch/cache AVA config ở PlaySweeps: trước/sau bao nhiêu ms, đo bằng gì]**. Nói 1 câu chuyện thật sau 7 bước = điểm Senior.

| Mid | Senior |
|---|---|
| Đọc code đoán chỗ chậm, "thêm cache", "thêm index" | Đo p50/p99, từ khi nào, ai bị → trace → gọi tên → công cụ xác nhận → giảm thiệt hại → fix có trade-off → alert + postmortem |
| Không phân biệt FE/BE | Network tab tách FE/BE trong 30 giây |
| "Scale thêm server" | Biết scale không cứu được lock/DB/N+1, còn làm nặng DB thêm |

---

### S2. "How does a distributed lock in Redis work? What can go wrong?"

**Bản chất.** Redis chạy lệnh **một luồng**, nên `SET key value NX PX 30000` là **nguyên tử**: chỉ một client tạo được key. Lock thực chất là **hợp đồng thuê có hạn (lease)**: TTL để lock không bị giữ mãi khi process chết; nhưng chính TTL làm lock **không an toàn tuyệt đối** — hết hạn khi việc chưa xong thì hai người cùng giữ.

**Trả lời mẫu:**
> **Acquire:** `SET lock:player:42 <random-token> NX PX 30000` — set only if not exists, with a 30-second expiry. Redis executes commands one at a time, so only one client succeeds. The token is a random value unique to this holder.
>
> **Release:** I can't just `DEL` the key, because my lock may have expired and someone else may hold it now. Release is a Lua script that deletes the key only if its value is still my token — compare and delete atomically.
>
> **Why the TTL:** if the holder crashes, the lock frees itself after 30 seconds instead of blocking everyone forever.
>
> **What can go wrong:**
> 1. **The lease expires while I'm still working** — a GC pause, a slow DB call, a network stall. Another process takes the lock and now two processes are in the critical section. Auto-extension — a watchdog that renews the TTL while work is running, which RedLock.net supports — reduces this but can't remove it: a paused process can't renew either.
> 2. **Failover.** Redis replication is asynchronous. If the primary grants my lock and crashes before replicating it, the promoted replica has no lock, and a second client gets it.
> 3. **Clock and timing assumptions.** The Redlock algorithm — acquire on a majority of five independent Redis nodes within a time budget — fixes the single-node failover issue, but it still relies on bounded pauses and clock drift. Kleppmann's critique is that it has no **fencing token**.
>
> **Fencing token** means the lock service gives an increasing number with each grant, and the storage rejects writes with an older number. Redis locks don't give you that, so for correctness I rely on the database: an optimistic concurrency check — `rowversion` in SQL Server, an ETag in Cosmos — or a unique constraint. The Redis lock then only reduces contention and duplicate work.
>
> **When I use it:** to avoid doing expensive work twice — rebuilding a cache entry, running a scheduled job on one instance — or to serialise operations per key when an occasional double execution is detected downstream anyway. At PlaySweeps we used Redis locks per player and game for spins, per transaction for deposits and redemptions, and per player for PrizeOut, with the money itself protected by the balance owner's idempotency check.

**Chuỗi follow-up:**

**F1. "How do you choose the TTL?"**
> Longer than the p99.9 of the protected work, with margin — if the work takes up to 2 seconds, maybe 10–30 seconds. Too short and it expires mid-work; too long and a crashed holder blocks that key for the whole TTL. If the work time is unpredictable, use a shorter TTL with auto-renewal, and put a timeout on the work itself so it can't run past the lease.

**F2. "What does a request do when it can't get the lock?"**
> Depends on the business. For a user action like a claim, fail fast with 409 or "please retry", or wait briefly with a small bounded retry and jitter — never spin in a tight loop. For a cache rebuild, the losers shouldn't wait at all; they serve the stale value. For a background job, skip this run because another instance is doing it.

**F3. "Redis is down. What happens to your locks?"**
> That's a design decision I'd make explicitly: fail closed — reject the operation — or fail open — proceed without the lock. If correctness is guaranteed by the database constraint, failing open is acceptable because the lock was only an optimisation. If the lock was the only protection, Redis being down means we either stop or risk duplicates — which is another argument for not making the lock the only protection.

**F4. "Why not just use a database lock?"**
> Often I would. If the data is in one SQL database, a row lock — `SELECT … WITH (UPDLOCK, ROWLOCK)` in SQL Server or `SELECT … FOR UPDATE` in PostgreSQL — or an application lock like `sp_getapplock` or `pg_advisory_xact_lock` is tied to the transaction: when the transaction commits or the connection dies, the lock is released, and there's no TTL race. The cost is holding a connection and a transaction while you wait. Redis locks make sense when the work spans several systems or no single database is involved.

**F5. "Is a Redis lock re-entrant?"**
> Not by default. If the same code path tries to acquire it again, it blocks itself until the TTL expires. You'd need to track the token per execution flow; usually it's simpler to design so the lock is taken once at the boundary.

**F6. "Two locks in opposite order?"**
> Distributed deadlock: request A holds lock X and waits for Y, B holds Y and waits for X. TTLs eventually break it, but slowly. Prevent it by always acquiring locks in a fixed order — for example sorted by key — or by taking only one lock per operation.

| Mid | Senior |
|---|---|
| "SETNX rồi DEL" | `SET NX PX` + token ngẫu nhiên + Lua compare-and-delete |
| Không nhắc lease hết hạn | Nêu GC pause, failover async, không có fencing token |
| Lock = đảm bảo đúng | Lock = tối ưu; **DB constraint / version là trọng tài** |
| Không biết khi nào không dùng | Cùng 1 DB → dùng lock DB/atomic UPDATE; chọn fail-open/fail-closed rõ ràng |

---

### S3. "A hot cache key is invalidated and 1 million requests hit it at the same moment. What happens and how do you protect the system?"

**Bản chất.** Đây là **cache stampede** (thundering herd / dog-piling). Key hết hạn → tất cả request đều cache miss → tất cả cùng query DB để dựng lại cùng một giá trị. Ví dụ con số: key "home page config" được đọc **20.000 req/s**; dựng lại mất **500 ms** → trong 500 ms đó có **~10.000 request** cùng miss và cùng bắn query vào DB. DB chịu được 500 query/s → nghẽn, query chậm lên 5 s → càng nhiều request miss hơn → **sụp dây chuyền** (cascading failure). Và 1 triệu request là con số để bạn **không thể** để chúng chạm DB.

**Trả lời mẫu (theo lớp phòng thủ):**
> First, name it: this is a **cache stampede**. When the key disappears, every request misses at the same time and all of them try to rebuild the same value from the database. If rebuilding takes 500 ms and we get 20,000 requests a second, that's around 10,000 identical queries in half a second — the database slows down, the rebuild takes even longer, and it cascades.
>
> I'd protect it in layers:
>
> **1. Only one request rebuilds — request coalescing.** Inside one instance, a single-flight: concurrent misses for the same key await the same `Task` instead of each querying — in .NET, a `ConcurrentDictionary<string, Lazy<Task<T>>>`, or `HybridCache` in .NET 9, which has this built in. Across instances, a short Redis lock on `rebuild:<key>`: the winner rebuilds, the others don't go to the database. With 50 instances, that's at most 50 queries instead of a million — or one, with the distributed lock.
>
> **2. Losers serve stale data — don't make them wait.** Store the value with a soft expiry inside it and a longer hard TTL in Redis. After the soft expiry, the first request triggers a background refresh and everyone, including that request, keeps getting the slightly stale value. So users never see the miss. This is stale-while-revalidate.
>
> **3. Don't let keys expire together.** Add jitter to TTLs — 10 minutes plus or minus a random minute — so keys created at the same time don't expire at the same time. For one very hot key, refresh it before it expires — refresh-ahead, or probabilistic early expiration, where each request has a small chance of refreshing early that grows as the expiry approaches.
>
> **4. Invalidate by replacing, not deleting.** When the data changes, write the new value into the cache instead of deleting the key, so there's never a window with no value.
>
> **5. Protect the database anyway.** A bulkhead — a limit on concurrent rebuild queries — and a circuit breaker, so if the database is struggling we serve stale data or a default instead of piling on.
>
> **6. Hot key itself.** A million requests on one Redis key all hit one shard. I'd add a small in-memory cache in each instance — even 5–10 seconds — so Redis sees a few requests per instance per period instead of every request.

**Chuỗi follow-up:**

**F1. "The instance holding the rebuild lock crashes."**
> The rebuild lock has a short TTL — a few seconds, slightly longer than the rebuild time — so another instance takes over after it expires. Meanwhile everyone is still served the stale value, so users don't notice. That's why stale-while-revalidate matters more than the lock.

**F2. "There's no stale value — it's the very first request after a deploy, or Redis was flushed."**
> Then the losers must wait — but on the single in-flight rebuild, with a timeout, not each on its own query. If the rebuild fails or times out, return a sensible default or a 503 with retry-after rather than letting a million requests through. For planned events like deploys, warm the cache before taking traffic.

**F3. "How stale is acceptable?"**
> That's a business question I'd ask the PO. A home-page banner can be a minute stale. A price or a balance can't be served from a cache like this at all — for money I read from the source of truth, or use the cache only for display with the real check at write time.

**F4. "You need to invalidate 100,000 keys at once — for example, a pricing change for all products."**
> Don't delete them all at once; that creates a stampede on 100,000 keys. Options: versioned keys — put a version number in the key, bump it, and old keys expire naturally while new ones fill gradually; or refresh in the background in batches; and serve stale until each is refreshed.

**F5. "Cache and database are inconsistent after an update. Which do you update first?"**
> The usual safe pattern is cache-aside: write the database first, then delete or replace the cache key. If you update the cache first and the DB write fails, the cache holds a value that never existed. Even DB-first has a small race — a reader can put an old value back right after you delete — so keep a TTL as a safety net, and for important keys use versioning or delete again after a short delay.

**F6. "Redis itself goes down."**
> The app must treat the cache as optional: short timeouts on Redis calls, a circuit breaker so we don't wait on a dead Redis for every request, and fall back to the in-memory layer plus a rate-limited path to the database. If the database can't take the full load without the cache, that's a capacity risk I'd raise — the cache has become a dependency, not an optimisation.

| Mid | Senior |
|---|---|
| "Tăng TTL", "dùng lock" | Gọi tên **cache stampede**, tính con số, phòng thủ nhiều lớp |
| Lock rồi bắt mọi request chờ | Single-flight trong process + lock phân tán + **serve stale** |
| Xoá key khi cập nhật | Ghi đè giá trị mới, versioned key, TTL jitter |
| Quên hot key / Redis down | L1 in-memory cache, circuit breaker, cache là optional |

**Chuyện thật để gắn:** **[Hiệp điền: AVA remote config ở PlaySweeps — config đọc rất nhiều, đã cache thế nào, có từng bị hết hạn đồng loạt không]**.

---
### S4. "What kinds of locks does a database have? How does each work, when do you use it, and what's the trade-off?"

**Bản chất.** Lock là cách DB giữ **Isolation** khi nhiều transaction chạm cùng dữ liệu. Có 3 trục để trả lời gọn: (1) **chế độ (mode)**: đọc chung hay ghi độc quyền; (2) **phạm vi (granularity)**: dòng, trang, bảng, khoảng key; (3) **cách dùng ở tầng ứng dụng**: pessimistic (khoá trước) vs optimistic (kiểm tra version lúc ghi). Hiệp làm **SQL Server** → nói SQL Server trước, rồi đối chiếu PostgreSQL.

**Trả lời mẫu:**
> I'd group them by mode, by granularity, and by how the application uses them. I've worked mostly with SQL Server, so I'll start there and say where PostgreSQL differs.
>
> **Modes in SQL Server:**
> – **Shared (S)** — taken by reads under the default READ COMMITTED; many readers can hold it, but it conflicts with writers. Normally released as soon as the row is read.
> – **Exclusive (X)** — taken by INSERT, UPDATE, DELETE and held until the transaction ends. Nobody else can modify that row, and under locking READ COMMITTED nobody can read it either.
> – **Update (U)** — taken when a statement reads a row it intends to update. Only one transaction can hold U on a row, which prevents the classic conversion deadlock where two transactions both hold S and both wait to upgrade to X. I use it explicitly with `WITH (UPDLOCK)` for read-then-update.
> – **Intent locks (IS, IX, SIX)** — placed on the page and table above a row lock, so the engine can quickly tell that someone holds row locks before granting a table lock.
> – **Schema locks** — Sch-S while a query runs, Sch-M for DDL like ALTER TABLE; Sch-M blocks everything on that table.
> – **Key-range locks** — under SERIALIZABLE, they lock the gap between index keys so no one can insert a row that would change my query's result — that's how phantoms are prevented.
>
> **Granularity:** row or key, page, table. Fine-grained locks give more concurrency but cost memory; SQL Server escalates to a table lock when one statement takes around five thousand locks on one object, which is why a big `UPDATE` without batching can suddenly block the whole table.
>
> **PostgreSQL differs** in two useful ways: readers never block writers and writers never block readers, because of MVCC — readers see a snapshot — so there's no shared lock for normal reads; and it has explicit row-lock modes — `FOR UPDATE`, `FOR NO KEY UPDATE`, `FOR SHARE`, `FOR KEY SHARE` — eight table-level lock modes, advisory locks, and it never escalates. SQL Server can get similar reader behaviour with Read Committed Snapshot Isolation.
>
> **Application level:**
> – **Pessimistic** — lock the row first, `SELECT … WITH (UPDLOCK, ROWLOCK)` or `FOR UPDATE`, then update. Correct and simple under high contention on the same row, but it holds locks and connections while you work, and you risk deadlocks.
> – **Optimistic** — no lock while reading; on write, check a version: `UPDATE … WHERE Id = @id AND RowVersion = @v`; zero rows affected means someone else changed it, so retry or show a conflict. Great when conflicts are rare, like two office users editing a quote; poor when many writers fight over one row, because most retries fail.
> – **Atomic conditional update** — often the best: `UPDATE Balances SET Amount = Amount - @x WHERE PlayerId = @p AND Amount >= @x` — one statement, the check and the write are atomic, no read-then-write gap.
> – **Unique constraint** — the strongest duplicate protection; the database guarantees it regardless of timing.

**Chuỗi follow-up (theo tình huống):**

**F1. "Two customers try to book the last delivery slot at the same time."** (nghiệp vụ Ops Hub)
> I'd avoid read-check-insert. Either an atomic update — `UPDATE Slots SET Booked = Booked + 1 WHERE SlotId = @id AND Booked < Capacity` and check rows affected — or, if one slot is one booking, a unique constraint on the slot so the second insert fails and we tell that customer the slot is gone. No explicit lock needed.

**F2. "Two transactions deadlock. What do you do?"**
> The database detects the cycle and kills one as the victim — error 1205 in SQL Server, `deadlock detected` in PostgreSQL. First, retry the victim transaction, because a deadlock is transient. Then find the cause: in SQL Server the `system_health` Extended Events session keeps the deadlock graph showing both statements and the resources. Typical fixes: access tables and rows in the same order in every code path, keep transactions short — no HTTP calls inside them — add an index so updates touch fewer rows, and use UPDLOCK for read-then-update.

**F3. "Multiple workers take jobs from a table. How do you stop two workers taking the same job without them blocking each other?"**
> Lock the row while claiming, but skip rows already locked. In SQL Server: `UPDATE TOP (1) Jobs WITH (ROWLOCK, READPAST, UPDLOCK) SET Status = 'Processing', LockedUntil = … OUTPUT inserted.* WHERE Status = 'Pending'`. In PostgreSQL: `SELECT … FOR UPDATE SKIP LOCKED LIMIT 1`. Each worker gets a different row without waiting. Add a lease time so a job claimed by a crashed worker becomes available again.

**F4. "A long report query makes the order screen freeze."**
> Under locking READ COMMITTED, the report's shared locks and the writers' exclusive locks block each other — or the report scans so much that it escalates. Options: enable Read Committed Snapshot so readers read row versions and don't block — the cost is tempdb version-store load; run the report on a read replica; or add an index so it doesn't scan. I would not use NOLOCK on anything involving money, because it can read uncommitted or even double-count rows during page splits.

**F5. "You add a column to a big table in production and the whole app stops."**
> DDL needs a schema-modification lock — Sch-M in SQL Server, ACCESS EXCLUSIVE in PostgreSQL. It has to wait for running queries, and while it waits, every new query queues behind it — so one long-running report plus one ALTER can freeze the table. Mitigation: set a lock timeout on migrations so they fail fast instead of queuing everyone, run them off-peak, and prefer metadata-only changes — adding a nullable column, or a column with a default in recent versions, is a metadata-only change in PostgreSQL 11+ and in SQL Server Enterprise edition.

**F6. "Optimistic or pessimistic for a player's balance?"**
> Neither, ideally: an atomic conditional update in one statement. If there's logic between read and write, then pessimistic for a hot row like a balance, because with optimistic locking many concurrent writers would keep failing and retrying. Optimistic for things people edit rarely at the same time, like a quote or a customer record — with a clear "someone else changed this" message.

**Liên hệ thật:** PlaySweeps lock Redis theo (player, game) cho spin, theo transaction cho deposit/redemption, theo player cho PrizeOut; balance Sweeps Coin do **Nexus** giữ, SP của Nexus kiểm idempotency rồi kiểm số dư và cập nhật. Nếu bị hỏi "vì sao lock Redis mà không lock DB": **[Hiệp xác nhận lý do thật]**; câu an toàn: *"The balance owner, Nexus, protected correctness in its stored procedure; our Redis locks prevented duplicate concurrent work on our side, like two spins for the same player and game."*

| Mid | Senior |
|---|---|
| "Có shared lock và exclusive lock" | Mode (S/X/U/intent/schema/key-range) + granularity + escalation + khác biệt PostgreSQL/MVCC |
| Luôn dùng lock | Ưu tiên atomic UPDATE và UNIQUE; optimistic khi ít xung đột; pessimistic khi dòng nóng |
| Deadlock: "tăng timeout" | Retry victim, đọc deadlock graph, thống nhất thứ tự, transaction ngắn |
| NOLOCK để hết chậm | Biết NOLOCK đọc dữ liệu chưa commit/đếm trùng → dùng RCSI hoặc replica |

---

### S5. "A client times out and retries a payment. How do you make sure it isn't charged twice?"

**Bản chất.** Mạng không cho bạn biết request **đã chạy hay chưa** khi bị timeout. Client buộc phải retry → server phải **idempotent**: chạy N lần = chạy 1 lần. "Exactly-once" qua mạng không tồn tại; cái làm được là **at-least-once + dedupe** = hiệu quả như exactly-once. Lỗi Hiệp hay mắc: **check ngoài transaction** và **trả lỗi khi trùng** thay vì trả lại kết quả cũ.

**Trả lời mẫu:**
> Timeouts are ambiguous: the client doesn't know if the payment happened, so it must be able to retry safely. I'd make the operation idempotent with an **idempotency key**.
>
> **1. The client generates the key** — a UUID per logical payment, created once when the user clicks Pay, and reused on every retry. Not per HTTP attempt.
>
> **2. The server stores the key with a unique constraint, in the same transaction as the business change.** For example, a table `IdempotencyKeys (Key PK, RequestHash, Status, ResponseBody, CreatedAt)`. Inside one transaction: insert the key; if the insert fails on the unique constraint, it's a duplicate; otherwise do the payment work and save the response. The unique constraint is what makes it safe — "check if it exists, then insert" is a race, because two concurrent retries can both see "not exists".
>
> **3. On a duplicate, return the original response**, not an error. If the first attempt succeeded, the retry gets the same 200 and the same payment ID. If the first attempt is still running, return 409 or "in progress" so the client retries later.
>
> **4. Check the payload.** Store a hash of the request; the same key with a different amount is a client bug — reject it with 422 instead of silently returning the old result.
>
> **5. Pass the key downstream.** If we call a payment provider, send the same key or a key derived from it — Stripe, for example, accepts an `Idempotency-Key` header — so our retry to them is also safe.
>
> **6. Expire keys** after a window longer than any client's retry period — say 24 hours to a few days.
>
> At PlaySweeps this was everyday work: in the Pragmatic Play wallet, the provider retries callbacks, so we deduplicated on its transaction reference and replayed the original response; and every balance change we sent to Nexus carried a transaction GUID that Nexus checked in the same stored procedure that updated the balance.

**Chuỗi follow-up:**

**F1. "Two retries with the same key arrive at exactly the same millisecond."**
> Both try to insert the key; the unique constraint lets exactly one succeed. The other gets a duplicate-key error and either waits briefly and returns the stored response, or returns 409 "in progress". No lock needed — the database decides.

**F2. "The server committed the payment but crashed before sending the response."**
> The client times out and retries with the same key. The key is already committed with the response, so we return the stored response. That's exactly the case idempotency exists for.

**F3. "We call an external provider, it charges the card, then we crash before saving anything."**
> This is the dangerous order, so I'd record the intent first: commit a row "payment pending, key K" before calling the provider, then call the provider with key K, then mark it completed. If we crash in the middle, a recovery job finds pending payments and asks the provider "what happened with K?" — or retries with K, which the provider deduplicates. Without a key at the provider, we'd need reconciliation against their report.

**F4. "Who generates the key, the client or the server?"**
> The client, because only the client knows that two HTTP requests are the same intent. If the server generated it, a retry would look like a new payment. For server-to-server events, the producer's event ID is the key.

**F5. "Can't you just use the order ID or round ID as the key?"**
> Only if the operation can happen once per order. If one order can have several payments — a deposit and a balance payment — or one game round has a bet and several wins, the key must identify the operation, not the parent. Too coarse a key rejects legitimate operations; too fine a key, like a timestamp, doesn't catch retries.

**F6. "What about a message consumer — Service Bus delivers the same message twice?"**
> Same idea on the consumer side, sometimes called an inbox: a `ProcessedMessages` table with the message ID as the primary key, inserted in the same transaction as the side effect. If the insert fails, we've done it already, so we just complete the message. Or make the operation naturally idempotent — "set status to Paid" is idempotent, "add 10 to the balance" is not.

| Mid | Senior |
|---|---|
| "Check xem đã có giao dịch chưa rồi insert" | **INSERT key + UNIQUE trong cùng transaction** |
| Trùng → trả lỗi 400 | Trùng → **trả lại response cũ**; đang chạy → 409; payload khác → 422 |
| Server tự sinh key | Client sinh 1 key cho 1 ý định, dùng lại khi retry |
| Quên hệ thống bên ngoài | Pending → gọi provider với key → completed + job đối soát |

---

### S6. "Crash scenarios: the database crashes before commit, during commit, after commit; the worker crashes after the commit."

**Bản chất — Write-Ahead Log (WAL).** Mọi DB quan hệ (PostgreSQL: WAL; SQL Server: transaction log) ghi **log thay đổi xuống đĩa trước** khi ghi trang dữ liệu. `COMMIT` chỉ trả "OK" sau khi bản ghi commit trong log đã được **fsync** xuống đĩa. Khi khởi động lại sau crash, DB **đọc log**: transaction đã commit thì làm lại (redo) cho đủ; transaction chưa commit thì coi như **chưa từng xảy ra**. → Durability nghĩa là: **đã nhận "OK" thì không mất**; **chưa nhận "OK" thì không chắc**.

Timeline một request ghi tiền + gửi message:
```
t0  BEGIN
t1  UPDATE balance ...           (ghi vào log + buffer, chưa bền)
t2  INSERT payment ...
t3  COMMIT gửi đi
t4  log commit record fsync xuống đĩa  ← điểm "đã commit"
t5  DB trả "OK" cho app
t6  app publish message "PaymentCompleted"
t7  worker nhận message, gửi email / gọi dịch vụ khác
t8  worker ack (complete) message
```

**Trả lời mẫu (đi theo timeline):**
> I'd walk through the timeline, because the answer depends on exactly where it crashes.
>
> **Database crashes before COMMIT (t1–t3).** Nothing is lost that was promised. The transaction never committed, so on restart the database recovers from its write-ahead log and the changes are discarded — PostgreSQL simply never marks the transaction as committed, so its row versions are invisible; SQL Server runs an undo phase from the transaction log. The app sees a connection error, and it's safe to retry the whole transaction.
>
> **Crash during COMMIT — the ambiguous case (t3–t5).** The app sent COMMIT and the connection died. Maybe the commit record reached disk at t4, maybe not. The app can't know. That's why the retry must be idempotent: retry with the same idempotency key, and the unique constraint tells us if the first attempt actually committed. Or reconnect and look the operation up by its key before retrying.
>
> **Database crashes after COMMIT returned (after t5).** The data is safe: the commit record was flushed to the log before we got "OK", and recovery replays it. Two caveats a senior should mention: if durability was relaxed — `synchronous_commit = off` in PostgreSQL or delayed durability in SQL Server — the last few milliseconds of commits can be lost; and with asynchronous replication, if the primary dies and we fail over, the replica may not have the last commits. That's the RPO of our setup, and for money I'd want synchronous replication or a synchronous commit to a standby.
>
> **App crashes after commit but before publishing the message (t5–t6).** The payment is saved but nobody is told — no email, no downstream update. This is the dual-write problem. The fix is the **transactional outbox**: write the message into an `Outbox` table in the same transaction as the payment; a separate publisher reads the outbox and sends to the queue, marking rows as sent. If it crashes after sending but before marking, it sends again — so delivery is at-least-once, and consumers must be idempotent.
>
> **Worker crashes after receiving the message but before finishing (t7).** If we only ack after the work is done — peek-lock in Service Bus, or manual ack — the lock expires and the message is redelivered to another worker. Nothing is lost. After a number of failures it goes to the dead-letter queue, which we alert on.
>
> **Worker finishes the work, crashes before ack (t7–t8).** The message is redelivered and the work runs twice. So the side effect must be idempotent: record the message ID in the same transaction as the work, or pass an idempotency key to the external call — the email provider, the payment provider.
>
> **Worker acks first, then crashes before doing the work.** The message is lost. That's why we never ack before the work is durable — "ack after commit" is the rule.
>
> So the overall design is: database transaction plus outbox on the producer side, at-least-once delivery, and idempotent consumers. Exactly-once delivery doesn't exist; exactly-once *effect* is what we build.

**Chuỗi follow-up:**

**F1. "Why not just publish the message first, then commit?"**
> Then a crash between them sends a "PaymentCompleted" event for a payment that rolled back — worse than losing an event. Either order of two separate writes is wrong; the outbox makes it one write.

**F2. "Why not a distributed transaction (2PC) between the database and the queue?"**
> Two-phase commit couples the availability of both systems — if the coordinator dies between phases, participants hold locks waiting — and many cloud services, like Azure Service Bus with an external database, don't support it. The outbox gives the same practical guarantee with just a local transaction.

**F3. "How does the outbox publisher not send the same row twice when you run two publisher instances?"**
> Claim rows with `UPDLOCK, READPAST` or `FOR UPDATE SKIP LOCKED`, so each instance takes different rows. Even so, a crash between send and mark can resend, so consumers stay idempotent — the outbox row ID becomes the message ID, which consumers use to deduplicate.

**F4. "The message order matters — 'PaymentRefunded' processed before 'PaymentCompleted'."**
> Two tools: partition by key so messages of one aggregate go in order to one consumer — Service Bus sessions with the payment ID as session ID, or a Kafka/Event Hub partition key — and make consumers check a version or sequence number, ignoring or parking an event older than the state they already have.

**F5. "A long transaction is running and PostgreSQL restarts. How long is recovery?"**
> Recovery replays the WAL from the last checkpoint, so recovery time depends on how much WAL was written since then — checkpoint frequency is the trade-off between write overhead and recovery time. A long uncommitted transaction doesn't need to be undone in PostgreSQL thanks to MVCC — its rows are just invisible — whereas SQL Server must roll it back in the undo phase, which can take as long as the transaction ran; Accelerated Database Recovery in newer versions fixes that. [Phần này là kiến thức tài liệu, không phải kinh nghiệm vận hành Postgres của Hiệp — nói "as far as I know from the documentation"]

**F6. "How do you detect that something got stuck in the middle?"**
> Business-level monitoring: outbox rows older than a minute, dead-letter queue count above zero, payments in "pending" older than five minutes, and a daily reconciliation comparing our records with the provider's report. Exceptions alone won't show a message that was silently never sent.

**Liên hệ thật:** Hiệp **đã nhầm Outbox với Mediator** và từng **chấp nhận mất message** cho luồng tiền (progress.md). Câu sửa sai nên thuộc: *"For anything involving money, losing a message isn't acceptable; I'd use an outbox in the same transaction and idempotent consumers."* Joblogic: BO notification idempotent theo `EventIdempotentId` → ví dụ thật cho consumer idempotent.

| Mid | Senior |
|---|---|
| "DB có ACID nên an toàn" | Đi theo timeline, chỉ ra **vùng mơ hồ khi COMMIT** |
| Không biết WAL | WAL/transaction log, fsync trước khi trả OK, redo/undo, `synchronous_commit` |
| Commit rồi publish | **Outbox** cùng transaction + publisher + consumer idempotent |
| Ack trước rồi xử lý | Ack sau khi commit, retry → DLQ + alert |
| Quên replica | Async replication → failover mất commit cuối (RPO) |

---

### S7. Ngân hàng tình huống thêm (trả lời nhanh 4–5 câu, theo khung 7 bước)

| Tình huống | Gọi tên | Xác nhận bằng | Xử lý tạm → gốc |
|---|---|---|---|
| Memory của API tăng dần rồi pod bị restart | Memory leak (static collection, event handler không gỡ, cache không giới hạn) | GC counters, `dotnet-gcdump`/`dotnet-dump`, so sánh 2 dump | Restart/scale → sửa chỗ giữ reference, cache có size limit |
| "Timeout expired… max pool size was reached" | Connection pool exhaustion | `dotnet-counters` (Microsoft.Data.SqlClient), query chậm hoặc connection không dispose | Kill query chậm → `using`/`await using`, transaction ngắn, Little's Law: pods × pool < max connections DB |
| Bên thứ ba (payment, SMS) chậm 30 s làm sập cả API | Cascading failure, thiếu timeout/bulkhead | Trace: span HTTP ngoài chiếm hết thời gian | Timeout ngắn + circuit breaker (Polly) → chuyển sang background job + retry có backoff |
| Một khách (tenant lớn) làm chậm mọi khách khác | Noisy neighbour | Lọc metric theo tenant | Rate limit theo tenant → index/phân trang, tách job nặng |
| Webhook từ provider bị gửi 3 lần, xử lý 3 lần | Thiếu idempotent consumer | Log theo event ID | Bảng processed events UNIQUE → trả 200 cho bản trùng |
| Hai admin sửa cùng một quote, người sau ghi đè người trước | Lost update | Audit log | rowversion / ETag → 409 "someone else changed this" |
| Job hằng đêm chạy 2 lần khi scale lên 3 instance | Thiếu leader/lock cho scheduled job | Log có 3 dòng start | Lock DB/Redis cho job hoặc dùng scheduler riêng; job idempotent |
| Deploy xong lỗi 500 ở 5% request | Release lỗi một phần (1 pod cấu hình sai / migration chưa chạy) | Lọc lỗi theo instance/version | Rollback → readiness check, canary, migration tương thích ngược |
| Báo cáo cuối tháng cộng tiền lệch vài cent | `double` thay vì `decimal`, làm tròn từng dòng vs tổng | So sánh từng dòng | `decimal`, quy tắc làm tròn thống nhất (banker's vs away-from-zero), test |
| Lịch giao hàng lệch 1 giờ sau ngày đổi giờ | DST, lưu giờ local | Dữ liệu quanh ngày DST | Lưu UTC + timezone ID, chuyển khi hiển thị |

---

## PHẦN 3 — Cách luyện với file này

1. **Mỗi ngày 2 tình huống**, nói to bằng tiếng Anh, bấm giờ: câu trả lời đầu ≤ 2 phút, mỗi follow-up ≤ 45 giây.
2. Tự chấm bằng bảng Mid/Senior cuối mỗi tình huống. Thiếu bước nào ghi lại ở `progress.md`.
3. Nhờ Claude (hoặc prompt ChatGPT trong `S-seadev-chatgpt-mock-prompt.md`) đóng vai interviewer, **chỉ hỏi follow-up "what if…"**, không cho xem đáp án trước.
4. **Điền hết [Hiệp điền] / [Hiệp xác nhận]** trước buổi phỏng vấn, ưu tiên: kết quả Quest Engine (1.1), ETag/If-Match (F4), cách trả thưởng (F6), bug thật (F9), câu chuyện tối ưu AVA (S1, S3), key thật của Pragmatic (1.4).
5. Câu thần chú trước khi vào phòng:
   - *"Let me first clarify and measure."*
   - *"The lock is an optimisation; the database constraint is the guarantee."*
   - *"INSERT with a UNIQUE constraint in the same transaction."*
   - *"On a duplicate, return the original response."*
   - *"Outbox in the same transaction, at-least-once delivery, idempotent consumers."*
