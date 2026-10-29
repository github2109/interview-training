# Funfinity — ôn phỏng vấn Backend / Game Server (Java/C++)

## 0. Nói thật về khoảng trống
- JD đòi **3 năm Java**. Java **chưa có bằng chứng** trong career-facts → không nhận là đã làm Java production.
- Bắc cầu: C#/.NET 8 gần như song sinh với Java (JVM ≈ CLR, GC thế hệ, generics, thread pool, async). Go (Altar of Sacrifice) cho tư duy goroutine/concurrency.
- Câu nói: "My production languages are C#/.NET, Go and Node. Java is very close to C# — same managed runtime model, GC, threading primitives — and I've been studying Java concurrency specifically: `java.util.concurrent`, the Java Memory Model, virtual threads. I'm confident I can be productive quickly."

## 1. Pitch 60 giây (EN)
"I've spent four years at Geargames, a game company, building backend systems for games. Most recently I worked on PlaySweeps, a US sweepstakes gaming platform with over 2 million registered players, on .NET 8, Redis and Azure. I was feature lead for the Quest Engine V2 — a personalized mission system with Redis distributed locks and idempotent reward claims — and the Pragmatic Play seamless wallet, where bet, result and refund callbacks must be idempotent and consistent under retries. Before that I built a Go backend for Altar of Sacrifice, a sacrifice/crafting system with drop rates, mint caps and a pity mechanic for Guild of Guardians, and game configuration tools with versioned Protobuf. I like game backends because correctness under concurrency directly affects players and money."

## 2. Ví dụ thật map vào JD
| JD | Ví dụ |
|---|---|
| Event, vận hành game | Quest Engine V2, Live Ops (AVA remote config/A-B, Kinoa), Banner System |
| Payment | Pragmatic seamless wallet (idempotency, hash, khoá pending wager), redemption, Apple Pay |
| Gameplay logic server | Altar of Sacrifice: recipe/sacrifice engine, mint cap, streak breaker (pity) |
| Redis/Cache | RedLock, rate limiting, cache config |
| Protobuf | Game config tool: Protobuf có version |
| Multiplayer real-time, TCP/UDP, matchmaking | **Chưa làm production** → trình bày thiết kế |

## 3. Java core cần nắm (C# → Java)
- `synchronized`/`ReentrantLock` ≈ `lock`/`Monitor`; `volatile` (visibility + ordering, không atomic cho `i++`).
- **Java Memory Model / happens-before**: unlock → lock, volatile write → read, `Thread.start`, `join`.
- `AtomicLong`, `LongAdder` (đếm nhiều thread tranh chấp), CAS.
- `ConcurrentHashMap` (`compute`, `merge` atomic theo key), `CopyOnWriteArrayList`, `BlockingQueue`.
- `ExecutorService`, `CompletableFuture` ≈ `Task`; **virtual threads (Java 21)** ≈ goroutine nhẹ cho IO.
- GC: heap thế hệ, **G1** mặc định, **ZGC** pause < 1ms → hợp game server; tránh tạo rác trong tick loop (object pool).
- Deadlock: khoá theo thứ tự cố định; `jstack` xem thread dump; profiler: JFR, async-profiler.

## 4. C++ tối thiểu (nếu bị hỏi)
- **RAII**: tài nguyên gắn với vòng đời object, destructor tự giải phóng (≈ `using`/try-with-resources nhưng tất định).
- `unique_ptr` (sở hữu duy nhất, move), `shared_ptr` (đếm tham chiếu, atomic → có chi phí), `weak_ptr` (phá vòng tham chiếu).
- Move semantics tránh copy. `std::atomic`, `std::mutex` + `lock_guard`.
- Nói thật: chưa làm C++ production.

## 5. Kiến trúc game server
- **Stateless API** (login, shop, guild, ranking) vs **stateful game server** (phòng/trận giữ state trong RAM).
- **Game loop theo tick**: ví dụ 20 tick/giây = 50ms/tick: nhận input → cập nhật state → gửi snapshot/delta.
- **Một room = một thread/actor**: mọi thao tác trên room chạy tuần tự trên một luồng → không cần lock state room; nhiều room chạy song song trên thread pool. (Mô hình actor, Akka/Orleans.)
- **Server-authoritative**: client chỉ gửi input, server tính kết quả → chống cheat.
- Routing: gateway giữ kết nối, route theo roomId tới đúng node (sticky); state trận kết thúc mới ghi DB.
- Scale: chia theo room/shard; gateway scale ngang; Redis pub/sub hoặc message bus giữa node.

