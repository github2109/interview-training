# Lộ trình ôn Senior .NET Backend

Nguồn: bộ 150 câu hỏi .NET Backend (Junior → Senior).
Đánh dấu `[x]` khi đã ôn xong và trả lời được trong khoảng 2 phút.

## Cách phân loại
- **Ưu tiên 1 — quyết định level Senior:** học kỹ, phải trả lời có ví dụ thực tế.
- **Ưu tiên 2 — nền tảng Mid:** chắc chắn sẽ bị hỏi, phải trả lời trôi chảy.
- **Ưu tiên 3 — Junior:** chỉ tự kiểm tra nhanh, không học sâu (trừ các câu được đánh dấu ⚠️ vì hay bị hỏi xoáy).

---

## Buổi 1 — Async, concurrency, DI (Ưu tiên 1)
- [ ] 23–26, 52–57 Async/await, SynchronizationContext, blocking, race condition, CancellationToken, WhenAll
- [ ] 108 Thread-pool starvation
- [ ] 32–33, 66–68 DI lifetimes, captive dependency, service locator vs constructor injection
- [ ] 134 Code review: `ProcessAsync` dùng `.Result`

## Buổi 2 — ASP.NET Core và kiến trúc API
- [ ] 31, 61–65 Request pipeline, middleware vs filter, cấu trúc Web API, DTO/domain/persistence, dependency inversion
- [ ] 22 Xử lý exception trong Web API (ProblemDetails, global handler)
- [ ] 78–81 Thiết kế REST, idempotency, versioning, pagination

## Buổi 3 — Data: EF Core, SQL, transaction
- [ ] 18–19 ⚠️, 58–60 Deferred execution, IEnumerable vs IQueryable, tối ưu LINQ
- [ ] 69–73 DbContext, tracking, N+1, optimistic concurrency, transaction
- [ ] 74–77 Normalization, isolation levels, điều tra query chậm, connection pooling
- [ ] 109–112, 127 DB cho hệ thống giao dịch lớn, denormalize, partitioning, migration an toàn, query chậm 20×

## Buổi 4 — Caching, messaging, độ tin cậy (gắn trực tiếp với kinh nghiệm PlaySweeps)
- [ ] 82–84 Cache đa instance, cache stampede
- [ ] 85–88, 102–104 Queue, at-least-once, DLQ, background worker, consumer tin cậy, pub/sub
- [ ] 143 Outbox pattern · 144 Saga · 101 Distributed transaction
- [ ] 100, 129, 131, 132 Idempotency, xử lý trùng, chạy 1 instance thì đúng nhưng 5 instance thì lỗi

## Buổi 5 — Distributed systems và resilience
- [ ] 97–99, 130, 146 Timeout, retry, circuit breaker, bulkhead (Polly), external API chậm
- [ ] 96, 145, 149 Eventual consistency, CAP, scalability/performance/availability/reliability
- [ ] 117–120 Graceful degradation, health check, graceful shutdown, zero-downtime deploy

## Buổi 6 — Performance và observability
- [ ] 89–91, 147 Logs/metrics/traces, API đột nhiên chậm
- [ ] 105–107 Prod chậm hơn local, CPU cao, memory leak (dotnet-counters, dotnet-dump)
- [ ] 28–29 ⚠️ GC, IDisposable

## Buổi 7 — Security
- [ ] 113–116 OWASP API, authN vs authZ, lưu password, chống lạm dụng API (rate limit, đúng kinh nghiệm của bạn)

## Buổi 8–10 — System design (phỏng vấn thử 45 phút)
- [ ] 121 Payment API ← đề mạnh nhất của bạn
- [ ] 124 Rate limiter đa instance ← bạn đã làm exponential rate limit
- [ ] 123 Notification system
- [ ] 122 Order processing
- [ ] 92–95 High traffic, monolith vs microservices, scaling, HA
- [ ] 148, 150 Đưa thay đổi kiến trúc lớn lên production, kiến trúc bạn tự tin vận hành

## Buổi 11 — Code review
- [ ] 133–136

## Buổi 12 — Behavioral (STAR, bằng tiếng Anh)
- [ ] 137 Bug production khó nhất
- [ ] 138 Vấn đề performance đã giải quyết
- [ ] 139 Sự cố do quyết định thiết kế
- [ ] 140 Bất đồng với quyết định kỹ thuật
- [ ] 141 Hệ thống tiếp quản khó bảo trì (Socure)
- [ ] 142 Bug không tái hiện được ở local

## Ưu tiên 2–3: tự kiểm tra nhanh
- C# nâng cao: 46–51 (ref/in/out, delegate/event, record, primary constructor, pattern matching)
- Junior: 1–17, 20–21, 27, 30, 34–45 (chỉ cần trả lời được trong 30 giây)
