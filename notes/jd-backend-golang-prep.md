# Ôn nhanh JD Backend Developer (Go/Java/Node/PHP · MySQL · ClickHouse · Redis · ES · Kafka/RabbitMQ)

## 0. Pitch 60 giây (EN)
"I'm a backend-focused full-stack engineer with 4 years of experience. For the last two years I worked on PlaySweeps, a US sweepstakes gaming platform with over 2 million registered players, built on .NET 8, Redis, Cosmos DB and Azure messaging. I was a feature lead: I wrote technical designs, implemented and released features like the Quest Engine V2 and the Pragmatic Play seamless wallet, reviewed PRs and did on-call. I've also built services in NestJS/Node and Go. What I care about most is correctness under concurrency — idempotency, locking, retries — and observability in production."

## 1. Map JD ↔ kinh nghiệm (nói thật, bắc cầu)
| JD | Đã làm | Cách nói |
|---|---|---|
| Go/Node | NestJS (EIM), Node, Go | Ngôn ngữ là công cụ; nguyên lý concurrency/IO giống nhau |
| MySQL | SQL Server qua Dapper + stored procedure | Index, transaction, isolation, EXPLAIN dùng chung tư duy |
| Redis | Cache, RedLock (Quest Engine), rate limit | Có ví dụ thật |
| Kafka / RabbitMQ | Azure Event Hub (≈ Kafka: partition, consumer group, offset) / Service Bus (≈ RabbitMQ: queue, topic, DLQ) | Nói rõ đã vận hành bản Azure, hiểu mô hình |
| ClickHouse / ES | Chưa dùng production | Nói đúng bản chất + khi nào dùng, không bịa |
| Prometheus/Grafana | Grafana Loki, App Insights, Splunk | Metrics vs logs vs traces |

## 2. Kiến thức cốt lõi

**System design — khung trả lời:** requirements (functional + non-functional: QPS, latency, consistency) → ước lượng con số → API → data model → kiến trúc → điểm nghẽn & scale → failure modes → observability.

**MySQL (InnoDB)**
- Clustered index theo PK (B+tree); secondary index lưu PK → lookup 2 lần. Covering index tránh lookup.
- Composite index: leftmost prefix; cột equality trước, range sau.
- `EXPLAIN`: xem `type` (ALL = full scan), `key`, `rows`, `Extra: Using filesort/temporary`.
- Default isolation **REPEATABLE READ**, MVCC; gap/next-key lock chống phantom → dễ deadlock khi insert theo range.
- Scale: read replica (lưu ý replication lag), partitioning, sharding theo key; connection pool.
- Pagination: keyset (`WHERE id > ? LIMIT n`) thay `OFFSET` lớn.

**Redis**
- Kiểu: string, hash, list, set, sorted set (leaderboard), stream.
- Cache-aside + TTL; chống stampede: lock/single-flight, TTL jitter; invalidate khi ghi.
- Distributed lock: `SET key val NX PX ttl`, release bằng Lua so khớp value; RedLock cho nhiều node. Lock không thay idempotency (ví dụ Quest Engine: RedLock + idempotency key cho claim).
- Rate limit: fixed window `INCR+EXPIRE`, sliding window bằng sorted set, token bucket.

**ClickHouse** — OLAP, lưu theo cột, nén tốt, quét/aggregate cực nhanh. `MergeTree`, `ORDER BY` là sparse primary index. Insert theo batch lớn, không hợp update/delete từng dòng hay OLTP. Dùng cho analytics/event log; nạp từ Kafka.

**Elasticsearch** — inverted index cho full-text; shard (scale) + replica (HA); near-real-time (refresh ~1s). Không làm source of truth; đồng bộ từ DB qua CDC/outbox → Kafka → indexer.

**Kafka vs RabbitMQ**
- Kafka: distributed log, partition giữ thứ tự trong partition, consumer group, giữ message theo retention, replay được, throughput cao.
- RabbitMQ: broker đẩy message, exchange/routing linh hoạt, ack xong là xoá, hợp task queue.
- Delivery thực tế: at-least-once → **consumer phải idempotent** (dedupe theo message id). Retry + DLQ. Ghi DB và publish nhất quán → **transactional outbox**.
- Thứ tự theo entity: partition key = userId.

**gRPC** — HTTP/2 + Protobuf, nhị phân, có streaming, code-gen hợp đồng; luôn đặt **deadline**. Dùng service-to-service nội bộ; REST cho public/browser.

**Go cơ bản** — goroutine (nhẹ, scheduler M:N), channel, `select`, `context` (cancel/timeout lan truyền), `sync.WaitGroup`/`errgroup`, `sync.Mutex`; `go test -race`; tránh goroutine leak (luôn có đường thoát qua ctx).

**Distributed system**
- CAP/PACELC; strong vs eventual consistency.
- Idempotency key, retry với exponential backoff + jitter, timeout, circuit breaker.
- Saga (orchestration/choreography) thay distributed transaction.
- Ví dụ thật: Pragmatic wallet — callback bet/result/refund có thể gửi lại → kiểm tra theo transaction/round id, trả lại kết quả cũ, khoá pending wager.

**Observability** — Prometheus pull/scrape `/metrics`; loại metric: counter, gauge, histogram (tính p95/p99), summary. RED (Rate, Errors, Duration) cho service, USE cho tài nguyên. Alert theo SLO, không theo CPU đơn thuần.

**CI/CD & Docker** — multi-stage build (image Go nhỏ, distroless), pipeline: lint → test → build image → push registry → deploy; rolling/blue-green/canary; health check readiness/liveness; secrets không nằm trong image.

**Testing & review** — unit (mock dependency, table-driven trong Go), integration với DB thật (Testcontainers), test case cho concurrency/idempotency. Review: correctness, edge case, transaction/lock, log/metric, backward compatibility.

## 3. Câu chuyện "scaling/optimizing" (STAR, EN)
"On PlaySweeps, sensitive APIs like login, OTP and redemption were targets for abuse. I implemented exponential rate limiting backed by Redis: each failed attempt increases the lockout window, keyed by user and device. The result was fewer abusive requests reaching the database and third-party providers, without hurting normal users. I monitored it through Application Insights and Grafana to tune the thresholds."

## 4. Câu hỏi nên hỏi lại
- Hệ thống hiện tại: monolith hay microservices, traffic cỡ nào?
- Kafka/ClickHouse dùng cho bài toán gì?
- Quy trình on-call, code review, release?
- Kỳ vọng với Senior trong 6 tháng đầu?