## 6. Network
| | TCP | UDP | WebSocket |
|---|---|---|---|
| Đặc điểm | Tin cậy, có thứ tự, có head-of-line blocking | Không đảm bảo, nhanh | Chạy trên TCP, full-duplex, qua được proxy/browser |
| Game hợp | Turn-based, card, idle, chat | FPS, action real-time | Casual, web/mobile game |
- TCP là **stream**, không phải message → cần **framing**: `[length 4 byte][payload]`.
- Payload nhị phân: **Protobuf** (nhỏ, có schema, versioning).
- Java: **Netty** (event loop non-blocking, NIO, epoll). C++: Boost.Asio.
- Heartbeat/ping để phát hiện mất kết nối; reconnect + resync state.
- Nagle → `TCP_NODELAY` cho game cần độ trễ thấp.

## 7. Các hệ thống trong JD
- **Ranking**: Redis Sorted Set: `ZINCRBY lb:season1 50 user42`, `ZREVRANGE 0 99`, `ZREVRANK`. Hàng triệu user vẫn O(log N). Hoà điểm: score = điểm × 1e10 + (MAX_TS − ts) để ai đạt trước xếp trên. Leaderboard theo mùa: key theo season, snapshot cuối mùa để trao thưởng.
- **Matchmaking**: hàng đợi theo vùng/mode; ghép theo MMR (Elo/Glicko) với **khoảng chấp nhận nới dần theo thời gian chờ** (0–10s ±50, sau 30s ±200). Worker chạy định kỳ, ghép nhóm, cấp phát room, gửi thông tin kết nối.
- **Guild**: quan hệ guild–member trong DB; giới hạn số thành viên → chống race bằng `UPDATE guild SET count=count+1 WHERE id=? AND count<max` (atomic) hoặc lock theo guildId; chat guild qua pub/sub.
- **Event/Live Ops**: config theo thời gian từ server (remote config), không cần ra bản client; tiến độ nhiệm vụ cập nhật từ event; nhận thưởng phải idempotent (Quest Engine).
- **Payment**: verify receipt với Apple/Google **ở server**; idempotency theo transactionId; cộng vật phẩm + ghi ledger trong một transaction; xử lý refund/chargeback qua webhook.

## 8. Concurrency trong game — câu hỏi kinh điển
"Hai request nhận cùng một phần thưởng / mua cùng item cuối cùng":
1. DB: `UPDATE ... WHERE stock > 0` (conditional atomic update) hoặc optimistic version.
2. Unique constraint trên (userId, rewardId) → idempotent.
3. Distributed lock (Redis) theo userId khi logic phức tạp — nhưng lock có TTL, không thay được idempotency.
4. Trong một process: single-thread per player/room hoặc `ConcurrentHashMap.compute`.

## 9. Tối ưu hiệu năng — cách trả lời
Đo trước (metrics p99, profiler/flame graph, GC log) → tìm điểm nghẽn (CPU, GC pause, lock contention, IO, N+1 query) → sửa (batch, cache, giảm allocation/object pool, chia lock nhỏ, async IO) → đo lại.

## 10. Câu hỏi nên hỏi lại
- Game thể loại gì, real-time hay turn-based? Giao thức TCP/WebSocket/UDP?
- Stack server hiện tại Java (Netty/Spring?) hay C++? Có dùng framework actor không?
- CCU cao nhất? Mô hình triển khai (VM, K8s)?
- Đối tác quốc tế: quy trình làm việc, timezone?

## Tiến độ học (dạy lại từ nền, 2026-10-30)
Đã xong: B1 race condition trong RAM (Atomic vs synchronized, 2 lần Atomic ≠ atomic; synchronized ≠ RedLock) · room nằm trên một instance (allocator + SET NX + kết nối thẳng) · B2 TCP/UDP/socket/HTTP/WebSocket · B3 event loop (epoll, không chặn loop) · B4 state trong RAM · B5 tick và room · B6 ranking (đang ở câu tự kiểm tra).
Còn lại: matchmaking · guild · event/live ops · payment IAP · deadlock + thứ tự khoá · Java core (collections, ExecutorService, CompletableFuture, GC) · C++ tối thiểu · tối ưu hiệu năng · luyện pitch + câu trả lời về khoảng trống Java · mock.
User hay bỏ qua câu tự kiểm tra → nhắc trả lời bằng miệng.
