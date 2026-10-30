# SEADEV — C# Developer (ShedPro Ops Hub): FILE HỌC TỔNG HỢP (bản sâu)

Cập nhật: 2026-10-30. **Viết lại theo độ sâu của buổi phỏng vấn Agapi**: mỗi section đi từ bản chất (OS, runtime, database) → ví dụ đời thường, code, con số → câu hỏi phỏng vấn kèm câu đào sâu → câu trả lời mẫu mức Senior → bẫy hay sai → tự kiểm tra.
Ngôn ngữ: **giải thích tiếng Việt, thuật ngữ trong ngoặc (English term)**, **câu trả lời mẫu tiếng Anh**. Câu mẫu về dự án chỉ dùng sự thật đã kiểm chứng (`context/career-facts.md`); chỗ cần Hiệp tự điền ghi **[Hiệp điền]**.

---

## 0. Cách dùng file này

### 0.1 Quy trình học (Hiệp chốt 2026-10-30)
1. Học **lần lượt từng section** theo bảng 0.2 (đi từ nền tảng lên nâng cao).
2. Đọc xong một section → nhắn "**xong A1**" (hoặc tên section). Claude đánh dấu ✅ trong bảng, rồi **hỏi kiểm tra** bằng các câu ở mục "Tự kiểm tra" và câu phỏng vấn của section đó; Hiệp trả lời, Claude chấm **Mid / Senior** và chỉ ra chỗ thiếu.
3. Muốn bỏ qua phần hỏi → nhắn "**skip**": đánh dấu ✅ (không kiểm tra) và đi tiếp section sau.
4. Nếu sắp tới ngày phỏng vấn mà chưa học hết: đọc **D1, D2** (pitch, kể dự án) trước, rồi phần "Câu hỏi phỏng vấn" của các section còn lại.

Ký hiệu trạng thái: ⬜ chưa học · 📖 đang học · ✅ xong (đã kiểm tra) · ⏭ xong (skip kiểm tra) · ⏳ section chưa được viết lại sâu (đang là nội dung cũ, Claude sẽ viết lại trước khi Hiệp học tới).

### 0.2 Bảng tiến độ
| # | Section | Ai hay hỏi | Khả năng bị hỏi | Trạng thái |
|---|---|---|---|---|
| **A** | **NỀN TẢNG** | | | |
| A1 | Process, thread, bộ nhớ, I/O | SA | Trung bình (gián tiếp qua câu "vì sao chậm") | ⬜ |
| A2 | Mạng và HTTP: TCP/TLS, cookie, stateless, CORS, L4/L7 | SA | Cao (nền của auth, LB) | ⬜ |
| A3 | C# và .NET runtime: CLR/JIT, value/reference, GC, IDisposable, LINQ, decimal | SA | Cao 65% | ⬜ |
| A4 | Async/await, thread pool starvation, đồng bộ trong process | SA | Cao 60% | ⬜ |
| A5 | SQL Server bên trong: page, B-tree, index, execution plan, JOIN, statistics | SA | Cao 70% | ⬜ |
| A6 | Transaction, isolation, lock, deadlock, XACT_ABORT, update balance | SA | Cao 70% | ⬜ |
| **B** | **XÂY ỨNG DỤNG .NET** | | | |
| B1 | ASP.NET Core: pipeline, DI, middleware, filter, cấu hình | SA | Cao 65% | ⬜ |
| B2 | ASP.NET MVC: model binding, validation, CSRF, over-posting, PRG | SA | Cao 60% | ⬜ |
| B3 | EF Core và Dapper: tracking, N+1, split query, concurrency, migration | SA | Cao 70% | ⬜ |
| B4 | REST API design | SA | Rất cao 85% | ⬜ |
| B5 | OOP, SOLID, layering, kiến trúc tổng thể | SA | Rất cao 90% | ⏳ |
| B6 | Design patterns | SA | Cao 80% | ⏳ |
| B7 | Clean code và code review | SA | Rất cao 80% | ⏳ |
| B8 | Unit test, integration test | SA | Cao 65% | ⏳ |
| B9 | Frontend (React/TS) và hợp đồng FE–BE | SA | Trung bình–Cao 60% | ⏳ |
| **C** | **HỆ THỐNG VÀ VẬN HÀNH (NÂNG CAO)** | | | |
| C1 | Authentication: stateful vs stateless, session cookie vs JWT, refresh, revoke | SA | Cao (Agapi đã hỏi) | ⏳ |
| C2 | Security: OWASP, secret, bảo vệ tiền trước người nội bộ | SA | Trung bình–Cao | ⏳ |
| C3 | Concurrency dữ liệu và idempotency xuyên hệ thống | SA | Cao 60% | ⏳ |
| C4 | Redis: bản chất, persistence RDB/AOF, khi Redis chết, distributed lock, cache | SA | Trung bình–Cao (Agapi đã hỏi) | ⏳ |
| C5 | Messaging, background job, outbox, saga | SA | Trung bình 50% | ⏳ |
| C6 | Scale và load balancer: thuật toán, sticky session, health check, CAP | SA | Trung bình–Cao (Agapi đã hỏi) | ⏳ |
| C7 | SQL vs NoSQL (MongoDB, Cosmos DB) | SA | Trung bình (Agapi đã hỏi) | ⏳ |
| C8 | Tích hợp bên thứ ba và resilience | SA | Trung bình 55% | ⏳ |
| C9 | Observability và chẩn đoán "request mất 8 giây" | SA | Cao (Agapi đã hỏi) | ⏳ |
| C10 | CI/CD, deploy an toàn, build .NET nhanh hơn | SA | Trung bình–Cao 60% | ⏳ |
| C11 | AWS (map từ Azure) | SA | Trung bình–Cao 60% | ⏳ |
| C12 | Multi-tenant SaaS | SA | Trung bình–Cao 60% | ⏳ |
| C13 | System design nhỏ | SA | Trung bình 40% | ⏳ |
| **D** | **NGHIỆP VỤ, DỰ ÁN, CON NGƯỜI** | | | |
| D1 | Giới thiệu bản thân, câu hỏi cá nhân | SA + PO | Rất cao 95% | ⏳ |
| D2 | Kể dự án trong CV + bị đào sâu | SA + PO | Rất cao 95% | ⏳ |
| D3 | Nghiệp vụ Ops Hub (quote → order → RTO → production → delivery) | PO (+SA) | Rất cao 85% | ⏳ |
| D4 | Câu hỏi PO: làm rõ yêu cầu, edge case, ưu tiên | PO | Rất cao 85% | ⏳ |
| D5 | Refactoring và tiếp quản code từ đối tác Mỹ | SA + PO | Cao 80% | ⏳ |
| D6 | Behavioral STAR (tiếng Anh) | SA + PO | Cao 75% | ⏳ |
| D7 | Git, Agile/Scrum, làm việc remote với Mỹ | SA + PO | Trung bình 50% | ⏳ |
| D8 | Câu hỏi ngược cho interviewer | SA + PO | Rất cao 95% | ⏳ |
| D9 | Checklist trước giờ phỏng vấn, phụ lục | — | — | ⏳ |

Đối chiếu bản cũ (2026-10-23) → bản mới: 11→A3, 12→A4, 15→A5/A6/B3, 13→B1, 14→B2, 4→B4, 3→B5/C6, 6→B6, 5→B7, 18→B8, 19→B9, 24→C1/C2, 16→C3, 23→C4/C5, 22→C8, 25→C9, 20→C10, 21→C11, 17→C12, 26→C13, 1→D1, 2→D2, 8→D3, 9→D4, 7→D5, 10→D6, 27/28→D7, 29→D8, 30/31→D9.

### 0.3 Ai phỏng vấn, họ quan tâm gì
- **Vòng 1 = culture & core values** → file riêng `notes/S-seadev-culture.md`. File này dành cho **vòng tech** (SA + PO). Interviewer tech vẫn nghe xem bạn có sống theo 5 value không: **1% Improvement, Driven by Customer Success, Enjoy Problem Solving, Be Accountable, Love our People & Communities**.
- **Solution Architect (có thể là Khiet Vo)**: gốc frontend / full stack JS–TS (React, TypeScript, UX/UI, Node), skill ở vai trò SA: **Software Architecture, CI/CD**; trước đó **AWS**, **REST, Clean Coding** (Urbanise: SaaS quản lý chung cư/facilities). Không khai C#/.NET → ít soi nội tại CLR, soi **thiết kế, API, chất lượng code, pipeline, cloud**; nhưng nếu SA mang câu hỏi kiểu Agapi (chẩn đoán, lock, auth, Redis, LB) thì Phần A và C là lá chắn.
- **Product Owner / PM**: nghiệp vụ, làm rõ yêu cầu, edge case, ưu tiên, giao tiếp, accountable.
- Bối cảnh JD: tiếp quản code từ **đối tác Mỹ**, **dẫn dắt** tính năng mới, giữ hiệu năng, chất lượng, bảo trì lâu dài. Yêu cầu: **≥ 4 năm** C#/.NET, ASP.NET MVC và/hoặc Web API, AWS/cloud, design pattern + refactoring, clean code, Git, Agile, REST; cộng điểm: React/Angular/Vue, unit test, tiếng Anh.

### 0.4 Khung trả lời chung
1. **Câu ngắn trước** (1–2 câu trả lời thẳng), rồi "Would you like me to go deeper into X?".
2. **Cơ chế** (vì sao nó như vậy, ở tầng nào).
3. **Ví dụ thật** của Hiệp (PlaySweeps, Joblogic, EIM…) hoặc ví dụ Ops Hub, có **con số**.
4. **Trade-off**: khi nào dùng, khi nào không.
5. **Failure mode**: hỏng thế nào, phát hiện bằng công cụ gì.
Với sự cố: **đo trước (p50/p99, từ khi nào, ai bị) → khoanh vùng → gọi tên vấn đề → xác nhận bằng công cụ → xử lý tạm → xử lý gốc → phòng ngừa**.
Với PO: **làm rõ (hỏi lại) → phương án nhỏ giao trước → edge case → đo kết quả**.

### 0.5 Ranh giới trung thực (đọc kỹ)
- Không nhắc chi tiết nội bộ ShedPro (release notes, tên đối tác RTO, bug cụ thể). Chỉ dựa vào phạm vi công khai trong JD, nói dạng "I'd assume… and I'd confirm with the PM".
- Joblogic: **EF6** ở domain Core cũ + EF Core ở phần mới + Dapper; handler tự viết trả `OneOf`; frontend **Razor + jQuery + Vue**; test **MSTest + AutoFixture + AutoMocker**; Azure Functions + Service Bus + MongoDB. Platform microservice **có sẵn** → nói "delivered features", không nói "built the architecture". Không chê code Joblogic.
- PlaySweeps: "sweepstakes gaming platform", **không** nói casino/real-money; không nói DAU/doanh thu. Vai trò **feature lead**, không phải team lead. Balance Sweeps Coin do **Nexus** (PLAYSTUDIOS) sở hữu.
- CI/CD: chỉ từng sửa config Jenkins/Helm values; **không** nhận đã dựng pipeline. GitHub Actions, Kubernetes, PostgreSQL: không nhận là kinh nghiệm chính.
- Không tự nhận "Senior" về chức danh; nói "about four years of professional experience".

---

## A1. Process, thread, bộ nhớ và I/O — nền của mọi câu "vì sao chậm"

**Vì sao phải học phần này trước.** Ở Agapi, câu "request mất 8 giây" bị đào sâu vì interviewer muốn biết bạn hiểu **thời gian của một request đi đâu**: CPU đang tính, hay thread đang **chờ** (wait) một thứ khác (DB, lock, mạng). Mọi chủ đề sau (async, thread pool starvation, connection pool, lock SQL, Redis, load balancer) đều dựa trên mấy khái niệm ở đây. Interviewer Senior hay hỏi kiểu: "CPU chỉ 5% mà request vẫn chậm, vậy nó đang làm gì?" — trả lời được câu đó là qua tầng 1.

### A1.1 Process và thread (tiến trình và luồng)

- **Process (tiến trình)** = một chương trình đang chạy, được hệ điều hành (OS) cấp **không gian bộ nhớ riêng** (virtual address space), danh sách file/socket đang mở (handle / file descriptor), và ít nhất một thread. App ASP.NET Core của bạn chạy là **một process** `dotnet MyApi.dll`. Hai process không đọc được bộ nhớ của nhau → muốn nói chuyện phải qua mạng, file, pipe…
- **Thread (luồng)** = một dòng thực thi bên trong process. Các thread trong cùng process **dùng chung heap** (nên phải lo race condition) nhưng mỗi thread có **stack riêng** (biến cục bộ, địa chỉ trả về của hàm). Stack mặc định khoảng **1 MB** mỗi thread trên Windows (Linux tuỳ cấu hình) → 1.000 thread là ~1 GB bộ nhớ dự trữ chỉ cho stack.
- **CPU core** chỉ chạy **một thread tại một thời điểm**. Máy 4 core chạy song song tối đa 4 thread; 500 thread còn lại phải xếp hàng. **Scheduler (bộ lập lịch)** của OS cắt thời gian (time slice ~ vài ms) và đổi thread đang chạy → gọi là **context switch (chuyển ngữ cảnh)**, tốn vài micro-giây mỗi lần + làm nguội cache CPU. Quá nhiều thread → CPU tốn thời gian đổi qua đổi lại thay vì làm việc.

Ví dụ đời thường: process là **một nhà hàng** (bếp, kho riêng); thread là **đầu bếp**; CPU core là **cái bếp lửa**. 4 bếp lửa thì chỉ 4 đầu bếp nấu cùng lúc. Thuê 500 đầu bếp không làm nhà hàng nhanh hơn — họ chen nhau, và mỗi người vẫn tốn lương (stack 1 MB).

### A1.2 Trạng thái của một thread: đang chạy hay đang chờ

Một thread ở một trong các trạng thái chính:
| Trạng thái | Nghĩa | Ví dụ |
|---|---|---|
| **Running** | Đang chạy trên CPU | Đang tính tổng tiền, serialize JSON |
| **Ready / Runnable** | Sẵn sàng nhưng chưa có core trống | Có 50 thread muốn chạy, máy 4 core |
| **Blocked / Waiting** | Đang chờ một sự kiện: I/O xong, lock được nhả, `Thread.Sleep` | `cmd.ExecuteReader()` chờ SQL Server trả kết quả; `.Result` chờ Task |

Điểm mấu chốt: **thread bị Blocked không tốn CPU nhưng vẫn bị chiếm** (giữ stack, giữ chỗ trong thread pool). Đây là lý do có hiện tượng **"CPU thấp nhưng chậm"**: tất cả thread đều đang chờ, không ai làm việc, request mới không có thread để chạy.

**Wall-clock time vs CPU time:** request 8 s có thể chỉ tốn 20 ms CPU, 7,98 s còn lại là **chờ**. Khi chẩn đoán, câu đầu tiên luôn là: thời gian này là **tính** hay **chờ**? Nếu chờ thì chờ **cái gì**? (DB, HTTP ngoài, lock, connection pool, thread pool).

### A1.3 CPU-bound vs I/O-bound

- **CPU-bound**: việc bị giới hạn bởi tốc độ tính toán — nén ảnh, sinh PDF, mã hoá, vòng lặp lớn, regex nặng. Tăng tốc bằng thuật toán tốt hơn, **song song (parallelism)** trên nhiều core, hoặc đẩy ra worker riêng.
- **I/O-bound**: việc bị giới hạn bởi thời gian chờ thiết bị/mạng — query DB, gọi API Nexus, đọc file, gọi Redis. Hầu hết web API là I/O-bound. Tăng **throughput (số request/giây)** bằng **async I/O** (không giữ thread khi chờ); giảm **latency** bằng cách giảm số lần chờ (cache, gộp query, gọi song song các việc độc lập).

Con số nên thuộc (bậc độ lớn, để ước lượng khi bị hỏi):
| Thao tác | Thời gian xấp xỉ |
|---|---|
| Đọc RAM | ~100 ns |
| Đọc SSD ngẫu nhiên | ~0,1 ms |
| Round-trip mạng trong cùng datacenter (app → Redis/SQL) | ~0,5 ms |
| Query SQL đơn giản có index | 1–5 ms |
| Gọi HTTP sang service khác cùng region | 10–50 ms |
| Round-trip Việt Nam ↔ Mỹ | ~200 ms |

→ Một request gọi DB **100 lần tuần tự** (N+1) × 2 ms = 200 ms chỉ để chờ mạng, dù mỗi query "rất nhanh".

### A1.4 Blocking I/O vs non-blocking / async I/O (ở tầng OS)

- **Blocking (đồng bộ)**: thread gọi `read()` trên socket → OS cho thread **ngủ** tới khi dữ liệu về. 1 request đang chờ = 1 thread bị giữ.
- **Async I/O**: thread **đăng ký** "khi socket này có dữ liệu thì báo tôi" rồi **quay về làm việc khác**. OS dùng cơ chế **IOCP (I/O Completion Port)** trên Windows, **epoll** trên Linux, **kqueue** trên macOS: một số ít thread theo dõi hàng nghìn socket. Khi dữ liệu về, OS báo, runtime lấy một thread rảnh chạy tiếp phần còn lại.
- Đây là bản chất của `await` trong .NET và của event loop trong Node.js: **trong lúc chờ I/O, không có thread nào bị chiếm** (xem A4).

Ví dụ đời thường: **blocking** = gọi điện cho nhà cung cấp rồi **cầm máy chờ** 10 phút; **async** = để lại số điện thoại, đi làm việc khác, khi họ gọi lại thì nghe.

### A1.5 Node.js: event loop, và vì sao "deadlock thread" là cách nói sai

Ở Agapi bạn nói "với Node.js có dead block ở thread nào đó". Cần nói chính xác:
- Node chạy **JavaScript trên một thread duy nhất** (main thread / event loop). I/O mạng dùng epoll/IOCP qua **libuv**; một số việc (file system, DNS `lookup`, crypto, zlib) chạy trên **libuv thread pool** (mặc định **4 thread**, đổi bằng `UV_THREADPOOL_SIZE`).
- Lỗi thường gặp **không phải deadlock** mà là **event loop bị chặn (event loop blocking)**: một đoạn code đồng bộ nặng (vòng lặp lớn, `JSON.parse` file 50 MB, `bcrypt.hashSync`, regex thảm hoạ) chiếm main thread 2 giây → **mọi request khác đứng chờ** 2 giây. Đo bằng **event loop lag/delay** (`perf_hooks.monitorEventLoopDelay`, Clinic.js, metric của APM).
- Deadlock kinh điển (A chờ B, B chờ A) trong Node hiếm vì chỉ có một thread JS; nhưng **deadlock logic** vẫn xảy ra ở tầng ngoài: hai request giữ hai lock Redis/SQL theo thứ tự ngược nhau.

Câu nói đúng: *"In Node.js the usual problem isn't a deadlock but a blocked event loop: synchronous CPU-heavy code on the main thread stalls every other request. I'd check event-loop delay metrics."*

### A1.6 Deadlock, starvation, livelock, contention — đặt tên đúng vấn đề

| Tên | Nghĩa | Ví dụ |
|---|---|---|
| **Deadlock (khoá chết)** | Hai (hoặc nhiều) bên chờ nhau vĩnh viễn | T1 giữ dòng A chờ dòng B; T2 giữ B chờ A |
| **Starvation (đói tài nguyên)** | Có tài nguyên nhưng một bên mãi không được cấp đủ | Thread pool starvation: request mới không có thread |
| **Livelock** | Hai bên cứ nhường nhau, không ai tiến | Hai process retry cùng nhịp, đụng nhau mãi (sửa bằng jitter) |
| **Contention (tranh chấp)** | Nhiều bên tranh một tài nguyên → xếp hàng, chậm nhưng vẫn tiến | 500 request cùng `UPDATE` một dòng balance |
| **Blocking (bị chặn)** | Một bên chờ bên khác nhả tài nguyên (chưa phải deadlock) | Transaction dài giữ lock, các query khác chờ |

**4 điều kiện Coffman** — deadlock chỉ xảy ra khi có đủ cả 4: (1) **mutual exclusion** (tài nguyên độc quyền), (2) **hold and wait** (giữ cái này, chờ cái kia), (3) **no preemption** (không giật được), (4) **circular wait** (chờ vòng tròn). Phá một điều kiện là hết deadlock; thực tế hay phá (4) bằng **khoá theo thứ tự cố định** (luôn khoá player id nhỏ trước), hoặc (2) bằng **timeout** (lock có hạn).

### A1.7 Little's Law — công thức ước lượng nên thuộc

**L = λ × W**: số việc đang xử lý đồng thời (L) = tốc độ đến (λ, request/giây) × thời gian mỗi việc (W).
- API nhận **200 req/s**, mỗi request giữ **connection DB 50 ms** → trung bình **10 connection** đang dùng. Pool 100 là thừa.
- Nếu DB chậm lại thành **500 ms** → cần **100 connection** → **cạn pool (pool exhaustion)**, request thứ 101 phải chờ, mặc định chờ **15 s** (`Connect Timeout`) rồi lỗi `Timeout expired… max pool size was reached`.
- Bài học: **một chỗ chậm lan ra cả hệ thống** (cascading failure). Request chậm → giữ tài nguyên lâu → cạn pool/thread → request khác cũng chậm.

Nói được con số này trong phỏng vấn là dấu hiệu Senior ("pods × MaxPoolSize ≤ max_connections của DB").

### A1.8 Bộ nhớ: stack, heap, GC (mức OS)

- **Stack**: theo thread, cấp/thu hồi tự động khi vào/ra hàm, rất nhanh. Đệ quy sâu → **StackOverflowException** (trong .NET không bắt được, process chết).
- **Heap**: dùng chung, object sống lâu hơn hàm. Trong .NET do **GC (garbage collector)** dọn (A3). GC có lúc phải **dừng các thread** (pause) → nguồn gây **p99 cao** thỉnh thoảng.
- **Memory leak trong ngôn ngữ có GC** = vẫn còn tham chiếu tới object không dùng (cache không giới hạn, static list, event handler không gỡ) → GC không dọn được.
- Process dùng quá giới hạn RAM của container → bị **OOM kill** (Kubernetes/ECS khởi động lại) → request đang chạy bị cắt.

### A1.9 Bẫy hay sai
- "Thêm thread là nhanh hơn" → sai với I/O-bound (chỉ thêm context switch, bộ nhớ); đúng phần nào với CPU-bound tới số core.
- "Async làm một request nhanh hơn" → sai; async tăng **throughput**, latency một request gần như không đổi.
- "Node.js bị deadlock thread" → nói "event loop blocked".
- "Lock Redis bị giữ mãi khi thread crash" → sai nếu lock có **TTL** (RedLock luôn có TTL); vấn đề thật là **giữ quá lâu cho tới khi TTL hết** hoặc **TTL hết khi việc chưa xong** (xem C4).
- Không phân biệt deadlock với blocking: SQL Server **tự phát hiện deadlock** sau vài giây và giết một bên (lỗi 1205); còn blocking thì chờ mãi tới timeout.

### A1.10 Câu hỏi phỏng vấn & trả lời mẫu

**Q1. What's the difference between a process and a thread?**
Ý chính: process có bộ nhớ riêng, thread chia sẻ heap trong process, có stack riêng; tạo thread rẻ hơn process nhưng vẫn tốn (~1 MB stack, context switch); thread chung heap nên cần đồng bộ.
> A process is a running program with its own memory space and resources; threads are units of execution inside a process. Threads share the heap, so they can work on the same data — which is why we need synchronisation — but each has its own stack. Threads are cheaper than processes, but not free: each reserves stack memory, and the OS pays a context switch every time it swaps them on a core. That's why in .NET we don't create a thread per request; we use the thread pool and async I/O.

**Q2. A request is slow but the server's CPU is at 5%. What is it doing?**
Ý chính: thời gian là **chờ**, không phải tính. Liệt kê thứ có thể đang chờ và công cụ xác nhận.
> If CPU is low, the request isn't computing, it's waiting. The usual suspects are: waiting on the database — a slow query or blocked by a lock; waiting on an external HTTP call without a proper timeout; waiting for a connection from an exhausted connection pool; or waiting for a thread because the thread pool is starved by blocking calls like `.Result`. I'd confirm with a distributed trace to see which span takes the time, `dotnet-counters` for thread-pool queue length and connection-pool counters, and on the SQL side `sys.dm_exec_requests` for blocking and wait types.

**Q3. CPU-bound vs I/O-bound — how does each change your solution?**
> For I/O-bound work, like most web APIs, async I/O lets a few threads serve thousands of concurrent requests, and I reduce latency by cutting the number of round trips — batching, caching, running independent calls in parallel. For CPU-bound work, async doesn't help; I'd optimise the algorithm, use parallelism up to the number of cores, or move it to a background worker so it doesn't hold web requests — for example PDF generation.

**Q4. (Đào sâu Agapi) You mentioned a deadlock in Node.js. What exactly happens?**
> I should be precise: Node runs JavaScript on a single event-loop thread, so the common failure isn't a classic deadlock but a blocked event loop. If one handler runs synchronous CPU-heavy code — parsing a huge JSON or hashing with a sync API — every other request waits behind it. You see it as event-loop delay rising while CPU is high on one core. The fix is to keep the main thread non-blocking: use async APIs, move heavy work to worker threads or a queue. A real deadlock can still happen at the resource level, for example two requests taking two Redis or database locks in opposite order.

**Q5. What is a deadlock and how do you prevent it?**
> A deadlock is when two parties each hold something the other needs and wait forever. It requires four conditions together: exclusive resources, holding while waiting, no pre-emption and a circular wait. In practice I break the circular wait by always acquiring locks in a fixed order, keep transactions short, and put timeouts on every lock. Databases detect deadlocks and kill one victim, so the application must be ready to retry that transaction.

**Q6. How many database connections does this service need?** (câu ước lượng)
> I'd use Little's Law: concurrent connections ≈ requests per second × time each request holds a connection. At 200 requests per second holding a connection for 50 ms, that's about 10 on average, so a pool of 100 has plenty of headroom. The danger is when the database slows down: at 500 ms per request we'd need 100, the pool runs out, and requests start timing out even though the app itself is fine. Across instances, pods times max pool size must stay under the database's connection limit.

**Q7. Why doesn't adding more threads make the API faster?**
> For I/O-bound work, more threads just means more threads waiting, more memory for stacks and more context switching. The real limit is usually the thing being waited on — the database or an external API. For CPU-bound work, you gain only up to the number of cores. The scalable approach is async I/O so threads aren't held while waiting.

### A1.11 Tự kiểm tra (Claude sẽ hỏi)
1. Thread bị blocked có tốn CPU không? Có tốn gì khác không?
2. Giải thích "CPU 5% nhưng p99 = 8 s" theo ít nhất 4 nguyên nhân + công cụ xác nhận.
3. Node.js: event loop blocking khác deadlock thế nào?
4. Bốn điều kiện Coffman; thực tế phá điều kiện nào?
5. Dùng Little's Law: 300 req/s, mỗi request giữ connection 80 ms → bao nhiêu connection? DB chậm gấp 5 thì sao?

---

## A2. Mạng và HTTP — nền của auth, cookie, load balancer, timeout

**Vì sao cần.** Câu "JWT hay cookie", "stateful hay stateless", "load balancer chia request thế nào", "vì sao không `new HttpClient()` mỗi lần" đều là câu hỏi về **HTTP và TCP**. Nếu không biết cookie thực chất là một header, hay HTTP vốn **không nhớ gì giữa hai request (stateless)**, thì trả lời auth sẽ lạc đề như ở Agapi.

### A2.1 Một request đi qua những gì (từ trình duyệt tới API)

Ví dụ trình duyệt gọi `https://api.opshub.com/quotes/42`:
1. **DNS**: đổi tên miền → địa chỉ IP (có cache theo **TTL**). Đổi DNS mà client cache IP cũ → vẫn gọi vào máy cũ.
2. **TCP 3-way handshake (bắt tay 3 bước)**: SYN → SYN-ACK → ACK, mất **1 round-trip (RTT)**. Việt Nam → Mỹ RTT ~200 ms → riêng bắt tay đã 200 ms.
3. **TLS handshake**: thoả thuận khoá mã hoá, kiểm chứng chỉ (certificate). TLS 1.3 mất **1 RTT** (TLS 1.2: 2 RTT). Tổng cộng trước khi gửi byte dữ liệu đầu tiên: 2–3 RTT.
4. **HTTP request**: dòng đầu `GET /quotes/42 HTTP/1.1`, các **header** (`Host`, `Authorization`, `Cookie`, `Accept`…), body (nếu có).
5. Đi qua **load balancer / reverse proxy** (ALB, Nginx, Azure Front Door) → tới một instance app (Kestrel) → middleware → controller.
6. **Response**: status code, header (`Set-Cookie`, `Cache-Control`, `ETag`…), body.

→ Vì handshake đắt, client nên **giữ kết nối mở và dùng lại (keep-alive / connection reuse)**. Đây là lý do có connection pool cho HTTP, DB, Redis.

### A2.2 HTTP là stateless — hiểu đúng chữ này

**Stateless (phi trạng thái)** nghĩa là: **giao thức HTTP không nhớ request trước**. Mỗi request phải tự mang đủ thông tin để server biết "bạn là ai". Server không tự biết request #2 đến từ cùng người với request #1.
→ Muốn "đăng nhập một lần, dùng nhiều lần" thì client phải **gửi kèm một thứ ở mỗi request**:
- một **session id** (chuỗi ngẫu nhiên) → server tra **kho session** để biết là ai → mô hình **stateful** (server giữ trạng thái đăng nhập), hoặc
- một **token tự chứa (self-contained)** như JWT, có chữ ký → server chỉ cần **kiểm chữ ký**, không cần tra kho → mô hình **stateless**.
Cả hai đều có thể đi trong **cookie** hoặc trong header **`Authorization: Bearer`**. Chi tiết ở **C1**.

### A2.3 Cookie thực chất là gì

- Server gửi header `Set-Cookie: sid=abc123; HttpOnly; Secure; SameSite=Lax; Path=/; Max-Age=3600`.
- Trình duyệt lưu lại và **tự động** gửi `Cookie: sid=abc123` ở mọi request sau tới đúng domain/path. **Tự động** là điểm mạnh (không cần code JS) và cũng là điểm yếu (**CSRF**: site lạ khiến trình duyệt gửi request kèm cookie của bạn).
- Các thuộc tính phải thuộc:
| Thuộc tính | Tác dụng |
|---|---|
| `HttpOnly` | JavaScript **không đọc được** cookie → XSS không lấy cắp được giá trị |
| `Secure` | Chỉ gửi qua HTTPS |
| `SameSite=Strict / Lax / None` | Có gửi cookie khi request đến từ site khác không. `Lax` (mặc định của trình duyệt hiện đại): gửi khi người dùng bấm link điều hướng (GET top-level), **không** gửi với POST từ site khác → chặn phần lớn CSRF. `None` phải đi cùng `Secure`, dùng khi cần cross-site thật |
| `Domain`, `Path` | Phạm vi gửi |
| `Expires` / `Max-Age` | Không có → **session cookie** (mất khi đóng trình duyệt) |
- Giới hạn ~**4 KB** mỗi cookie → JWT to (nhiều claim) bỏ vào cookie có thể vượt.

### A2.4 HTTP/1.1, HTTP/2, HTTP/3
| | HTTP/1.1 | HTTP/2 | HTTP/3 |
|---|---|---|---|
| Kết nối | Mỗi kết nối xử lý 1 request tại một lúc (trình duyệt mở ~6 kết nối/domain) | **Multiplexing**: nhiều request song song trên **một** kết nối TCP | Chạy trên **QUIC (UDP)** |
| Header | Text, lặp lại | Nén (HPACK) | Nén (QPACK) |
| Điểm yếu | Head-of-line blocking ở tầng HTTP | Mất một gói TCP thì mọi stream chờ (HOL ở tầng TCP) | Giải quyết HOL của TCP, bắt tay nhanh hơn |
- **gRPC** chạy trên HTTP/2. Load balancer L4 với HTTP/2 sẽ dồn mọi request của một client vào một instance (vì chỉ có một kết nối dài) → cần LB L7 hiểu HTTP/2 (xem C6).

### A2.5 Kết nối, socket và `HttpClient`
- Mỗi kết nối TCP là một **socket**. Khi đóng, phía chủ động đóng giữ socket ở trạng thái **TIME_WAIT** khoảng 1–4 phút (tuỳ OS) để chặn gói tin trễ.
- `new HttpClient()` mỗi request rồi `Dispose` → mỗi lần mở kết nối mới + để lại TIME_WAIT → tải cao thì **cạn cổng (socket/port exhaustion)**: lỗi `SocketException: Only one usage of each socket address…` hoặc `Address already in use`.
- Ngược lại một `HttpClient` **static sống mãi** thì không cập nhật **DNS** khi IP đổi.
- Đúng: **`IHttpClientFactory`** (typed client) — dùng lại `SocketsHttpHandler` có pool kết nối, xoay handler định kỳ (mặc định 2 phút) để nhận DNS mới; hoặc một `HttpClient` singleton với `PooledConnectionLifetime`.
- **Timeout**: `HttpClient.Timeout` mặc định **100 giây** — quá dài cho API. Đặt timeout theo SLA (vd. 2–5 s) + `CancellationToken`. Không có timeout = một provider chậm có thể giữ thread/kết nối của bạn rất lâu → cạn tài nguyên.

### A2.6 CORS (Cross-Origin Resource Sharing)
- **Same-origin policy**: JavaScript ở `https://app.opshub.com` mặc định **không đọc được response** từ origin khác (`https://api.opshub.com` khác subdomain = khác origin).
- **CORS** là cách **server nói với trình duyệt** "origin X được phép": header `Access-Control-Allow-Origin`. Request "không đơn giản" (có `Authorization`, `Content-Type: application/json`, method PUT/DELETE) → trình duyệt gửi **preflight `OPTIONS`** trước.
- CORS **không phải cơ chế bảo vệ server**: curl/Postman không quan tâm CORS. Nó chỉ bảo vệ **người dùng trình duyệt**. Không dùng `*` khi có `Allow-Credentials: true` (trình duyệt cũng không cho).

### A2.7 Header hay dùng trong hệ thống thật
- `X-Forwarded-For`, `X-Forwarded-Proto`: proxy/LB thêm vào để app biết IP thật của client và client dùng https. ASP.NET Core: `UseForwardedHeaders` (cấu hình `KnownProxies` để không bị giả mạo IP — quan trọng khi rate limit theo IP).
- `traceparent` (W3C Trace Context): mang trace id qua các service.
- `Idempotency-Key`, `If-Match`/`ETag`, `Retry-After`, `Cache-Control` (B4).
- **Kết nối dài**: WebSocket (hai chiều), **Server-Sent Events** (server → client một chiều), **SignalR** (thư viện .NET tự chọn WebSocket/SSE/long polling). Với nhiều instance, SignalR cần **backplane** (Redis/Azure SignalR) để gửi tới client đang nối ở instance khác.

### A2.8 OSI rút gọn: L4 vs L7 (dùng cho câu load balancer)
- **L4 (transport: TCP/UDP)**: chỉ thấy IP + port. Nhanh, không đọc nội dung, không biết URL hay cookie.
- **L7 (application: HTTP)**: đọc được URL, header, cookie → định tuyến theo path (`/api` → service A), sticky theo cookie, kết thúc TLS, nén, WAF.
- AWS: **NLB** = L4, **ALB** = L7. Azure: Load Balancer = L4, Application Gateway / Front Door = L7.

### A2.9 Bẫy hay sai
- "JWT là một cách lưu" → sai: JWT là **định dạng token**; cookie / localStorage / header là **nơi chứa/cách gửi**.
- "HTTP stateless nên app của tôi stateless" → hai chuyện khác nhau: app stateless nghĩa là **instance không giữ trạng thái riêng trong RAM** (session, file, cache cục bộ quan trọng), để LB gửi request tới instance nào cũng được.
- "CORS bảo vệ API" → không; bảo vệ API là authN/authZ.
- Quên timeout cho HTTP client → nguyên nhân phổ biến của request treo 100 s.

### A2.10 Câu hỏi phỏng vấn & trả lời mẫu

**Q1. What happens when the browser calls our API over HTTPS?**
> The browser resolves the domain through DNS, opens a TCP connection with a three-way handshake, then does a TLS handshake to agree on keys and verify the certificate — that's two or three round trips before any data, which is why connections are kept alive and reused. Then it sends the HTTP request with headers like Host, Authorization or Cookie. It usually reaches a load balancer or reverse proxy first, which forwards it to one of our app instances, through the middleware pipeline to the controller, and the response comes back the same way.

**Q2. What does "HTTP is stateless" mean, and how does login work then?**
> It means the protocol doesn't remember anything between requests, so each request has to carry enough information to identify the user. After login, the client sends either a session ID, which the server looks up in a session store — that's stateful — or a signed token like a JWT, which the server can verify without any lookup — that's stateless. Both can travel in a cookie or in the Authorization header.

**Q3. Which cookie attributes matter for security?**
> `HttpOnly`, so JavaScript can't read the cookie and an XSS bug can't steal it; `Secure`, so it only goes over HTTPS; and `SameSite`, which controls whether the browser sends it on cross-site requests — `Lax` or `Strict` blocks most CSRF. Then a sensible expiry and the narrowest domain and path.

**Q4. Why shouldn't you create a new HttpClient per request?**
> Each new client opens new TCP connections and leaves sockets in TIME_WAIT when disposed, so under load you can exhaust ports. A single static client fixes that but never picks up DNS changes. `IHttpClientFactory` pools and recycles the handlers, so you get connection reuse and DNS refresh. And I always set a timeout — the default of 100 seconds is far too long for an API call.

**Q5. What is CORS? Does it protect the API?**
> CORS is how a server tells the browser which other origins may read its responses; the browser enforces it, often with a preflight OPTIONS request. It protects users in the browser, not the API — any script or curl can call the API directly — so the API still needs proper authentication and authorisation.

**Q6. HTTP/1.1 vs HTTP/2?**
> HTTP/2 multiplexes many requests over one TCP connection and compresses headers, so it avoids opening many connections and the head-of-line blocking of HTTP/1.1 at the HTTP level. A side effect is that one client keeps one long-lived connection, so a layer-4 load balancer would pin all its requests to one instance; you need a layer-7 balancer that understands HTTP/2, which matters for gRPC.

### A2.11 Tự kiểm tra
1. Cookie và JWT có phải hai thứ cùng loại không? Giải thích.
2. Ba thuộc tính cookie quan trọng và mỗi cái chặn tấn công gì?
3. `new HttpClient()` mỗi request gây lỗi gì? `static HttpClient` gây lỗi gì? Cách đúng?
4. L4 và L7 khác nhau ở chỗ nào, ví dụ dịch vụ AWS/Azure?
5. "App stateless" nghĩa là gì, khác "HTTP stateless" ra sao?

---

## A3. C# và .NET runtime — CLR, bộ nhớ, GC, kiểu dữ liệu, LINQ

**Vì sao cần.** Vị trí là **C# Developer**, nên dù SA gốc frontend, vòng tech gần như chắc có vài câu nền để lọc ("value vs reference type", "GC hoạt động thế nào", "IEnumerable vs IQueryable", "vì sao decimal cho tiền"). Câu trả lời Mid là định nghĩa; câu trả lời Senior **giải thích cơ chế + hậu quả thực tế + ví dụ đã gặp**.

### A3.1 Code C# chạy thế nào: IL, CLR, JIT
1. `dotnet build` biên dịch C# thành **IL (Intermediate Language)** nằm trong file `.dll` + metadata (kiểu, method).
2. Khi chạy, **CLR (Common Language Runtime)** nạp dll, và **JIT (Just-In-Time compiler)** dịch IL của từng method sang **mã máy** ở **lần gọi đầu tiên** → lần gọi đầu chậm hơn (một phần của **cold start**).
3. **Tiered compilation** (.NET Core 3+): lần đầu JIT nhanh, ít tối ưu (tier 0); method gọi nhiều thì JIT lại tối ưu (tier 1). **Dynamic PGO** (mặc định từ .NET 8) dùng dữ liệu chạy thật để tối ưu tiếp.
4. **ReadyToRun (R2R)**: biên dịch sẵn một phần sang mã máy lúc publish → khởi động nhanh hơn, file to hơn. **Native AOT** (.NET 7+): biên dịch hết sang mã máy, khởi động rất nhanh, bộ nhớ ít, nhưng hạn chế reflection/dynamic (EF Core, một số thư viện chưa hỗ trợ đủ). Dùng cho Lambda/CLI/microservice nhỏ.
- CLR còn lo: **GC**, kiểm tra kiểu (type safety), exception, thread, bảo mật kiểu.
- .NET Framework (chỉ Windows, `System.Web`) vs .NET (Core) 5+ (cross-platform). **.NET 8 LTS** (hỗ trợ tới 11/2026), **.NET 10 LTS** (11/2025). Codebase partner có thể còn .NET Framework → biết để nói chuyện migrate.

### A3.2 Value type vs reference type — chính xác về bộ nhớ
| | Value type | Reference type |
|---|---|---|
| Ví dụ | `int`, `decimal`, `bool`, `DateTime`, `Guid`, `enum`, `struct`, `record struct` | `class`, `record` (class), `string`, mảng, `delegate` |
| Biến chứa gì | **Chính dữ liệu** | **Địa chỉ (tham chiếu)** tới object trên heap |
| Gán `b = a` | **Copy toàn bộ giá trị** | Copy **địa chỉ** → hai biến cùng trỏ một object |
| Nằm ở đâu | **Nơi nó được khai báo**: biến cục bộ → stack (thường); field của class → **trong object trên heap**; phần tử mảng → trong mảng trên heap | Object luôn trên **managed heap** |
| null | Không (trừ `int?` = `Nullable<int>`) | Có |

- "Value type luôn nằm trên stack" là **sai** — interviewer hay gài câu này. Ví dụ `class Order { decimal Total; }` → `Total` nằm trong object `Order` trên heap. Biến cục bộ bị lambda/async capture cũng lên heap (thành field của closure/state machine).
- **Boxing**: gán value type vào `object`/interface → cấp một object mới trên heap chứa bản copy. `ArrayList.Add(5)`, `string.Format("{0}", 5)` kiểu cũ, `Dictionary<object,…>`. Trong vòng lặp nóng → nhiều rác → GC nhiều. Generics (`List<int>`) không boxing.
- **struct** hợp: nhỏ (≲ 16 byte), bất biến, có ngữ nghĩa giá trị (`Money`, toạ độ). Struct lớn bị copy mỗi lần truyền → chậm; struct mutable gây bug (sửa bản copy chứ không phải bản gốc).

### A3.3 string, record, equality
- **string bất biến (immutable)**: `s += "x"` tạo string mới. Nối 10.000 lần trong vòng lặp → O(n²) copy → dùng `StringBuilder` hoặc `string.Join`. Lợi: thread-safe, dùng làm key an toàn, **string interning** cho literal.
- So sánh chuỗi: `string.Equals(a, b, StringComparison.OrdinalIgnoreCase)` cho mã/khoá; culture-aware chỉ khi hiển thị/sắp xếp cho người đọc (bẫy "Turkish i").
- **record**: class (hoặc struct) với **equality theo giá trị** (compiler sinh `Equals`, `GetHashCode`, `==`), `ToString` đẹp, `with` để copy-sửa, `init`. Hợp **DTO, message, value object**. Không hợp **entity EF** (entity có identity theo Id và thay đổi theo thời gian).
- Override `Equals` thì **phải** override `GetHashCode` (cùng giá trị → cùng hash), nếu không `Dictionary/HashSet` hỏng.

### A3.4 GC (Garbage Collector) — cơ chế và hậu quả production
- **Managed heap** chia thế hệ (generation):
  - **Gen 0**: object mới. Phần lớn object chết trẻ (DTO của một request) → dọn Gen 0 rất nhanh (vài trăm µs–vài ms).
  - **Gen 1**: vùng đệm.
  - **Gen 2**: object sống lâu (cache, singleton). Dọn Gen 2 = **full GC**, tốn nhất.
  - **LOH (Large Object Heap)**: object ≥ **85.000 byte** (mảng/chuỗi lớn: đọc file vào `byte[]`, JSON to). Chỉ dọn cùng Gen 2, mặc định **không nén (compact)** → **phân mảnh**. **POH** (pinned object heap, .NET 5+).
- Cách GC chạy: đánh dấu (mark) object còn được tham chiếu từ **root** (biến trên stack, static, handle) → dọn phần còn lại → nén (compact) để hết lỗ. Trong lúc đó các thread managed có thể bị **tạm dừng (pause)**. .NET có **background GC** cho Gen 2 để giảm pause nhưng Gen 0/1 vẫn dừng ngắn.
- **Workstation GC** (app desktop) vs **Server GC** (ASP.NET Core mặc định khi chạy server: một heap + một thread GC mỗi core, throughput cao, tốn RAM hơn). Trong container giới hạn CPU/RAM, có thể chỉnh `GCHeapHardLimit`, hoặc dùng **DATAS** (.NET 8 tuỳ chọn, mặc định bật với Server GC từ .NET 9) để heap co giãn theo tải.
- **Hậu quả production**: cấp phát nhiều (allocation rate cao) → GC chạy thường xuyên → CPU tăng + **pause làm p99 cao**. Xem `dotnet-counters`: `% Time in GC`, `Gen 0/1/2 GC Count`, `Allocation Rate`, `GC Heap Size`. Gen 2 count tăng đều + heap không giảm → nghi **leak**.
- Giảm cấp phát: tránh `ToList()` thừa, tránh LINQ trong vòng lặp nóng, `StringBuilder`, `ArrayPool<T>`, `Span<T>`, stream thay vì đọc hết file vào RAM.

### A3.5 IDisposable, using, finalizer
- **GC chỉ dọn bộ nhớ managed**, không biết khi nào nên **đóng** connection DB, file handle, socket. Những thứ đó implement `IDisposable` → gọi `Dispose()` để **giải phóng ngay**.
- `using var conn = new SqlConnection(...)` → compiler sinh `try/finally { conn.Dispose(); }`. Với `SqlConnection`, Dispose **trả connection về pool** (không đóng TCP thật). Quên Dispose → connection chỉ quay lại pool khi GC chạy finalizer → **cạn pool** dù tải thấp.
- `await using` cho `IAsyncDisposable` (`DbContext`, `Utf8JsonWriter`…).
- **Finalizer** (`~Class()`) chỉ là lưới an toàn cho tài nguyên unmanaged; object có finalizer sống thêm một vòng GC (đi qua finalization queue) → chậm. Pattern chuẩn: `Dispose()` + `GC.SuppressFinalize(this)`.
- DI container tự Dispose các service `IDisposable` nó tạo (Scoped khi hết request, Singleton khi app tắt). Đừng tự Dispose object do container quản lý.

### A3.6 Exception — chi phí và cách dùng
- Throw exception **đắt** (chụp stack trace, unwind): ~ micro-giây tới chục micro-giây mỗi lần, so với nano-giây cho `if`. Không dùng exception cho luồng nghiệp vụ bình thường (ví dụ "số dư không đủ" xảy ra thường xuyên) → dùng **Result type** (Joblogic dùng `OneOf`).
- `throw;` giữ nguyên stack trace; `throw ex;` **reset** stack trace (mất dấu chỗ lỗi gốc).
- Exception filter `catch (SqlException e) when (e.Number == 1205)` → bắt riêng deadlock để retry, không unwind nếu không khớp.
- `catch (Exception) { }` nuốt lỗi → lỗi im lặng, khó điều tra.

### A3.7 Collections — độ phức tạp và cấu trúc bên trong
| Collection | Tra/ thêm | Ghi chú |
|---|---|---|
| `List<T>` | index O(1), `Contains` O(n), `Add` O(1) khấu hao | Mảng bên dưới, đầy thì cấp mảng gấp đôi + copy → biết trước size thì `new List<T>(capacity)` |
| `Dictionary<K,V>` | O(1) trung bình | Mảng **bucket** theo `GetHashCode()`; hash tệ (mọi key cùng hash) → O(n). **Không thread-safe** khi có ghi: ghi đồng thời có thể làm hỏng cấu trúc, thậm chí vòng lặp vô hạn |
| `HashSet<T>` | O(1) | Tập không trùng; dùng thay `List.Contains` trong vòng lặp (O(n²) → O(n)) |
| `ConcurrentDictionary` | O(1) | Khoá theo vùng; `GetOrAdd(key, factory)` — factory **có thể chạy nhiều lần** song song (bọc `Lazy<T>` nếu đắt) |
| `ImmutableArray/ImmutableList` | | An toàn chia sẻ, mỗi lần sửa tạo bản mới |
| `Queue`, `Stack`, `PriorityQueue` (.NET 6) | | |

Ví dụ thật: kiểm tra 10.000 player id có trong danh sách 50.000 id bị chặn bằng `List.Contains` = 500 triệu phép so sánh; đổi sang `HashSet` = ~10.000 lần tra.

### A3.8 LINQ: deferred execution, IEnumerable vs IQueryable
- **Deferred execution (thực thi trì hoãn)**: `var q = orders.Where(o => o.Total > 100);` **chưa chạy gì**, chỉ là "công thức". Chạy khi **tiêu thụ**: `ToList`, `First`, `Count`, `Any`, `Sum`, `foreach`. Dùng `q` hai lần = chạy hai lần (với EF = **2 câu SQL**, và dữ liệu có thể khác nhau giữa hai lần).
- **`IEnumerable<T>` + `Func<T,bool>`**: lambda đã biên dịch thành code → chạy **trong RAM**, từng phần tử.
- **`IQueryable<T>` + `Expression<Func<T,bool>>`**: lambda được giữ dưới dạng **cây biểu thức (expression tree)** = dữ liệu mô tả code → **provider (EF Core)** đọc cây và **dịch sang SQL**.
- Bẫy kinh điển khi tiếp quản code: repository trả `IEnumerable<Order>` → `repo.GetAll().Where(o => o.StoreId == id)` → EF chạy `SELECT * FROM Orders` (cả bảng), rồi lọc trong RAM. Code **đúng nhưng chậm dần theo dữ liệu**. C# chọn `Where` theo **kiểu biến lúc compile**, không theo object thật.
- EF Core 3+ **ném lỗi** khi không dịch được biểu thức sang SQL (EF Core ≤ 2 âm thầm chạy trong RAM → "client evaluation").
- `Any()` thay `Count() > 0` (dừng ở dòng đầu, SQL `EXISTS`); `First` (ném nếu rỗng) vs `FirstOrDefault` vs `Single` (ném nếu > 1, phải đọc 2 dòng để chắc).

### A3.9 Delegate, lambda, closure
- **Delegate** = kiểu "con trỏ hàm" an toàn kiểu: `Func<int, decimal>`, `Action<string>`, `Predicate<T>`.
- **Event** = delegate mà chỉ class chủ được gọi (invoke); bên ngoài chỉ `+=`/`-=`. Đăng ký `+=` vào event của object sống lâu (singleton) mà không `-=` → object đăng ký **không bao giờ được GC** → **memory leak** kinh điển.
- **Closure**: lambda "bắt" biến bên ngoài → compiler chuyển biến đó thành **field của một class ẩn** trên heap. Cẩn thận bắt biến trong vòng lặp hoặc bắt `DbContext`/`HttpContext` vào task chạy sau (đã bị dispose).

### A3.10 Kiểu số: decimal vs double cho tiền
- `double`/`float` là **số nhị phân dấu phẩy động (binary floating point)**: không biểu diễn chính xác 0.1 → `0.1 + 0.2 == 0.30000000000000004`. Cộng dồn 1 triệu giao dịch → lệch vài cent.
- `decimal` là **số thập phân** 128-bit, 28–29 chữ số có nghĩa, biểu diễn chính xác 0.1 → dùng cho **tiền**. Chậm hơn double ~10 lần nhưng với nghiệp vụ không đáng kể.
- **Làm tròn**: `Math.Round(2.345m, 2)` mặc định **banker's rounding (`MidpointRounding.ToEven`)** → 2.34; kế toán thường cần `AwayFromZero` → 2.35. Làm tròn **một chỗ**, theo quy tắc PO/kế toán chốt.
- SQL: `DECIMAL(18,2)` (đơn giá có thể `DECIMAL(19,4)`); EF `HasPrecision(18,2)`; không dùng `money` của SQL Server nếu phải chia/nhân nhiều (làm tròn 4 chữ số trung gian).
- Overflow: `int` cộng tràn **âm thầm** (unchecked mặc định) → `checked { }` hoặc `long`; `decimal` tràn thì ném `OverflowException`.

### A3.11 OOP và C# hiện đại (trả lời nhanh, 1–2 câu mỗi ý)
- **4 tính chất OOP**: Encapsulation (giấu trạng thái, đổi qua method có luật: `Order.Cancel()` thay vì `order.Status = ...`), Abstraction (interface che chi tiết: `IPaymentProvider`), Inheritance (dùng tiết kiệm, ưu tiên composition), Polymorphism (cùng lời gọi, hành vi theo kiểu thật: Strategy).
- **abstract class vs interface**: abstract có state + code chung, kế thừa đơn; interface là hợp đồng, một class implement nhiều interface, có default method (C# 8). DI/test → interface.
- **virtual/override vs new**: override là đa hình (gọi qua biến kiểu cha vẫn chạy bản con); `new` chỉ **che (hide)** — gọi qua kiểu cha chạy bản cha → bug khó thấy.
- **const vs readonly**: const là hằng **compile-time**, được **nhúng vào assembly gọi** (đổi const trong thư viện mà không build lại app gọi → app vẫn dùng giá trị cũ); readonly gán lúc runtime (constructor).
- **Nullable reference types** (`string?`, `<Nullable>enable`): chỉ là **cảnh báo compile**, runtime vẫn có thể null.
- **sealed** chặn kế thừa (rõ ý + JIT tối ưu được gọi hàm). **Extension method** = static method gọi như instance (LINQ, `services.AddXxx()`).
- **Generic constraint** `where T : class, new()`; **covariance** `IEnumerable<out T>` (cho `IEnumerable<Dog>` vào chỗ `IEnumerable<Animal>`).
- **ref/out/in**; **Span<T>/Memory<T>** (thao tác vùng nhớ không cấp phát, ví dụ parse chuỗi lớn).
- **Pattern matching**: `order is { Status: OrderStatus.Delivered, Total: > 1000 }`, switch expression.
- C# 10–12: `record struct`, file-scoped namespace, global using, `required`, raw string literal `"""`, **primary constructor** (C# 12: `class OrderService(AppDbContext db)` — tham số **không** phải readonly field, có thể bị gán lại), collection expression `[1, 2, 3]`.

### A3.12 Bẫy hay sai
- "Value type nằm trên stack, reference trên heap" → nói đúng: value type nằm **ở nơi nó được khai báo**.
- "GC dọn connection cho mình" → GC không biết thời điểm; phải `Dispose`.
- "Dictionary dùng đa luồng cũng được nếu chỉ thỉnh thoảng ghi" → không; một lần ghi đồng thời là đủ làm hỏng.
- `double` cho tiền; không biết banker's rounding.
- Không phân biệt IEnumerable/IQueryable → không giải thích được vì sao query chậm sau khi đổi kiểu trả về repository.

### A3.13 Câu hỏi phỏng vấn & trả lời mẫu

**Q1. Value type vs reference type — where do they live?**
> A value type variable holds the data itself and is copied on assignment; a reference type variable holds a reference to an object on the managed heap, so two variables can point to the same object. The common claim that value types live on the stack isn't quite right: a value type lives wherever it's declared — a local variable usually on the stack, but a field of a class lives inside that object on the heap, and captured locals in lambdas or async methods are moved to the heap too. Boxing a value type into `object` allocates a heap copy, which matters in hot loops.

**Q2. How does garbage collection work in .NET, and how can it affect production?**
> The GC is generational. New objects go to gen 0, which is collected very often and cheaply because most objects die young, like request DTOs. Survivors are promoted to gen 1 and gen 2; a gen 2 collection is a full GC and the most expensive. Objects over 85 KB go to the large object heap, which is collected with gen 2 and not compacted by default, so it can fragment. Collections pause managed threads briefly, so a high allocation rate shows up as more CPU and worse p99 latency. I'd look at `dotnet-counters` for allocation rate, GC counts and time in GC, and reduce allocations — avoid unnecessary `ToList`, stream big payloads instead of loading them, pool buffers.

**Q3. What's the difference between IDisposable and garbage collection?**
> The GC frees memory, at a time it chooses. `IDisposable` is for releasing resources deterministically — database connections, file handles, sockets — because those are limited and the GC doesn't know they're urgent. With `SqlConnection`, Dispose returns the connection to the pool; if you forget it, the pool can run dry under modest load and requests time out after 15 seconds waiting for a connection. So I use `using` or `await using`, and let the DI container dispose what it creates.

**Q4. IEnumerable vs IQueryable?**
> `IQueryable` keeps the lambda as an expression tree, so a provider like EF Core can translate the whole chain into SQL — filtering, sorting and paging happen in the database. `IEnumerable` runs compiled delegates in memory. The classic bug is a repository returning `IEnumerable`: a `Where` after it pulls the entire table and filters in memory. It's correct but gets slower as data grows, and it's one of the first things I look for when taking over a codebase. Both are deferred, so enumerating twice runs the query twice.

**Q5. Why decimal for money?**
> `double` is binary floating point and can't represent values like 0.1 exactly, so sums drift by fractions of a cent, which is unacceptable for invoices or balances. `decimal` is a base-10 type with 28–29 significant digits, so it's exact for currency. I'd also centralise rounding with an explicit rule, because `Math.Round` defaults to banker's rounding, which isn't always what accounting expects.

**Q6. class vs struct vs record?**
> A class is a reference type with identity — good for entities and services. A struct is a value type copied on assignment — good for small immutable values like a money amount, bad if it's large or mutable. A record gives value-based equality, immutability with `init` and `with` expressions, so it's ideal for DTOs, messages and value objects; I wouldn't use records for EF entities because entities have identity and change over time.

**Q7. How would you find a memory leak in a .NET service?**
> First confirm it with `dotnet-counters`: GC heap size and gen 2 size keep growing even after full collections. Then take two `dotnet-gcdump` snapshots some minutes apart and compare which types grow, and follow the retention path to the root — typically a static collection, an unbounded cache, an event handler that was never unsubscribed, or a DbContext captured by a singleton whose change tracker keeps growing. The fix is to remove the reference or bound it, for example an `IMemoryCache` with size limits and expiry.

**Q8. `throw` vs `throw ex`?**
> `throw;` rethrows the same exception and keeps the original stack trace; `throw ex;` resets the stack trace to the current line, so you lose where the error really happened. If I need to add context, I wrap it in a new exception with the original as the inner exception.

### A3.14 Tự kiểm tra
1. `decimal Total` là field của class `Order` thì nằm ở đâu? Biến `int i` bị lambda capture nằm ở đâu?
2. LOH là gì, vì sao dễ phân mảnh, ví dụ code nào tạo ra object LOH?
3. Quên `Dispose` `SqlConnection` thì hậu quả cụ thể là gì, sau bao lâu lỗi?
4. Vì sao repository trả `IEnumerable` làm query chậm? Cách phát hiện?
5. `Math.Round(2.345m, 2)` ra bao nhiêu? Vì sao?

---

## A4. Async/await, thread pool và đồng bộ trong process

**Vì sao cần.** Đây là chỗ interviewer .NET hay chờ nghe trong câu "request 8 s": **thread pool starvation**. Ở Agapi bạn chưa nhắc tới. Phần này đã học ở Buổi 1 (`notes/01`), ở đây gom lại thành một mạch để nói trôi chảy và trả lời được câu đào sâu.

### A4.1 `await` thực sự làm gì
```csharp
public async Task<QuoteDto> GetQuoteAsync(int id, CancellationToken ct)
{
    var quote = await _db.Quotes.AsNoTracking()
        .Where(q => q.Id == id).Select(...).SingleAsync(ct);   // (1)
    var tax = await _taxClient.GetRateAsync(quote.Zip, ct);     // (2)
    return quote with { TaxRate = tax };
}
```
- Compiler biến method `async` thành một **state machine** (struct có `MoveNext()`, trường `state`, các biến cục bộ thành field).
- Method chạy **đồng bộ** cho tới `await` đầu tiên **chưa xong**. Tại (1): EF gửi câu SQL qua socket, nhận về một `Task` chưa hoàn thành → `await` **đăng ký continuation** ("khi Task xong thì gọi `MoveNext()` tiếp từ state 1") rồi **return** → thread **quay về thread pool** phục vụ request khác.
- Trong lúc SQL Server chạy query, **không có thread nào bị chiếm** cho request này. OS theo dõi socket qua **IOCP/epoll** (A1.4). Khi dữ liệu về, một thread pool thread bất kỳ chạy tiếp từ sau (1). Có thể là **thread khác** với thread ban đầu.
- `await` **không tạo thread**. `Task.Run` mới **mượn** một thread pool thread để chạy code CPU.

Con số để nói: server 100 thread, mỗi request chờ DB 200 ms. **Sync**: mỗi request giữ 1 thread 200 ms → tối đa ~500 req/s. **Async**: thread chỉ bận vài ms để chạy code → hàng chục nghìn req/s, giới hạn chuyển sang DB/connection pool. **Latency từng request vẫn ~205 ms**: async tăng **throughput**, không giảm latency.

### A4.2 Task không phải Thread
- **Thread**: luồng thật của OS (stack ~1 MB, context switch).
- **Task**: object đại diện cho **một việc sẽ có kết quả** (promise/future). Task I/O không có thread nào "chạy" nó trong lúc chờ.
- **Async ≠ concurrency ≠ parallelism**: async = không chặn khi chờ; concurrency = nhiều việc cùng tiến triển (xen kẽ); parallelism = chạy **cùng lúc** trên nhiều core (`Parallel.ForEach`, PLINQ) — cho CPU-bound.

### A4.3 Thread pool hoạt động thế nào
- .NET có **một thread pool chung** cho process: chạy continuation sau `await`, `Task.Run`, timer, và các request ASP.NET Core.
- Số thread tối thiểu mặc định = **số core**. Khi mọi thread bận, pool **thêm thread từ từ** (thuật toán hill-climbing + phát hiện starvation), cỡ **1–2 thread mỗi giây**, để tránh tạo quá nhiều thread khi chỉ là tải nhất thời.
- Công việc chờ thread nằm trong **hàng đợi của pool (ThreadPool queue)**.

### A4.4 Thread pool starvation — cơ chế, triệu chứng, xác nhận, xử lý
**Nguyên nhân phổ biến nhất: sync-over-async** (`.Result`, `.Wait()`, `GetAwaiter().GetResult()`), hoặc gọi API đồng bộ chặn lâu (`Thread.Sleep`, `File.ReadAllText`, `HttpClient.Send`, EF `ToList()` thay vì `ToListAsync()`).

Cơ chế với `.Result`:
1. Thread A gọi `_client.GetAsync(url).Result` → **thread A ngủ** chờ Task.
2. Khi HTTP xong, continuation để "hoàn thành Task" cần **một thread khác** (thread B) từ pool.
3. Tải cao: 200 request cùng làm vậy → 200 thread ngủ trong `.Result`, continuation của chúng **xếp hàng** chờ thread rảnh, nhưng không ai rảnh → pool thêm 1–2 thread/giây → **mọi request chậm dần**, có thể hàng chục giây. **Một thao tác chiếm 2 thread.**

Triệu chứng nhận ra:
- Latency tăng vọt (p50 cũng tăng), **CPU thấp**, DB bình thường, error timeout tăng.
- **Thread count** tăng chậm, đều đặn.
- Thường xảy ra lúc **tải tăng đột ngột** (sáng thứ Hai, sau deploy restart, khi một dependency chậm đi).

Xác nhận bằng công cụ:
- `dotnet-counters monitor -p <pid> System.Runtime` → **ThreadPool Queue Length** tăng cao, **ThreadPool Thread Count** tăng chậm.
- `dotnet-stack report -p <pid>` hoặc `dotnet-dump collect` rồi `analyze` → `clrstack -all`: hàng trăm stack đứng ở `Task.Wait` / `.Result` / `Monitor.Wait`.
- APM (Application Insights): dependency (SQL/HTTP) nhanh nhưng request chậm → thời gian nằm **trước** khi code chạy.

Xử lý:
- **Tạm thời**: `ThreadPool.SetMinThreads(200, 200)` (pool tạo ngay thread tới mức này) hoặc scale out thêm instance → giảm đau, không chữa.
- **Tận gốc**: **async all the way** (không `.Result` trong code request), timeout + `CancellationToken` cho mọi I/O, tìm thư viện cũ chỉ có API sync (bọc lại hoặc thay).
- Phòng ngừa: analyzer (`VSTHRD002`, `CA2012`), code review, load test.

### A4.5 SynchronizationContext và deadlock kiểu cũ
- **SynchronizationContext** quyết định continuation chạy **ở đâu**. WinForms/WPF: phải quay về **UI thread**. ASP.NET (Framework cũ): quay về context của request (một thread mỗi lúc).
- Deadlock kinh điển (ASP.NET cũ/WPF): thread UI gọi `.Result` → ngủ; continuation cần **chính thread UI** để chạy → không bao giờ chạy → **deadlock vĩnh viễn**.
- **ASP.NET Core không có SynchronizationContext** → `.Result` không deadlock nhưng gây **starvation**. `ConfigureAwait(false)` vì vậy chủ yếu quan trọng trong **thư viện** (có thể bị gọi từ app có context).
- Codebase partner có thể còn ASP.NET MVC 5 (.NET Framework) → `.Result` ở đó **deadlock thật**.

### A4.6 Những lỗi async khác hay bị hỏi
| Lỗi | Hậu quả | Đúng |
|---|---|---|
| **Quên `await`** (fire-and-forget) | Exception bị nuốt (client vẫn nhận 200); DbContext/HttpContext đã dispose khi task chạy; "A second operation was started on this context"; mất việc khi app tắt | Việc nền → `Channel<T>` + `BackgroundService` (scope riêng) hoặc queue/outbox |
| **`async void`** | Exception thoát ra → ném lại trên thread pool → **crash process** | Chỉ cho event handler; còn lại `async Task` |
| `async` method gọi API sync bên trong | Vẫn chặn thread | `ToListAsync`, `ReadAsStringAsync`… |
| Bọc `Task.Run` quanh code request trong ASP.NET Core | Chỉ chuyển từ thread này sang thread khác, thêm overhead | Không làm; chỉ `Task.Run` cho CPU-bound ở app UI |
| `Task.WhenAll` dùng **chung một DbContext** | Ném "second operation" (DbContext không thread-safe, 1 connection = 1 lệnh/lúc) | Mỗi task một context (`IDbContextFactory`), cân nhắc ×N connection |
| Không truyền `CancellationToken` | Client huỷ/timeout mà server vẫn chạy query tốn tài nguyên | Truyền `HttpContext.RequestAborted` (tham số `CancellationToken ct` của action) xuống tới EF/HttpClient |
| `lock` quanh `await` | **Lỗi compile** (CS1996) | `SemaphoreSlim.WaitAsync()` |

### A4.7 Đồng bộ trong một process (khi nhiều thread chạm cùng dữ liệu)
| Công cụ | Dùng khi | Lưu ý |
|---|---|---|
| `lock` (`Monitor`) | Đoạn code ngắn, đồng bộ, trong 1 process | Không await bên trong; chỉ bảo vệ **trong một instance** |
| `SemaphoreSlim(1,1)` + `WaitAsync` | Cần khoá quanh code async | Luôn `Release()` trong `finally` |
| `SemaphoreSlim(n)` | Giới hạn số việc đồng thời (bulkhead): tối đa 10 lời gọi tới provider | |
| `Interlocked.Increment` | Bộ đếm đơn giản | Nguyên tử ở mức CPU, không khoá |
| `ConcurrentDictionary`, `Channel<T>` | Cấu trúc dữ liệu dùng chung | Channel = hàng đợi producer/consumer async có giới hạn (bounded) |
| `ReaderWriterLockSlim` | Đọc rất nhiều, ghi hiếm | Phức tạp, ít khi cần |

**Quan trọng nhất cho phỏng vấn:** `lock` trong C# **vô dụng khi chạy nhiều instance** (2 pod, mỗi pod một `lock` riêng). Dữ liệu dùng chung giữa instance phải do **database** (atomic UPDATE, UNIQUE, rowversion — A6) hoặc **distributed lock** (Redis — C4) quyết định.

### A4.8 Một số API nâng cao
- **`ValueTask<T>`**: tránh cấp phát Task khi kết quả thường có sẵn (cache hit). Chỉ được await **một lần**.
- **`IAsyncEnumerable<T>` + `await foreach`**: stream dữ liệu lớn (EF `AsAsyncEnumerable()`), giữ connection suốt vòng lặp.
- **`Parallel.ForEachAsync(items, new ParallelOptions { MaxDegreeOfParallelism = 8 }, ...)`**: chạy nhiều việc I/O song song **có giới hạn** (đừng `Task.WhenAll` 10.000 lời gọi cùng lúc → đánh sập provider và cạn connection).
- **`TimeProvider`** (.NET 8): thay `DateTime.UtcNow` để test được; `Task.Delay(time, provider)`.

### A4.9 Bẫy hay sai
- "Thread pool tạo quá nhiều thread nên chậm" → sai; vấn đề là pool **tạo thread quá chậm** so với số thread bị chặn.
- "`await` tạo thread mới" → sai.
- "Async làm query nhanh hơn" → sai; chỉ không giữ thread.
- "`ConfigureAwait(false)` sửa được starvation" → không; nó chỉ quyết định continuation chạy ở context nào.
- "Dùng `lock` để chống double spin" → chỉ đúng với 1 instance.

### A4.10 Câu hỏi phỏng vấn & trả lời mẫu

**Q1. What happens to the thread when you await a database call?**
> Nothing is blocked. The method runs synchronously until the first await on an incomplete task; EF sends the query, the await registers a continuation and returns, and the thread goes back to the pool to serve other requests. While SQL Server works, no thread is held for this request — the OS tracks the socket through IOCP or epoll. When the result arrives, any free pool thread resumes the method. That's why async improves throughput, not the latency of a single request.

**Q2. What is thread-pool starvation and how would you confirm it?**
> It's when all pool threads are blocked, so queued work — including the continuations that would unblock them — can't run, and the pool only adds about one or two threads a second. The typical cause is sync-over-async like `.Result` on the request path: each call holds one sleeping thread and needs a second thread to complete. Symptoms are latency climbing for every endpoint while CPU stays low and the database looks healthy. I'd confirm with `dotnet-counters` — thread-pool queue length rising and thread count creeping up — and a `dotnet-stack` or dump showing hundreds of threads in `Task.Wait`. Short term, raise min threads or scale out; the real fix is async all the way with timeouts and cancellation.

**Q3. Why is `.Result` dangerous? Does it deadlock in ASP.NET Core?**
> In classic ASP.NET or WPF it can deadlock: the blocked thread is the one the continuation needs because of the synchronisation context. ASP.NET Core has no synchronisation context, so it doesn't deadlock, but it blocks a pool thread and needs another one to finish, so under load it causes thread-pool starvation. Either way, I avoid it on request paths.

**Q4. You need to call three independent services. How?**
> Start all three and `await Task.WhenAll`, so the latency is the slowest call instead of the sum — for example 80 + 60 + 50 ms becomes about 80 ms. Two cautions: if they're EF queries, each needs its own DbContext because a context can't run two commands at once, and parallelism multiplies connection usage per request, so on a hot endpoint I'd measure before doing it. For many items I'd use `Parallel.ForEachAsync` with a max degree of parallelism instead of firing thousands of calls at once.

**Q5. What happens if you forget to await a task, or use async void?**
> A forgotten await means exceptions are lost — the client gets a 200 even though the work failed — and the task may run after the request scope is disposed, so DbContext calls fail or race. `async void` is worse: an unhandled exception is rethrown on the thread pool and crashes the process. For real background work I'd put it on a `Channel` consumed by a `BackgroundService` with its own scope, or a durable queue if it must survive restarts.

**Q6. How do you protect shared state across threads? Across instances?**
> Inside one process: `lock` for short synchronous sections, `SemaphoreSlim` when there's an await inside, `Interlocked` for counters, or concurrent collections. Across instances none of that works, because each instance has its own lock. Then the database must be the arbiter — an atomic conditional update, a unique constraint or a row version — and only if there's no single row to protect would I use a distributed lock in Redis, with its caveats.

### A4.11 Tự kiểm tra
1. Vì sao `.Result` chiếm **2** thread? Vẽ lại timeline.
2. Ba dấu hiệu nhận ra starvation, hai công cụ xác nhận, một cách chữa tạm, một cách chữa gốc.
3. `Task.WhenAll` với chung DbContext lỗi gì? Vì sao?
4. `lock` C# có chống được double spin khi chạy 3 pod không? Dùng gì thay?
5. ASP.NET Core có cần `ConfigureAwait(false)` không? Vì sao?

---

## A5. SQL Server bên trong: lưu trữ, index, execution plan, JOIN

**Vì sao cần.** Ở Agapi, khi bạn nói "DB có vấn đề", interviewer đào: *cụ thể là gì? JOIN nhiều bảng có chậm không? index theo gì? làm sao biết index đúng?* Bạn trả lời "join nhiều bảng chậm, cần split query" và "chưa shard" — cả hai bị bác. Để trả lời đúng phải hiểu **DB lưu dữ liệu thế nào** và **DB quyết định chạy query ra sao**. Phần này đi từ trang dữ liệu 8 KB tới cách đọc execution plan.

### A5.1 Dữ liệu nằm trên đĩa thế nào
- SQL Server lưu dữ liệu theo **page (trang) 8 KB**; 8 page liền nhau = 1 **extent** (64 KB). Mọi đọc/ghi đều theo đơn vị page.
- Page được nạp vào **buffer pool** (RAM). Đọc page đã có trong RAM = **logical read**; phải lấy từ đĩa = **physical read** (chậm hơn hàng trăm lần). Restart server → buffer pool trống → query đầu chậm ("cold cache").
- Mọi thay đổi ghi vào **transaction log** (ghi tuần tự) **trước** khi page dữ liệu được ghi xuống đĩa → **write-ahead logging (WAL)**, đảm bảo khôi phục được khi crash (xem A6).
- Con số: bảng `Orders` 10 triệu dòng × ~200 byte/dòng ≈ 2 GB ≈ **250.000 page**. Scan cả bảng = đọc 250.000 page. Seek một dòng qua index = đọc **3–4 page**.

### A5.2 Clustered index, heap, nonclustered index
- **Clustered index** = **chính bảng**, dữ liệu được xếp theo **clustered key** (thường là PK) trong một cây **B-tree** (B+ tree): tầng gốc (root) → tầng trung gian → **tầng lá (leaf) chứa toàn bộ dòng**. Mỗi bảng tối đa 1 clustered index. 10 triệu dòng chỉ cần cây ~3–4 tầng → tìm theo Id = 3–4 page đọc.
- **Heap** = bảng không có clustered index, dòng nằm lộn xộn; tìm qua RID (file:page:slot). Ít dùng cho bảng nghiệp vụ.
- **Nonclustered index** = một **cây B-tree riêng**, như **mục lục cuối sách**: lá chứa **cột key của index + clustered key** (để quay về bảng). Một bảng có thể có nhiều nonclustered index.
- Ví dụ đời thường: clustered = **danh bạ xếp theo họ tên** (bản thân danh bạ là dữ liệu); nonclustered trên `Phone` = **một sổ riêng xếp theo số điện thoại**, mỗi dòng ghi "số này → xem tên Nguyễn Văn A trong danh bạ".

Chọn clustered key: **hẹp, tăng dần, không đổi, duy nhất** (`int/bigint IDENTITY`). `Guid` ngẫu nhiên (`NEWID()`) làm clustered key → chèn vào giữa cây → **page split** (tách trang) liên tục, phân mảnh, ghi chậm → dùng `NEWSEQUENTIALID()` hoặc Guid v7 / giữ `bigint` làm clustered, Guid làm cột public.

### A5.3 Seek, Scan, Key Lookup — ba thao tác cần nhận ra trong plan
| Thao tác | Nghĩa | Chi phí tỉ lệ với |
|---|---|---|
| **Index Seek** | Đi từ gốc cây thẳng tới khoảng cần tìm | Số dòng trả về (+ 3–4 page để đi xuống cây) |
| **Index/Table Scan** | Đọc **toàn bộ** lá của index/bảng | **Số page của cả bảng** |
| **Key Lookup** | Tìm được dòng trong nonclustered index nhưng **thiếu cột** cần SELECT → quay lại clustered index lấy từng dòng | **Mỗi dòng một lần seek**, đọc ngẫu nhiên |

- Seek trả 20 dòng + 20 key lookup → rất nhanh. Seek trả **200.000 dòng** + 200.000 key lookup → chậm hơn cả scan → optimizer có thể **chọn scan** (đúng đắn). "Scan" không phải lúc nào cũng xấu; xấu là **scan bảng lớn để lấy vài dòng**.
- **Covering index** ("độ bao phủ" mà interviewer Agapi nhắc tới) = index chứa **đủ mọi cột** query cần (cột tìm trong key, cột hiển thị trong `INCLUDE`) → **không cần key lookup**.

```sql
-- Query màn hình "đơn của đại lý trong tháng"
SELECT Id, CustomerName, Total, Status
FROM Orders
WHERE StoreId = @storeId AND CreatedAt >= @from
ORDER BY CreatedAt DESC;

-- Index phủ (covering): key để tìm + sắp xếp, INCLUDE để hiển thị
CREATE INDEX IX_Orders_Store_CreatedAt
ON Orders (StoreId, CreatedAt DESC)
INCLUDE (CustomerName, Total, Status);
```

### A5.4 Composite index: thứ tự cột quyết định tất cả
Index `(StoreId, CreatedAt)` giống danh bạ xếp theo **(Họ, Tên)**:
| Điều kiện | Seek được? | Vì sao |
|---|---|---|
| `StoreId = 5` | ✅ | Cột đầu |
| `StoreId = 5 AND CreatedAt >= '2026-10-01'` | ✅ | Đi tới StoreId 5 rồi tới khoảng ngày |
| `StoreId = 5 ORDER BY CreatedAt DESC` + `TOP 20` | ✅ không cần Sort | Dữ liệu đã xếp sẵn, đọc 20 dòng là dừng |
| `CreatedAt >= '2026-10-01'` (không có StoreId) | ❌ scan | Như tìm theo **tên** trong danh bạ xếp theo **họ** |
| `StoreId IN (1,2,3) AND CreatedAt >= …` | ✅ (3 lần seek) | |
- Quy tắc sắp cột: **Equality → Sort → Range (E-S-R)**: cột so sánh bằng trước, cột sắp xếp, rồi cột khoảng. Range ở cột trước thì các cột sau chỉ còn dùng để lọc lại, không seek được.
- Index `(A)` thừa nếu đã có `(A, B)`. Mỗi index thêm **làm chậm INSERT/UPDATE/DELETE** (phải cập nhật cây đó, trong cùng transaction) và tốn dung lượng → đừng tạo index cho mọi cột.
- Index luôn được cập nhật **đồng bộ** với dữ liệu → không bao giờ "cũ". Cái có thể cũ là **statistics** (A5.6).

### A5.5 Index cho FK — điểm bạn bị thiếu ở Agapi
- **SQL Server (và PostgreSQL) không tự tạo index cho cột foreign key.** PK có index (clustered), nhưng `Orders.CustomerId` (FK → Customers) **không có** trừ khi bạn tạo. EF Core migration **tự tạo** index cho FK; DB tạo tay hoặc legacy (Dapper + stored procedure như PlaySweeps, code partner) hay thiếu.
- Thiếu index trên FK gây ba chuyện:
  1. **JOIN chậm**: `Customers JOIN Orders ON o.CustomerId = c.Id` → mỗi lần phải scan `Orders`.
  2. **Lọc theo cha chậm**: "tất cả order của customer 42" → scan 10 triệu dòng.
  3. **DELETE/UPDATE bảng cha chậm và khoá rộng**: xoá 1 customer → SQL Server phải kiểm tra không còn order nào trỏ tới → **scan bảng con** + giữ lock lâu → block người khác.
- Khi tiếp quản DB: chạy query tìm FK không có index (so `sys.foreign_key_columns` với `sys.index_columns`) — một trong các việc đầu tiên.

### A5.6 Query optimizer, statistics, cardinality estimation
- SQL là ngôn ngữ **khai báo (declarative)**: bạn mô tả **kết quả**, **query optimizer** chọn **cách chạy** (plan): dùng index nào, JOIN theo thứ tự nào, thuật toán JOIN nào. Thứ tự bạn viết `JOIN ... WHERE` **không** phải thứ tự chạy; optimizer gần như luôn **lọc WHERE trước** rồi mới JOIN.
- Optimizer chọn plan dựa trên **ước lượng số dòng (cardinality estimation)**, lấy từ **statistics** (histogram tối đa 200 bậc phân bố giá trị của cột/index).
- **Statistics cũ** (tự cập nhật khi thay đổi vượt ngưỡng, với bảng lớn có thể lâu mới cập nhật) → ước lượng 10 dòng nhưng thật 1 triệu → chọn plan tệ (nested loops cho 1 triệu dòng, cấp RAM sort quá ít → **spill xuống tempdb**). Dấu hiệu trong actual plan: **Estimated Rows ≪ Actual Rows**. Sửa: `UPDATE STATISTICS Orders WITH FULLSCAN`.
- **Parameter sniffing**: stored procedure/query tham số hoá được **compile một lần với giá trị tham số đầu tiên**, plan được cache và **dùng lại cho mọi giá trị**. Lần đầu chạy với đại lý nhỏ (50 đơn) → plan seek + nested loops; sau đó đại lý lớn (80.000 đơn) dùng lại plan đó → rất chậm. Triệu chứng: **lúc nhanh lúc chậm**, restart hoặc rebuild index thì tự khỏi (plan bị xoá), chạy trong SSMS với giá trị literal thì nhanh. Sửa: index tốt hơn để plan nào cũng ổn, `OPTION (RECOMPILE)` cho query chạy không thường xuyên, `OPTIMIZE FOR UNKNOWN`, hoặc Query Store **force plan**.

### A5.7 Thuật toán JOIN — để trả lời "JOIN có chậm không"
| Thuật toán | Cách chạy | Tốt khi |
|---|---|---|
| **Nested Loops** | Với mỗi dòng bảng ngoài, seek bảng trong | Bảng ngoài ít dòng + bảng trong có index trên cột JOIN |
| **Merge Join** | Hai đầu vào **đã sắp xếp** theo cột JOIN, đi song song như khoá kéo | Cả hai đã có index theo cột JOIN |
| **Hash Join** | Dựng bảng băm từ đầu vào nhỏ, dò bằng đầu vào lớn | Hai tập lớn, không có index phù hợp; tốn RAM (memory grant), có thể spill |

**JOIN tự nó không chậm.** Join 5–6 bảng có index đúng chạy trong vài ms. JOIN chậm khi:
1. **Cột JOIN không có index** (thường là FK) → scan hoặc hash join trên bảng lớn.
2. **JOIN làm nhân số dòng (row multiplication)**: join cùng lúc **hai bảng con ngang hàng** của một bảng cha. 1 user có 100 Transactions và 50 LoginHistories → JOIN cả hai = 100 × 50 = **5.000 dòng** thay vì 150. Chậm (DB sinh nhiều dòng, network chở nhiều, app phải gộp lại) và **sai kết quả** nếu `SUM(t.Amount)` (mỗi giao dịch bị cộng 50 lần). Sửa: tách query (EF Core `AsSplitQuery()`), hoặc aggregate từng bảng con trong subquery rồi mới JOIN.
3. **Điều kiện JOIN/WHERE không "sargable"** (xem A5.8) → không dùng được index.
4. **Statistics sai** khiến chọn thuật toán sai.
5. Join rất nhiều bảng (10+) → optimizer không thử hết thứ tự, có thể chọn plan chưa tốt.

JOIN dạng chuỗi (Order → OrderLine → Product) **không** nhân dòng, vì mỗi dòng con chỉ nối với một dòng cha.

### A5.8 Sargable — viết điều kiện để index dùng được
**SARGable** (Search ARGument-able) = điều kiện cho phép seek. Không sargable thì dù có index vẫn scan:
| Không sargable | Sửa thành |
|---|---|
| `WHERE YEAR(CreatedAt) = 2026` | `WHERE CreatedAt >= '2026-01-01' AND CreatedAt < '2027-01-01'` |
| `WHERE CAST(Phone AS int) = @p` / bọc hàm lên cột | So sánh trực tiếp cột với tham số cùng kiểu |
| `WHERE Email LIKE '%@gmail.com'` (wildcard đầu) | Lưu cột domain riêng / full-text |
| Cột `varchar` so với tham số `nvarchar` (Dapper truyền `string` mặc định là `nvarchar`) → **`CONVERT_IMPLICIT`** trên cột | Truyền đúng kiểu: Dapper `new DbString { IsAnsi = true }` hoặc `DbType.AnsiString` |
| `WHERE a.X = @x OR b.Y = @y` trải trên nhiều bảng | Tách `UNION ALL` hai nhánh |
| `ISNULL(Col, 0) = 0` | `Col = 0 OR Col IS NULL` |

### A5.9 Công cụ: làm sao **biết** index đúng hay chưa
Đây là câu bạn chưa trả lời được ở Agapi. Thứ tự dùng:
1. **Query Store** (SQL Server 2016+, Azure SQL bật sẵn): top query theo **tổng duration / CPU / logical reads**, lịch sử plan, phát hiện query **đổi plan** (regression), force plan tốt.
2. **Actual Execution Plan** (SSMS: Ctrl+M, hoặc `SET STATISTICS XML ON`): tìm
   - **Table/Index Scan** trên bảng lớn trả ít dòng → thiếu index / không sargable.
   - **Key Lookup** với số lần thực thi lớn → thêm cột vào `INCLUDE` (covering).
   - **Estimated vs Actual rows** lệch nhiều → statistics / parameter sniffing.
   - **Sort**, **Hash Match** tốn nhiều, cảnh báo **spill to tempdb**, cảnh báo **CONVERT_IMPLICIT**, **Missing Index** (gợi ý màu xanh).
3. **`SET STATISTICS IO, TIME ON`**: số **logical reads** từng bảng. Đây là thước đo khách quan: thêm index, logical reads từ 250.000 xuống 12 = chứng minh.
4. **Missing index DMV**: `sys.dm_db_missing_index_details`, `..._group_stats` (gợi ý index + mức cải thiện ước tính). Chỉ là **gợi ý**: hay đề xuất trùng lặp, nhiều cột INCLUDE; phải gộp và cân nhắc chi phí ghi.
5. **Index usage**: `sys.dm_db_index_usage_stats` → index có `user_updates` cao nhưng `user_seeks + scans` ≈ 0 = **index thừa** (chỉ làm chậm ghi) → cân nhắc xoá.
6. **Đang chạy / bị block**: `sys.dm_exec_requests` (cột `blocking_session_id`, `wait_type`), `sp_WhoIsActive` (script cộng đồng phổ biến). Wait type hay gặp: `LCK_M_X`/`LCK_M_U` (chờ lock), `PAGEIOLATCH_SH` (chờ đọc đĩa), `CXPACKET` (song song), `RESOURCE_SEMAPHORE` (chờ RAM cho sort/hash), `ASYNC_NETWORK_IO` (**app đọc kết quả chậm** — thường do app lấy quá nhiều dòng hoặc xử lý từng dòng).
7. **Sau khi sửa**: so sánh lại logical reads, duration p95 trên Query Store/APM.

### A5.10 Thang xử lý "DB chậm" — vì sao "chưa shard" là câu trả lời sai lúc đầu
Sharding (chia dữ liệu ra nhiều DB) là **bước cuối cùng**, đắt và phức tạp (query xuyên shard, transaction phân tán, rebalance). Một request 8 s gần như không bao giờ do "chưa shard". Thang đúng, từ rẻ tới đắt:
1. Sửa **query** (sargable, bớt cột `SELECT *`, phân trang, tránh N+1).
2. Thêm/sửa **index** (FK, composite đúng thứ tự, covering).
3. Sửa **statistics / plan** (update stats, xử lý parameter sniffing).
4. Giảm **blocking** (transaction ngắn, RCSI — A6).
5. **Cache** dữ liệu đọc nhiều ít đổi (C4).
6. **Read replica** cho báo cáo, tách OLTP và báo cáo.
7. **Scale up** DB (CPU/RAM/IOPS).
8. **Partitioning** (bảng rất lớn, lọc theo cột partition), **archive** dữ liệu cũ.
9. **Sharding** (multi-tenant: tenant lớn sang shard riêng — Joblogic có shard theo tenant).

### A5.11 Bẫy hay sai
- "JOIN nhiều bảng làm chậm" → nói: "JOIN tự nó không chậm; chậm khi thiếu index trên cột JOIN (FK), khi JOIN nhân dòng, hoặc điều kiện không sargable."
- "Đánh index theo WHERE là đủ" → còn **cột JOIN (FK)**, **cột ORDER BY**, thứ tự cột, INCLUDE; và phải **đo** bằng plan + logical reads.
- "Index càng nhiều càng tốt" → mỗi index làm ghi chậm và tốn chỗ.
- "Scan luôn xấu" → scan đúng khi lấy phần lớn bảng.
- "Shard để tăng tốc query" → bước cuối.
- Không biết `ASYNC_NETWORK_IO` nghĩa là **app** chậm đọc, không phải DB chậm.

### A5.12 Câu hỏi phỏng vấn & trả lời mẫu

**Q1. (Agapi) You said the database might be the problem. What specifically would you look for?**
> I'd separate "the query is slow" from "the query is waiting". For slow queries I'd open the actual execution plan and look for scans on large tables that return few rows, key lookups executed thousands of times, a big gap between estimated and actual rows, implicit conversions, sorts or hash joins spilling to tempdb. For waiting, I'd check `sys.dm_exec_requests` for blocking sessions and wait types — lock waits mean another transaction holds the rows, `PAGEIOLATCH` means disk reads, `ASYNC_NETWORK_IO` means the application is slow to consume results. Query Store tells me which queries cost the most overall and whether a plan recently changed.

**Q2. (Agapi) Does joining many tables make a query slow?**
> Not by itself. With indexes on the join columns, joining five or six tables runs in milliseconds, because the optimizer filters first and then seeks into each table. Joins become slow for specific reasons: the join column — usually a foreign key — has no index, so each join scans; the join multiplies rows, for example joining two child collections of the same parent, which also inflates SUMs; the predicate isn't sargable, like a function on the column or a type mismatch; or the statistics are stale so the optimizer picks the wrong join algorithm. So I'd look at the plan rather than reduce the number of joins.

**Q3. (Agapi) How do you decide what to index, and how do you know an index is right?**
> I index what the query uses to find and order rows: equality columns first, then the sort column, then range columns, and I include the displayed columns so the index covers the query and avoids key lookups. Foreign keys need their own index, because SQL Server doesn't create one automatically and missing ones slow joins and cascading deletes. To know it's right, I measure: logical reads with `SET STATISTICS IO` before and after, the actual plan showing a seek instead of a scan, and Query Store duration. I also check `sys.dm_db_index_usage_stats` for indexes that are written a lot but never read, since every index slows down writes.

**Q4. Clustered vs nonclustered index?**
> The clustered index is the table itself, stored as a B-tree ordered by the clustered key, with the full rows in the leaf level — so there's only one. A nonclustered index is a separate B-tree with the index key plus the clustered key as a pointer back to the row, like the index at the back of a book. If a nonclustered index doesn't contain every column the query needs, SQL Server does a key lookup per row, which is why covering indexes with INCLUDE matter. I prefer a narrow, increasing clustered key like a bigint identity; a random GUID causes page splits and fragmentation.

**Q5. What is parameter sniffing?**
> SQL Server compiles a parameterised query using the parameter values of the first execution and caches that plan for every later value. If the first call was for a store with fifty orders, the cached plan may be a seek with nested loops, which is terrible for a store with eighty thousand. The symptom is "sometimes fast, sometimes slow", and it fixes itself after a restart or index rebuild. I'd confirm by comparing compiled and runtime parameter values in the plan and multiple plans in Query Store, then fix it with a better index, `OPTION (RECOMPILE)` for infrequent queries, or by forcing a good plan.

**Q6. A query got 20 times slower overnight with no deployment. Why?**
> Most likely the plan changed. Statistics may have updated, or the plan was recompiled with unusual parameter values, or data volume crossed a threshold. I'd check Query Store for a plan change on that query, compare the old and new plans, and force the old one as an immediate fix, then address the root cause — a missing index or parameter sniffing. Other candidates: blocking from a new job, or a big data load leaving statistics stale.

**Q7. Why does a filter like `YEAR(CreatedAt) = 2026` not use the index?**
> Because the function is applied to the column, SQL Server can't seek on the index — it has to compute the function for every row. Rewriting it as a range, `CreatedAt >= '2026-01-01' AND CreatedAt < '2027-01-01'`, makes it sargable. The same happens with implicit conversions, for example Dapper sending an nvarchar parameter against a varchar column.

**Q8. When would you shard a database?**
> Only after cheaper options run out: query and index fixes, removing blocking, caching, read replicas for reporting, scaling up, partitioning or archiving. Sharding adds cross-shard queries, distributed transactions and rebalancing. In multi-tenant SaaS it makes sense to move very large tenants to their own shard, which Joblogic did with a shard key per tenant — but it's not how you fix a single slow request.

### A5.13 Tự kiểm tra
1. Seek trả 200.000 dòng kèm key lookup, vì sao optimizer có thể chọn scan?
2. Viết index cho: `WHERE TenantId=@t AND Status='Open' ORDER BY DueDate` hiển thị `Id, Title, DueDate`.
3. Ba hậu quả của thiếu index trên FK.
4. Năm thứ cần tìm trong actual execution plan.
5. Wait type `ASYNC_NETWORK_IO` nghĩa là gì? `LCK_M_U`?
6. Vì sao JOIN Transactions và LoginHistories cùng lúc làm `SUM` sai?

---

## A6. Transaction, isolation, lock, deadlock trong SQL Server

**Vì sao cần.** Câu Agapi số 3: *"update balance khi spin thế nào? có bao nhiêu cách lock trong SQL? thiếu rollback"*. Bạn làm tốt phần `UPDATE ... WHERE Balance >= @bet` nhưng hiểu sai `HOLDLOCK`, không kể được các loại lock, và không nói được xử lý lỗi/rollback (`XACT_ABORT`, retry deadlock). Ops Hub cũng toàn tiền và trạng thái (balance due, giữ chỗ xe giao hàng, inventory), nên đây là phần SA rất có thể đào.

### A6.1 ACID và cách DB đảm bảo
| Chữ | Nghĩa | Cơ chế trong SQL Server |
|---|---|---|
| **Atomicity** (nguyên tử) | Hoặc tất cả, hoặc không gì | Transaction log: rollback dùng log để hoàn tác |
| **Consistency** (nhất quán) | Dữ liệu luôn thoả ràng buộc | PK, FK, UNIQUE, CHECK, trigger |
| **Isolation** (cô lập) | Các transaction đồng thời không thấy "nửa chừng" của nhau (tuỳ mức) | **Lock** hoặc **row versioning** |
| **Durability** (bền vững) | Commit rồi thì không mất kể cả mất điện | **Write-ahead log**: commit = log đã ghi xuống đĩa |

- **Commit** chỉ cần ghi **log** (tuần tự, nhanh), page dữ liệu ghi sau (checkpoint). Crash → khi khởi động, SQL Server **redo** các transaction đã commit và **undo** các transaction dở.
- Mỗi câu lệnh đơn lẻ đã là một transaction (**autocommit**). Muốn nhiều câu lệnh cùng thành công/thất bại → `BEGIN TRAN ... COMMIT`.

### A6.2 Các loại lock (lock mode) — câu "có bao nhiêu cách lock"
**Theo chế độ (mode):**
| Mode | Ai lấy | Ý nghĩa |
|---|---|---|
| **S (Shared)** | `SELECT` (ở mức lock-based) | Nhiều người đọc cùng lúc được; chặn người ghi |
| **U (Update)** | `UPDATE`/`DELETE` khi đang **tìm** dòng; hoặc hint `UPDLOCK` | "Tôi đọc để sắp sửa". Tương thích với S, **không tương thích với U khác** → hai người cùng "đọc để sửa" phải xếp hàng → **chặn deadlock chuyển đổi** (S→X) |
| **X (Exclusive)** | Khi thực sự sửa dòng | Không ai đọc (kiểu lock) hay ghi được; **luôn giữ tới hết transaction** ở mọi isolation level |
| **IS / IX / SIX (Intent)** | Tự động ở cấp page/table | Báo "bên dưới có người đang giữ S/X" để người muốn khoá cả bảng biết ngay, không phải kiểm tra từng dòng |
| **Sch-S / Sch-M (Schema)** | Query / DDL (`ALTER TABLE`, tạo index offline) | Sch-M chặn mọi thứ → migration giờ cao điểm có thể đứng cả hệ thống |
| **Key-range (RangeS-S, RangeS-U, RangeI-N, RangeX-X)** | Mức **Serializable** / hint `HOLDLOCK` | Khoá **khoảng giá trị** trong index, kể cả **khoảng chưa có dòng** → chặn INSERT vào khoảng đó (chống **phantom**) |

Bảng tương thích cần nhớ: S–S ✅, S–U ✅, U–U ❌, S–X ❌, U–X ❌, X–X ❌.

**Theo phạm vi (granularity):** dòng (**KEY** trong index / **RID** trong heap) → **PAGE** → **OBJECT** (cả bảng). Khi một câu lệnh giữ quá ~**5.000 lock** trên một bảng, SQL Server **leo thang (lock escalation)** lên khoá **cả bảng** để tiết kiệm RAM → `UPDATE` 100.000 dòng một lần có thể khoá cả bảng `Orders` → mọi người khác đứng chờ. Sửa: chia lô (batch 1.000–4.000 dòng).

**Theo hint (cách bạn "xin" lock khác mặc định):**
| Hint | Tác dụng | Khi dùng |
|---|---|---|
| `UPDLOCK` | Lấy **U** thay vì S khi đọc, **giữ tới hết transaction** | Đọc rồi mới quyết định sửa (read-modify-write) |
| `HOLDLOCK` (= `SERIALIZABLE` cho bảng đó) | Giữ lock đọc tới hết transaction **và khoá khoảng (key-range)** | Khi dòng **có thể chưa tồn tại**: "kiểm tra chưa có thì INSERT" (upsert) |
| `UPDLOCK, HOLDLOCK` | Kết hợp: khoá để sửa + khoá cả khoảng | Mẫu upsert an toàn, giữ chỗ (xe, ngày) |
| `XLOCK` | Lấy X ngay khi đọc | Hiếm |
| `ROWLOCK` / `PAGLOCK` / `TABLOCK(X)` | Gợi ý phạm vi | `TABLOCK` cho bulk load |
| `NOLOCK` (= `READUNCOMMITTED`) | Đọc không lấy S lock, không tôn trọng X lock | **Không dùng cho tiền**: đọc dữ liệu chưa commit, có thể **đọc trùng hoặc sót dòng** khi page bị tách |
| `READPAST` | Bỏ qua các dòng đang bị khoá | Hàng đợi công việc trong bảng: nhiều worker lấy job khác nhau (`UPDLOCK, READPAST`) |
| `NOWAIT` / `SET LOCK_TIMEOUT 2000` | Không chờ / chờ tối đa 2 s rồi lỗi 1222 | Fail-fast thay vì treo |

**Sửa lại câu trả lời Agapi:** "`HOLDLOCK` để giữ lock tới khi transaction xong" là **chưa đúng ý chính**: `UPDLOCK` và X lock **đã giữ tới hết transaction** rồi. `HOLDLOCK` thêm **ngữ nghĩa Serializable**: giữ cả **S lock** tới cuối và **khoá khoảng** để không ai INSERT dòng mới khớp điều kiện.

### A6.3 Isolation level và các hiện tượng (anomaly)
**Hiện tượng:**
- **Dirty read**: đọc dữ liệu người khác **chưa commit** (họ rollback → bạn dùng số không tồn tại).
- **Non-repeatable read**: đọc lại cùng dòng trong một transaction thấy giá trị khác (người khác đã sửa + commit).
- **Phantom read**: chạy lại cùng `WHERE` thấy **thêm/mất dòng** (người khác INSERT/DELETE).
- **Lost update**: hai bên cùng đọc 100, cùng cộng 10 trong code, cùng ghi 110 → mất một lần cộng.
- **Write skew**: hai bên đọc cùng tập, mỗi bên sửa **dòng khác nhau** dựa trên điều kiện chung → vi phạm luật (ví dụ: luật "ít nhất 1 tài xế trực", hai tài xế cùng xin nghỉ, mỗi người thấy còn người kia).

| Mức | Dirty | Non-repeatable | Phantom | Cách SQL Server làm |
|---|---|---|---|---|
| Read Uncommitted | ✅ có thể | ✅ | ✅ | Không lấy S lock |
| **Read Committed** (mặc định) | ❌ | ✅ | ✅ | S lock **nhả ngay sau khi đọc xong dòng** |
| Repeatable Read | ❌ | ❌ | ✅ | S lock giữ tới cuối transaction |
| Serializable | ❌ | ❌ | ❌ | + key-range lock |
| **Snapshot** | ❌ | ❌ | ❌ | Đọc bản chụp lúc bắt đầu transaction (row versioning); ghi đụng nhau → lỗi **3960 update conflict** |
| **RCSI** (Read Committed Snapshot) | ❌ | ✅ | ✅ | Mỗi **câu lệnh** đọc bản đã commit mới nhất từ **version store (tempdb)**; **người đọc không chặn người ghi và ngược lại** |

- **Azure SQL Database bật RCSI mặc định**; SQL Server on-prem/RDS mặc định **tắt** → kiểm tra `SELECT is_read_committed_snapshot_on FROM sys.databases`. RCSI giảm rất nhiều blocking đọc–ghi, cái giá là tempdb lớn hơn, mỗi lần sửa thêm ~14 byte version info.
- **Không có mức nào tự chống lost update khi bạn đọc vào app rồi ghi lại** (trừ Serializable/Snapshot báo lỗi xung đột). Cách chống đúng ở A6.4.
- Đừng nâng cả transaction lên Serializable "cho chắc": khoá khoảng rộng, deadlock nhiều. **Khoá đúng dòng cần khoá.**

### A6.4 Bốn cách xử lý tranh chấp ghi (thứ tự ưu tiên)
Ví dụ thật: số dư (balance) khi spin; ở Ops Hub: giữ chỗ xe giao hàng, trừ inventory.

**1. Atomic conditional UPDATE (ưu tiên số 1)** — kiểm tra và sửa trong **một câu lệnh**:
```sql
UPDATE Wallets
SET Balance = Balance - @bet, Version = Version + 1
WHERE PlayerId = @playerId AND Balance >= @bet;
-- @@ROWCOUNT = 0 → không đủ tiền (hoặc không có ví)
```
Cơ chế: câu UPDATE tìm dòng bằng U lock → đổi sang X lock, sửa, **giữ X tới commit**. Request thứ hai cùng player **chờ** ở U lock; khi người đầu commit, nó **đọc giá trị đã commit mới nhất và đánh giá lại `WHERE`** → nếu không còn đủ tiền thì 0 dòng. **Không cần SELECT trước, không cần lock thủ công.** Đúng ở cả Read Committed lẫn RCSI (ghi luôn chặn ghi).

**2. Optimistic concurrency (khoá lạc quan)** — đọc không khoá, khi ghi kiểm tra phiên bản:
```sql
UPDATE Orders SET Status = @new, ...
WHERE Id = @id AND RowVersion = @originalRowVersion;   -- 0 dòng → người khác đã sửa
```
EF Core: `[Timestamp] byte[] RowVersion` → `DbUpdateConcurrencyException` → trả **409/412**, UI tải lại. Hợp khi **xung đột hiếm** và có **người dùng chờ giữa đọc và ghi** (form sửa đơn, kéo thả hàng đợi sản xuất).

**3. Pessimistic lock (khoá bi quan)** — khoá dòng khi đọc vì logic nhiều bước:
```sql
BEGIN TRAN;
SELECT Capacity, Booked FROM TruckDay WITH (UPDLOCK, HOLDLOCK)
WHERE TruckId = @t AND Date = @d;         -- người thứ hai chờ ở đây
-- kiểm tra luật phức tạp trong C# (tổng kích thước shed, cửa sổ giờ...)
INSERT INTO Deliveries (...) VALUES (...);
UPDATE TruckDay SET Booked = Booked + 1 WHERE TruckId = @t AND Date = @d;
COMMIT;
```
Hợp khi tranh chấp cao + logic không viết gọn được trong một câu UPDATE. **Transaction phải ngắn**: không gọi HTTP, không chờ người dùng bên trong.

**4. Distributed lock (Redis/RedLock)** — **cuối cùng**, khi không có một dòng DB chung để khoá (ví dụ Quest Engine state ở Cosmos DB). Không có fencing token thì không an toàn tuyệt đối (C4). DB vẫn phải có ràng buộc cuối (UNIQUE).

**Kèm theo luôn: UNIQUE constraint** cho thao tác "chỉ một lần" (idempotency key, `Orders.QuoteId`): `INSERT` và bắt lỗi **2627/2601** trong cùng transaction — không "SELECT xem có chưa rồi mới INSERT" (**check-then-act**, lỗi bạn hay lặp).

### A6.5 Thiết kế update balance khi spin — câu trả lời đầy đủ
Thực tế PlaySweeps (nói trung thực): Sweeps Coin do **Nexus** (service của PLAYSTUDIOS) sở hữu; backend gửi **delta + TransactionId (GUID)**; stored procedure của Nexus kiểm tra idempotency rồi kiểm tra số dư và cập nhật trong một transaction; bảng `PlayerBalances` bên mình là **bản sao (mirror)** ghi giá trị tuyệt đối; Redis lock theo (player, game) cho spin.

Nếu **mình tự làm ví**, thiết kế chuẩn:
```sql
CREATE PROCEDURE dbo.ApplyWager @PlayerId bigint, @TxId uniqueidentifier, @Amount decimal(18,2)
AS
BEGIN
  SET NOCOUNT ON;
  SET XACT_ABORT ON;                 -- lỗi bất kỳ hoặc client timeout → rollback toàn bộ
  BEGIN TRY
    BEGIN TRAN;
      -- 1) Idempotency: ghi sổ cái trước, UNIQUE(TxId) là trọng tài
      INSERT INTO WalletLedger (TxId, PlayerId, Amount, Type, CreatedAt)
      VALUES (@TxId, @PlayerId, -@Amount, 'Wager', SYSUTCDATETIME());

      -- 2) Atomic funds check + update
      UPDATE Wallets SET Balance = Balance - @Amount
      WHERE PlayerId = @PlayerId AND Balance >= @Amount;
      IF @@ROWCOUNT = 0 THROW 50001, 'Insufficient funds', 1;   -- → rollback cả INSERT ở trên
    COMMIT;
  END TRY
  BEGIN CATCH
    IF @@TRANCOUNT > 0 ROLLBACK;
    IF ERROR_NUMBER() IN (2627, 2601)          -- trùng TxId: request lặp lại
      BEGIN SELECT 'Duplicate' AS Result; RETURN; END   -- app trả lại kết quả lần đầu (replay)
    THROW;                                    -- lỗi khác (vd. 1205 deadlock) → app retry
  END CATCH
END
```
Điểm phải nói được:
- **Ledger chỉ ghi thêm (append-only)** + số dư là kết quả, giải thích được từng đồng; đối soát (reconciliation) `SUM(ledger) = Balance`.
- Idempotency key và atomic update **cùng transaction**; trùng → **replay** response cũ, không báo lỗi cho provider.
- Spin "pending" rồi "result": bet trừ tiền ngay (giữ tiền), result cộng thắng; refund tới trước bet → ghi tombstone (đã có trong `notes/01`).

### A6.6 "Thiếu rollback" — xử lý lỗi transaction đúng cách
Đây nhiều khả năng là ý interviewer Agapi nhắc:
- **`SET XACT_ABORT ON`**: với `OFF` (mặc định), nhiều lỗi runtime chỉ huỷ **câu lệnh lỗi**, transaction **vẫn mở**, các câu trước vẫn chờ commit → dữ liệu nửa vời. Nguy hiểm nhất: **client timeout** (ADO.NET `CommandTimeout` mặc định **30 s**) gửi tín hiệu *attention* → batch dừng nhưng **transaction vẫn mở và giữ lock** trên connection đó tới khi connection bị đóng/reset → các request khác bị block. `XACT_ABORT ON` → lỗi hoặc attention đều **rollback cả transaction** ngay.
- **TRY/CATCH + `IF @@TRANCOUNT > 0 ROLLBACK` + `THROW`** (không nuốt lỗi).
- Trong C#: `using var tx = conn.BeginTransaction();` … `tx.Commit();` — thoát khỏi `using` mà chưa Commit (exception) → **Dispose tự rollback**. EF Core: `SaveChanges` tự bọc transaction; nhiều bước thì `await using var tx = await db.Database.BeginTransactionAsync();`.
- **Retry cho lỗi tạm thời**: deadlock victim **1205**, lock timeout 1222, lỗi kết nối Azure SQL (40613, 40501…). Retry **cả transaction** (không chỉ câu lỗi), có backoff + jitter, giới hạn số lần, và chỉ an toàn khi transaction **idempotent** hoặc có idempotency key. EF Core: `EnableRetryOnFailure()` + bọc transaction thủ công trong `db.Database.CreateExecutionStrategy().ExecuteAsync(...)`.

### A6.7 Deadlock — ví dụ, phát hiện, sửa
Ví dụ chuyển tiền:
```
T1: UPDATE Wallets ... WHERE PlayerId = 1   (X trên dòng 1)
T2: UPDATE Wallets ... WHERE PlayerId = 2   (X trên dòng 2)
T1: UPDATE Wallets ... WHERE PlayerId = 2   → chờ T2
T2: UPDATE Wallets ... WHERE PlayerId = 1   → chờ T1  ⇒ vòng tròn
```
- SQL Server có **lock monitor** kiểm tra định kỳ (mặc định ~5 s, nhanh hơn khi đang có deadlock), chọn **victim** (transaction rẻ nhất để rollback, chỉnh bằng `SET DEADLOCK_PRIORITY`), trả lỗi **1205** cho victim; bên kia chạy tiếp.
- Xem lại: **Extended Events session `system_health`** lưu sẵn `xml_deadlock_report` (deadlock graph: ai giữ gì, chờ gì, câu SQL nào).
- Sửa:
  1. **Khoá theo thứ tự cố định** (luôn PlayerId nhỏ trước): `UPDATE ... WHERE PlayerId IN (1,2)` hoặc sắp xếp trước khi khoá.
  2. **Transaction ngắn**, ít dòng.
  3. **Index đúng**: UPDATE không có index phải scan và khoá nhiều dòng hơn cần → dễ đụng nhau.
  4. **RCSI** để loại deadlock đọc–ghi.
  5. **Retry** victim trong app (vì deadlock không thể loại bỏ 100%).
- Phân biệt: **blocking** = chờ (có thể rất lâu tới timeout), **deadlock** = vòng tròn, DB tự giết một bên trong vài giây.

### A6.8 Điều tra blocking trên production
```sql
SELECT r.session_id, r.blocking_session_id, r.wait_type, r.wait_time, r.status,
       t.text AS running_sql
FROM sys.dm_exec_requests r
CROSS APPLY sys.dm_exec_sql_text(r.sql_handle) t
WHERE r.blocking_session_id <> 0;
```
- Tìm **đầu chuỗi (head blocker)**: session đang block người khác nhưng tự nó không bị block. Thường là session **sleeping có transaction mở** (`sys.dm_exec_sessions.open_transaction_count > 0`) — dấu hiệu app quên commit/rollback, hoặc transaction có gọi HTTP chậm bên trong.
- Xử lý tạm: `KILL <spid>` (rollback transaction đó — cân nhắc). Gốc: sửa code giữ transaction lâu, thêm `XACT_ABORT ON`, chia lô.

### A6.9 Bẫy hay sai
- "HOLDLOCK để giữ lock tới cuối transaction" → nói đúng: **UPDLOCK/X đã giữ tới cuối**; HOLDLOCK = **Serializable**, khoá khoảng chống INSERT.
- "Đặt transaction là chống được race" → sai ở Read Committed: hai transaction vẫn cùng đọc được giá trị cũ rồi cùng ghi (check-then-act).
- "Dùng NOLOCK cho nhanh" → sai cho dữ liệu tiền; dùng RCSI.
- "SELECT kiểm tra trùng rồi INSERT" → phải UNIQUE + bắt lỗi trong cùng transaction.
- Quên `XACT_ABORT ON`; retry chỉ câu lỗi thay vì cả transaction.
- Không phân biệt deadlock (1205) với lock timeout (1222) và command timeout (client).

### A6.10 Câu hỏi phỏng vấn & trả lời mẫu

**Q1. (Agapi) How would you update a player's balance on a spin so it's correct under concurrency?**
> I'd make the database decide in a single statement: `UPDATE Wallets SET Balance = Balance - @bet WHERE PlayerId = @id AND Balance >= @bet`, and check the row count — zero means insufficient funds. The update takes an exclusive lock on that row until commit, so a concurrent spin waits, then re-evaluates the condition against the committed balance; no prior SELECT and no explicit lock are needed. In the same transaction I insert a ledger row with the provider's transaction ID under a unique constraint, so a retried request hits the constraint and we replay the original response instead of charging twice. With `XACT_ABORT ON` and a TRY/CATCH, any error rolls back both statements. In PlaySweeps the balance itself was owned by PLAYSTUDIOS' Nexus service, which applied our deltas with a transaction ID in exactly that way.

**Q2. (Agapi) What kinds of locks does SQL Server have?**
> By mode: shared locks for reads, update locks taken while finding rows to modify — they're compatible with shared but not with other update locks, which prevents the classic conversion deadlock — exclusive locks for the actual modification, always held until the transaction ends, intent locks at page and table level, schema locks for DDL, and key-range locks under serializable to block inserts into a range. By granularity: row or key, page and table, with escalation to a table lock at around five thousand locks per statement. And there are hints to change the defaults: `UPDLOCK` to read-for-update, `HOLDLOCK` for serializable range protection, `NOLOCK` which I avoid for money, `READPAST` for queue tables, and `NOWAIT` or `LOCK_TIMEOUT` to fail fast.

**Q3. (Agapi) What's the difference between UPDLOCK and HOLDLOCK?**
> `UPDLOCK` takes update locks instead of shared locks when reading, and keeps them until the end of the transaction, so two sessions can't both read a row intending to change it. `HOLDLOCK` is the serializable hint: it keeps read locks to the end and adds key-range locks, so nobody can insert a new row that would match my WHERE clause. Together they're the safe pattern for "check if it exists, otherwise insert" or for locking a capacity row that might not exist yet.

**Q4. (Agapi) You forgot about rollback — how do you handle errors in a transaction?**
> I set `XACT_ABORT ON`, so any runtime error — or a client timeout — rolls back the whole transaction instead of leaving it open with locks held, which otherwise can block other sessions until the connection is reset. Inside, TRY/CATCH with `IF @@TRANCOUNT > 0 ROLLBACK` and rethrow. In C#, a transaction in a `using` block rolls back on dispose if it wasn't committed. And transient errors like deadlock victim 1205 are retried as a whole transaction with backoff, which is only safe because the operation is idempotent through its transaction ID.

**Q5. Explain isolation levels. What does SQL Server use by default?**
> Read Uncommitted allows dirty reads; Read Committed, the default, prevents them but allows non-repeatable reads and phantoms; Repeatable Read holds read locks to the end; Serializable adds range locks to stop phantoms; Snapshot reads a consistent version from the start of the transaction. SQL Server's Read Committed is lock-based by default, but with Read Committed Snapshot — on by default in Azure SQL — each statement reads the last committed version from the version store, so readers and writers don't block each other. None of them alone prevents a lost update if the application reads, computes and writes back; for that I use an atomic update, a row version or an update lock.

**Q6. Optimistic vs pessimistic concurrency — when each?**
> Optimistic — a row version checked on update — when conflicts are rare and there's user think-time between read and write, like editing an order form; the loser gets a 409 and reloads. Pessimistic — `UPDLOCK` inside a short transaction — when conflicts are frequent and the logic needs several steps, like booking the last slot on a delivery truck. If the rule fits in one statement, an atomic conditional update beats both.

**Q7. How do you find and fix deadlocks?**
> SQL Server's lock monitor detects the cycle and kills one victim with error 1205. The `system_health` Extended Events session keeps the deadlock graph, which shows each session's statement, what it held and what it waited for. Typical fixes are acquiring rows in a consistent order, keeping transactions short, adding the index so updates don't scan and lock extra rows, enabling RCSI for reader–writer deadlocks, and always retrying the victim transaction in the application.

**Q8. Why not NOLOCK?**
> `NOLOCK` reads uncommitted data, so you can see values that are later rolled back, and because it ignores page locks during splits you can read the same row twice or skip rows. For dashboards that's sometimes tolerated; for balances, invoices or stock it isn't. If reads are being blocked, RCSI gives non-blocking reads of committed data instead.

### A6.11 Tự kiểm tra
1. Ma trận tương thích S/U/X. Vì sao U lock tồn tại?
2. `UPDLOCK` khác `HOLDLOCK` ở đâu? Khi nào cần cả hai?
3. Viết câu UPDATE trừ inventory an toàn; giải thích request thứ hai chờ ở đâu và thấy giá trị gì.
4. Client timeout 30 s xảy ra giữa transaction, `XACT_ABORT OFF` → chuyện gì xảy ra với lock?
5. Deadlock 1205: phát hiện ở đâu, bốn cách giảm, và app phải làm gì?
6. RCSI giải quyết gì, không giải quyết gì (lost update)?

---

## B1. ASP.NET Core: pipeline, DI, middleware, filter, cấu hình, background service

**Vì sao cần.** SA hỏi kiến trúc sẽ đi qua đây: "request đi qua những gì?", "đặt audit/permission/correlation id ở đâu?", "Singleton/Scoped/Transient?", "captive dependency?", "chạy việc nền thế nào?". Đã học ở Buổi 1–2 (`notes/01`, `notes/02`); ở đây sắp lại thành mạch có cơ chế và câu đào sâu.

### B1.1 Từ socket tới controller
1. **Kestrel** (web server có sẵn của ASP.NET Core) nhận kết nối TCP, parse HTTP, tạo **`HttpContext`** (Request, Response, User, RequestServices, Items, RequestAborted).
2. Đằng trước thường có **reverse proxy / load balancer** (Nginx, IIS, ALB, Azure Front Door) lo TLS, nén, giới hạn kích thước → app cần `UseForwardedHeaders` để biết IP/scheme thật.
3. `HttpContext` đi qua **pipeline middleware** (các lớp lồng nhau như búp bê Nga): mỗi middleware làm việc trước, gọi `await next(context)`, rồi làm việc sau khi response quay về. Không gọi `next` = **short-circuit** (ví dụ static file trả luôn, rate limiter trả 429).
4. **Routing** chọn endpoint (controller action / minimal API) và gắn **metadata** (`[Authorize]`, `[AllowAnonymous]`, policy).
5. Endpoint chạy: MVC thì thêm **filter pipeline**, model binding, validation, action, result.
6. Response đi ngược qua các middleware.

```csharp
var app = builder.Build();
app.UseExceptionHandler();          // ngoài cùng: bắt lỗi của mọi lớp bên trong
app.UseHsts(); app.UseHttpsRedirection();
app.UseStaticFiles();
app.UseRouting();                    // chọn endpoint, lộ metadata cho các lớp sau
app.UseCors();
app.UseAuthentication();             // đọc cookie/JWT → HttpContext.User
app.UseAuthorization();              // kiểm tra policy của endpoint
app.UseRateLimiter();
app.MapControllers();
```
- **Thứ tự quan trọng**: `UseAuthorization` trước `UseAuthentication` → `User` vẫn ẩn danh → "token đúng mà vẫn 401". Exception handler đặt sau một middleware thì **không bắt** được lỗi của middleware đó.

### B1.2 Middleware vs filter — đặt logic ở đâu
**"Middleware lo HTTP, filter lo action."**
| | Middleware | Filter (MVC) |
|---|---|---|
| Chạy cho | **Mọi request** (kể cả 404, 401, file tĩnh) | Chỉ request vào **action MVC** |
| Thấy gì | `HttpContext` thô | Action nào, **tham số đã bind**, `ModelState`, kết quả action |
| Hợp cho | Exception toàn cục, correlation id/tracing, authN, rate limit, request logging, security header | Validation, permission theo action (`[Permission(PROJECT_DOWNLOAD)]` ở Joblogic), audit theo action, xác thực hash callback, transaction quanh action |

Thứ tự filter: **Authorization → Resource → (model binding) → Action → (action chạy) → Exception → Result**.
- **Resource filter** chạy **trước model binding** → hợp để đọc **raw body** (xác thực chữ ký HMAC của webhook Pragmatic: body là stream chỉ đọc một lần → `Request.EnableBuffering()`). Action filter chỉ thấy object đã bind, serialize lại có thể khác byte gốc → hash sai.
- Minimal API dùng **endpoint filter** (`AddEndpointFilter`).
- Middleware viết dạng class được tạo **một lần (singleton)** → service Scoped phải inject qua **tham số của `InvokeAsync`**, không qua constructor.

### B1.3 Dependency Injection: lifetime và captive dependency
| Lifetime | Tạo khi | Ví dụ đúng |
|---|---|---|
| **Singleton** | Một lần cho cả app | Cấu hình, `IMemoryCache`, `IHttpClientFactory`, client Redis (`ConnectionMultiplexer`), `TimeProvider` |
| **Scoped** | Một lần **mỗi request** (mỗi `IServiceScope`) | `DbContext`, unit of work, service cần biết user/tenant hiện tại |
| **Transient** | Mỗi lần resolve | Service nhẹ, không state |

- Scope tạo đầu request, **Dispose cuối request** (container dispose luôn các Scoped/Transient `IDisposable` nó tạo).
- **Captive dependency**: service sống dài giữ service sống ngắn. Ví dụ Singleton `QuoteCache` inject `AppDbContext` (Scoped) → DbContext sống suốt process:
  - nhiều request dùng chung → **"A second operation was started on this context"** (DbContext không thread-safe);
  - **change tracker phình** (mọi entity đã load bị giữ) → memory leak, `DetectChanges` chậm dần;
  - dữ liệu cũ (entity đã track không được làm mới).
  Sửa: đổi lifetime cho đúng, hoặc Singleton dùng `IDbContextFactory<T>` / `IServiceScopeFactory` tạo context ngắn hạn khi cần. Phòng ngừa: bật `ValidateScopes` + `ValidateOnBuild` ở **mọi** môi trường (mặc định chỉ bật ở Development).
- Quy tắc một câu: **không inject service sống ngắn hơn vào service sống dài hơn.**
- **Constructor injection** (phụ thuộc lộ rõ, dễ test) vs **service locator** (`IServiceProvider.GetService` rải khắp nơi: giấu phụ thuộc). Service locator chỉ ở chỗ hạ tầng (factory, middleware, background job tạo scope).
- .NET 8: **keyed services** `AddKeyedScoped<IRtoProvider, AcmeRto>("acme")` + `[FromKeyedServices("acme")]`. PlaySweeps dùng **Autofac** (module, decorator, assembly scanning); built-in DI đủ cho đa số trường hợp.

### B1.4 Xử lý lỗi toàn cục, ProblemDetails, logging
- `.NET 8`: `builder.Services.AddProblemDetails()` + `AddExceptionHandler<GlobalExceptionHandler>()` + `app.UseExceptionHandler()`. `IExceptionHandler.TryHandleAsync` trả `true` nếu đã xử lý, `false` để handler sau thử.
- 500: trả ProblemDetails **không lộ** `ex.Message`/stack trace, kèm `traceId` để support tra log.
- **"Exception cho chuyện bất ngờ, Result cho chuyện bình thường"**: thiếu số dư, đơn đã huỷ là chuyện bình thường → Result/OneOf → map ra 409/422; DB sập là bất ngờ → exception → 500/503.
- Log: 4xx là **Warning** (lỗi phía client), 5xx là **Error** + alert. Structured logging: `_logger.LogInformation("Quote {QuoteId} finalized by {UserId}", id, userId)` (template, không nối chuỗi) → tìm được theo field trong App Insights/CloudWatch/Loki. Correlation id / trace id ở mọi log.

### B1.5 Cấu hình và secret
- Nguồn cấu hình theo thứ tự đè: `appsettings.json` → `appsettings.{Environment}.json` → **User Secrets** (chỉ Development) → **biến môi trường** → command line → nguồn thêm (**AWS Secrets Manager / Parameter Store, Azure Key Vault, App Configuration**).
- **Options pattern**: `services.Configure<TaxOptions>(config.GetSection("Tax"))` + validate lúc khởi động (`ValidateDataAnnotations().ValidateOnStart()`).
  - `IOptions<T>`: đọc một lần (Singleton).
  - `IOptionsSnapshot<T>`: đọc lại **mỗi request** (Scoped).
  - `IOptionsMonitor<T>`: Singleton nhưng nhận **thay đổi nóng** + callback `OnChange`.
- Secret không bao giờ nằm trong git; app lấy credential cloud qua **IAM role / Managed Identity**, không access key.

### B1.6 Việc nền: BackgroundService, Channel, graceful shutdown
- `BackgroundService` (implement `IHostedService`) được đăng ký như **Singleton** → mỗi lần xử lý phải **tạo scope** để lấy DbContext:
```csharp
public class PdfWorker(Channel<Guid> queue, IServiceScopeFactory scopes, ILogger<PdfWorker> log) : BackgroundService
{
    protected override async Task ExecuteAsync(CancellationToken stoppingToken)
    {
        await foreach (var quoteId in queue.Reader.ReadAllAsync(stoppingToken))
        {
            using var scope = scopes.CreateScope();
            var svc = scope.ServiceProvider.GetRequiredService<QuotePdfService>();
            try { await svc.GenerateAsync(quoteId, stoppingToken); }
            catch (Exception ex) { log.LogError(ex, "PDF failed for {QuoteId}", quoteId); }
        }
    }
}
```
- `Channel<T>` là hàng đợi **trong RAM**: app restart/deploy → **mất việc** đang chờ. Việc không được mất (gửi hợp đồng, cộng tiền) → **queue bền** (SQS/Service Bus) hoặc **outbox** trong DB (C5), hoặc Hangfire (lưu job trong DB).
- **Graceful shutdown**: khi deploy, host gửi `stoppingToken`, mặc định chờ **30 s** (`HostOptions.ShutdownTimeout`) để xử lý xong; load balancer cần **connection draining** để ngừng gửi request mới tới instance đang tắt.
- Nhiều instance → mỗi instance có một `BackgroundService` → job định kỳ chạy **N lần** → cần leader election / distributed lock / scheduler trung tâm, và job phải **idempotent**.

### B1.7 Health check, rate limiting, minimal API
- **Liveness** (`/health/live`): process còn sống không, **không** kiểm tra DB (DB chết mà liveness fail → orchestrator restart hàng loạt pod vô ích). **Readiness** (`/health/ready`): đã sẵn sàng nhận traffic chưa (DB, cache kết nối được) → load balancer chỉ gửi request khi ready.
- Rate limiting built-in (.NET 7+): `AddRateLimiter` với **fixed window, sliding window, token bucket, concurrency**; nhưng counter nằm trong RAM **từng instance** → nhiều instance cần Redis hoặc limit ở gateway.
- **Minimal API vs Controller**: minimal gọn, nhanh, hợp API nhỏ/microservice; controller hợp app lớn có filter, convention, nhiều action. Không phải chọn phe.

### B1.8 Bẫy hay sai
- Đặt `UseAuthorization` trước `UseAuthentication`, hoặc `UseExceptionHandler` không ở ngoài cùng.
- Inject Scoped vào constructor của middleware class / Singleton.
- Nghĩ "Scoped = một instance cho mỗi thread" → sai, là **mỗi scope** (mỗi request).
- Dùng `Channel` cho việc liên quan tiền rồi nói "không mất".
- Liveness kiểm tra DB.
- `IOptions<T>` rồi thắc mắc vì sao đổi cấu hình không có tác dụng.

### B1.9 Câu hỏi phỏng vấn & trả lời mẫu

**Q1. Walk me through what happens to a request in ASP.NET Core.**
> Kestrel accepts the connection and builds an HttpContext. It goes through the middleware pipeline in order — exception handling first, then HTTPS, routing, CORS, authentication, authorization, rate limiting — each one can act before and after calling the next. Routing picks the endpoint and exposes its metadata, so authorization knows the policy. For a controller, the MVC filter pipeline runs: authorization filters, resource filters, model binding and validation, action filters, the action, then result filters, and the response flows back out through the middleware. Order matters: authorization before authentication gives you a 401 with a valid token.

**Q2. Where would you put audit logging, a permission check and a correlation ID?**
> Correlation ID and request timing go in middleware, as early as possible, because they apply to every request including 404s and 401s. A permission check per action — like "can download project documents" — fits an authorization filter or a policy attribute, because it needs to know which action is running. Audit of business changes I'd do in the application layer or a SaveChanges interceptor, since it should capture what actually changed, not just which endpoint was hit. Business rules never go in middleware or filters.

**Q3. Explain Singleton, Scoped and Transient. What's a captive dependency?**
> Singleton is one instance for the app — configuration, caches, the HTTP client factory. Scoped is one per request — the DbContext and anything that depends on the current user or tenant. Transient is a new instance every time it's resolved. A captive dependency is a longer-lived service holding a shorter-lived one, for example a singleton cache with a DbContext injected: the context lives for the whole process, gets used by concurrent requests and throws "a second operation was started", and its change tracker grows forever. I fix it with `IDbContextFactory` or a scope factory, and enable `ValidateScopes` and `ValidateOnBuild` in every environment so it fails at startup.

**Q4. How do you handle exceptions globally?**
> `UseExceptionHandler` as the outermost middleware with an `IExceptionHandler`, returning ProblemDetails with a trace ID and no internal details. Expected business failures — insufficient balance, an order already cancelled — aren't exceptions in my code; handlers return a result type that the controller maps to 409 or 422. Unexpected errors log at Error and alert; client errors log at Warning.

**Q5. How do you run background work in ASP.NET Core?**
> For lightweight in-process work, a `BackgroundService` reading from a bounded `Channel`, creating a new DI scope per item so it gets its own DbContext. That work is lost on restart, so anything that must not be lost — sending a contract, crediting money — goes through a durable queue or a transactional outbox, processed idempotently. With several instances, scheduled jobs run on each instance unless I use a central scheduler or a lock, so jobs must be idempotent.

**Q6. Liveness vs readiness?**
> Liveness answers "is the process alive" and should be cheap, so the orchestrator only restarts truly stuck instances. Readiness answers "can I take traffic now" and may check the database or cache, so the load balancer stops routing to an instance that's starting up or has lost a dependency. Putting the database check in liveness makes a database blip restart every pod at once.

**Q7. IOptions, IOptionsSnapshot, IOptionsMonitor?**
> `IOptions` reads once and is a singleton; `IOptionsSnapshot` is scoped and re-reads per request; `IOptionsMonitor` is a singleton that sees changes live and can notify. I validate options at startup so a missing setting fails the deployment instead of the first customer request.

### B1.10 Tự kiểm tra
1. Viết đúng thứ tự 6 middleware chính. Đổi chỗ AuthN/AuthZ thì sao?
2. Vì sao xác thực hash webhook phải ở resource filter, không phải action filter?
3. Singleton inject DbContext: kể 3 hậu quả và 2 cách sửa.
4. `Channel` + `BackgroundService` có hợp cho gửi email xác nhận thanh toán không? Vì sao?
5. Liveness kiểm tra DB thì chuyện gì xảy ra khi DB chập chờn 30 giây?

---

## B2. ASP.NET MVC: model binding, validation, CSRF, over-posting, PRG

**Vì sao cần.** JD ghi "ASP.NET MVC và/hoặc Web API", và code tiếp quản từ đối tác Mỹ có thể là MVC (thậm chí MVC 5 trên .NET Framework). Hiệp có kinh nghiệm thật ở Joblogic (khoảng 20 view `.cshtml`, 27 controller, Razor + jQuery + Vue nhúng). Câu SA hay hỏi: "submit form thì chuyện gì xảy ra", "over-posting", "CSRF", "double submit".

### B2.1 Một lần submit form đi qua những gì
```
Trình duyệt POST /quotes/42/edit (form-urlencoded + cookie đăng nhập + anti-forgery token)
 → middleware (auth cookie → User)
 → routing chọn QuotesController.Edit(int id, EditQuoteViewModel vm)
 → filter: Authorization → Resource → model binding → validation → Action filter
 → action: kiểm tra ModelState, gọi handler, nhận Result
     ✔ thành công → RedirectToAction("Details", new { id })   (302)
     ✘ lỗi validation → return View(vm)   (render lại form kèm lỗi)
 → Result filter → Razor render HTML (nếu là View)
```
- **Model binding** lấy giá trị theo tên từ: route (`{id}`), query string, form, body (`[FromBody]`, chỉ đọc **một lần**), header (`[FromHeader]`), service (`[FromServices]`).
- `[ApiController]` (cho API) tự trả **400 ProblemDetails** khi `ModelState` không hợp lệ và suy luận nguồn bind; MVC trả View thì **tự kiểm tra** `ModelState.IsValid`.

### B2.2 Over-posting (mass assignment) — lỗi bảo mật kinh điển
Entity:
```csharp
public class Quote { public int Id; public string CustomerName; public decimal Discount; public bool IsApproved; }
```
Action bind thẳng entity:
```csharp
[HttpPost] public async Task<IActionResult> Edit(Quote quote) { _db.Update(quote); await _db.SaveChangesAsync(); ... }
```
Form chỉ có ô `CustomerName`, nhưng kẻ xấu mở DevTools thêm `IsApproved=true&Discount=500` → model binder gán luôn → **tự duyệt báo giá, tự giảm giá**. `_db.Update(entity)` còn đánh dấu **mọi cột** là sửa → ghi đè cả cột không có trong form thành giá trị mặc định.
Chặn:
- **ViewModel/DTO chỉ chứa field được phép sửa**, map tay vào entity đã load từ DB:
```csharp
public record EditQuoteViewModel(string CustomerName, string? Notes);
var quote = await _db.Quotes.SingleAsync(q => q.Id == id && q.TenantId == _tenant.Id);
quote.Rename(vm.CustomerName);      // method domain có luật
await _db.SaveChangesAsync();       // EF chỉ UPDATE cột thật sự đổi
```
- Không dùng `[Bind]` dài, không `TryUpdateModelAsync` không giới hạn field.
- Field nhạy cảm (giá, chiết khấu, trạng thái duyệt) **server tự tính/kiểm quyền**, không tin form.

### B2.3 Validation hai phía
- **Client-side** (jQuery Unobtrusive Validation, React Hook Form): chỉ để UX nhanh. **Server-side luôn bắt buộc** (người dùng tắt JS, gọi thẳng API).
- DataAnnotations (`[Required]`, `[Range(0, 100)]`, `[StringLength]`) cho luật đơn giản; **FluentValidation** cho luật phức tạp/phụ thuộc nhau; luật nghiệp vụ sâu (hạn mức, trạng thái) nằm ở **domain/handler**, trả lỗi về `ModelState.AddModelError` để hiển thị cạnh field.
- Razor: `<span asp-validation-for="CustomerName"></span>`, `<div asp-validation-summary="ModelOnly">`.

### B2.4 CSRF và anti-forgery token
**Bản chất:** trang dùng **cookie authentication** → trình duyệt **tự động** gửi cookie cho mọi request tới domain đó, kể cả request do **site khác** kích hoạt.
Tấn công: người dùng đang đăng nhập Ops Hub, mở `evil.com` có form ẩn tự submit `POST https://opshub.com/orders/42/cancel` → trình duyệt kèm cookie → server tưởng người dùng thật bấm.
Phòng thủ:
- **Anti-forgery token** (synchronizer token): server đặt một token vào form (`<input name="__RequestVerificationToken">`, tag helper `<form>` tự thêm) và một cookie liên kết; POST phải có **cả hai khớp nhau**. `evil.com` không đọc được token (same-origin policy) → không giả được.
- `[ValidateAntiForgeryToken]` trên action, hoặc `AutoValidateAntiforgeryTokenAttribute` **toàn cục** cho mọi POST/PUT/DELETE.
- AJAX: gửi token qua header (`RequestVerificationToken`).
- Cookie `SameSite=Lax/Strict` chặn thêm phần lớn trường hợp (A2.3).
- **API dùng `Authorization: Bearer`** (token do JS tự gắn vào header) **không bị CSRF** vì trình duyệt không tự gửi header đó → không cần anti-forgery; nhưng nếu SPA để JWT **trong cookie** thì lại cần chống CSRF.

### B2.5 PRG (Post–Redirect–Get) chống double submit
- POST thành công mà trả thẳng View → người dùng bấm F5 → trình duyệt **gửi lại POST** → tạo order lần 2.
- PRG: POST xử lý xong → `RedirectToAction("Details")` (**302/303**) → trình duyệt GET trang kết quả → F5 chỉ GET lại. Thông báo "Đã lưu" qua `TempData` (sống đúng một request sau).
- Chống double click nhanh: disable nút khi submit (UX) + **idempotency/unique constraint ở server** (C3). PRG không chặn được hai click trước khi trang kịp chuyển.

### B2.6 Razor, view, tái sử dụng UI
- `@model EditQuoteViewModel`, `asp-for`, `asp-action`, `asp-route-id` (tag helper); `@` **tự HTML-encode** → an toàn XSS mặc định. Nguy hiểm: `@Html.Raw(...)` với dữ liệu người dùng (rich text điều khoản) → **sanitize** (HtmlSanitizer) + CSP header.
- **ViewModel** (có kiểu, compile-time check) > `ViewBag`/`ViewData` (dynamic, gõ sai tên là lỗi runtime).
- **Layout** (`_Layout.cshtml`), **partial view** (mảnh HTML dùng lại, không logic riêng), **view component** (có logic + DI riêng, ví dụ widget "Balance due" trên nhiều trang), **tag helper** tự viết.
- **Razor Pages**: mô hình theo trang (PageModel) cho CRUD đơn giản.
- Joblogic: Razor + **Vue nhúng** cho phần tương tác (kéo-thả lưới Selling Rate), Razor cho form thường.

### B2.7 Concurrency trên form MVC
Hai nhân viên cùng mở form sửa đơn:
- Gửi `RowVersion` (base64) trong **hidden field**; khi lưu gán `_db.Entry(order).Property(o => o.RowVersion).OriginalValue = vm.RowVersion;` → EF thêm `WHERE RowVersion = @original` → người lưu sau nhận `DbUpdateConcurrencyException` → hiển thị "Đơn đã bị người khác sửa", cho xem bản mới.

### B2.8 Authorization trong MVC
- `[Authorize]`, `[Authorize(Roles = "Manager")]`, **policy-based** `[Authorize(Policy = "CanApproveQuote")]` (requirement + handler).
- **Resource-based**: quyền phụ thuộc **dữ liệu cụ thể** (đơn này thuộc store của user không?) → `await _authz.AuthorizeAsync(User, order, "CanEdit")`. Không có bước này = lỗi **IDOR/BOLA** (C2).
- Joblogic: attribute permission tự viết trên action (`[Permission(...)]`).

### B2.9 MVC 5 (.NET Framework) vs ASP.NET Core MVC
| | ASP.NET MVC 5 | ASP.NET Core MVC |
|---|---|---|
| Nền tảng | .NET Framework, chỉ Windows/IIS, `System.Web` | .NET 6/8+, cross-platform, Kestrel |
| Pipeline | `Global.asax`, HTTP modules/handlers | Middleware |
| DI | Không có sẵn (dùng Autofac/Unity) | Có sẵn |
| Cấu hình | `web.config` | `appsettings.json`, env vars, options |
| Async | `.Result` dễ **deadlock** (có SynchronizationContext) | Không deadlock nhưng starvation |
- Migrate dần: **strangler fig** — đặt app Core phía trước (YARP reverse proxy) chuyển từng route; hoặc dùng công cụ **.NET Upgrade Assistant**; tách thư viện nghiệp vụ sang .NET Standard/.NET 8 trước.

### B2.10 Bẫy hay sai
- Bind thẳng entity; dùng `_db.Update(entity)` từ dữ liệu form.
- "Có validation phía client là đủ".
- "API cũng cần anti-forgery" / "SPA để JWT trong cookie thì không cần chống CSRF" — cả hai sai.
- Nghĩ PRG chống được double click.
- `Html.Raw` dữ liệu người dùng.

### B2.11 Câu hỏi phỏng vấn & trả lời mẫu

**Q1. Walk me through submitting a form in ASP.NET MVC.**
> The browser posts the form with the auth cookie and the anti-forgery token. Middleware authenticates the cookie, routing selects the action, and the filter pipeline runs: authorization, anti-forgery validation, model binding into a view model, then validation into ModelState. The action checks ModelState; if invalid, it returns the same view with the errors; if valid, it calls the application handler and, on success, redirects to a GET page — post-redirect-get — so a refresh doesn't resubmit.

**Q2. What is over-posting and how do you prevent it?**
> It's when the model binder sets properties the form never intended to expose, because an attacker adds fields like `IsApproved=true` or a discount to the request. It happens when you bind directly to entities. I bind to a view model with only the editable fields, load the entity from the database scoped to the user's tenant, and apply the changes through domain methods. Prices, discounts and approval flags are calculated or authorised on the server, never taken from the form.

**Q3. What is CSRF and why does MVC need anti-forgery tokens but a bearer-token API doesn't?**
> CSRF abuses the fact that browsers attach cookies automatically: another site can make the user's browser post to our app with their session cookie. The anti-forgery token is a secret value in the form that the attacker's site can't read, so a forged request fails validation; SameSite cookies add another layer. A bearer-token API isn't exposed the same way, because the browser never adds the Authorization header by itself — our JavaScript does. If a SPA keeps its token in a cookie, though, it needs CSRF protection again.

**Q4. A user double-submits an order form. How do you stop duplicates?**
> On the UI, disable the button on submit and use post-redirect-get so a refresh doesn't repeat the POST. Those only improve the experience; the real guarantee is on the server: the form carries a unique submission or idempotency key, and the order insert relies on a unique constraint in the same transaction, so a second request returns the order that was already created.

**Q5. Two staff edit the same order form. What happens?**
> I'd use optimistic concurrency: the form carries the row version in a hidden field, and the update includes it in the WHERE clause. The second person to save gets a concurrency exception, and we show them that the order changed, with the latest values, instead of silently overwriting the first person's changes.

**Q6. How would you migrate an MVC 5 app to ASP.NET Core?**
> Incrementally. I'd put an ASP.NET Core app in front with YARP as a reverse proxy, move routes one by one, and share session or auth between the two during the transition. Business logic moves first into libraries that target modern .NET. A big-bang rewrite loses hidden business rules and blocks feature work for months, so I'd avoid it.

### B2.12 Tự kiểm tra
1. Viết payload over-posting cho form sửa quote; sửa code thế nào?
2. Vì sao `evil.com` không lấy được anti-forgery token?
3. PRG chặn được gì, không chặn được gì?
4. API Bearer có cần anti-forgery không? JWT trong cookie thì sao?
5. Resource-based authorization khác `[Authorize(Roles=...)]` ở đâu?

---

## B3. EF Core và Dapper: tracking, N+1, split query, concurrency, transaction, migration

**Vì sao cần.** Hầu hết bug hiệu năng trong app .NET nằm ở lớp truy cập dữ liệu: N+1, kéo cả bảng về RAM, tracking thừa, JOIN nhân dòng. SA sẽ hỏi "EF hay Dapper", "N+1 là gì và phát hiện thế nào", "migration không downtime". Nền SQL ở A5/A6; phần này là **ORM nói chuyện với SQL thế nào**.

### B3.1 DbContext là gì
- **DbContext = Unit of Work + change tracker + một connection** (mở khi cần, trả về pool khi xong). **Scoped** (một mỗi request), **không thread-safe**: một context chỉ chạy **một lệnh tại một thời điểm**.
- `DbSet<T>` đã là repository; `SaveChanges()` gom mọi thay đổi đã track thành các câu INSERT/UPDATE/DELETE trong **một transaction**.
- **Identity resolution**: trong một context, cùng một khoá chính chỉ có **một object** → query lại `Quotes.Find(42)` trả về đúng object đã track (không đọc lại DB nếu dùng `Find`).

### B3.2 Change tracking hoạt động thế nào
1. Query có tracking → EF lưu **snapshot** giá trị gốc của từng entity.
2. Bạn sửa property trong C#.
3. `SaveChanges` gọi **`DetectChanges`**: so từng entity đang track với snapshot → sinh `UPDATE Quotes SET CustomerName = @p0 WHERE Id = @p1` **chỉ với cột đổi**.
- Chi phí: track 10.000 entity = RAM cho 10.000 snapshot + `DetectChanges` duyệt hết. Màn hình **chỉ đọc** → `AsNoTracking()`, tốt hơn nữa là **projection**:
```csharp
var rows = await _db.Orders
    .Where(o => o.StoreId == storeId && o.CreatedAt >= from)
    .OrderByDescending(o => o.CreatedAt)
    .Select(o => new OrderRow(o.Id, o.Customer.Name, o.Total, o.Status))   // chỉ 4 cột, không tracking
    .Take(50)
    .ToListAsync(ct);
```
Projection sinh `SELECT` đúng cột cần, tự JOIN `Customer`, khớp được **covering index** (A5.3).

### B3.3 N+1 — phát hiện và sửa
```csharp
var orders = await _db.Orders.Where(o => o.StoreId == id).ToListAsync();   // 1 query
foreach (var o in orders)
    total += o.Lines.Sum(l => l.Amount);   // lazy loading: mỗi order 1 query → N query
```
50 order = **51 query**; mỗi query 2 ms round-trip → 100 ms chỉ để chờ mạng; 500 order → 1 s. Không lazy loading mà **query trong vòng lặp** cũng y hệt.
- Sửa: projection tính ở DB (`Select(o => new { o.Id, Total = o.Lines.Sum(l => l.Amount) })`), `Include(o => o.Lines)`, hoặc batch: lấy danh sách id rồi một query `WHERE OrderId IN (...)` (`Contains`).
- Phát hiện: log `Microsoft.EntityFrameworkCore.Database.Command` (có thời gian từng lệnh), **đếm số câu SQL mỗi request** (App Insights dependency, MiniProfiler); trace thấy hàng chục span SQL giống nhau liên tiếp = N+1.

### B3.4 Include nhiều collection: nhân dòng và `AsSplitQuery`
- `Include(u => u.Transactions).Include(u => u.LoginHistories)` → một câu SQL `LEFT JOIN` cả hai → 100 × 50 = **5.000 dòng** cho 150 dòng thật (A5.7). EF Core cảnh báo trong log.
- `.AsSplitQuery()` (EF Core 5+): tách thành 3 câu (User, Transactions, LoginHistories) → ~151 dòng. Đổi lại: thêm round-trip, và **không nhất quán tuyệt đối** nếu có ghi xen giữa các câu (trừ khi chạy trong transaction Snapshot/Serializable). Có thể đặt mặc định toàn cục `UseQuerySplittingBehavior(QuerySplittingBehavior.SplitQuery)`.
- Include **chuỗi** (Order → Lines → Product) không nhân dòng theo kiểu này.

### B3.5 Những API cần biết
- `ToQueryString()`: xem SQL EF sẽ sinh.
- `ExecuteUpdateAsync` / `ExecuteDeleteAsync` (EF 7+): một câu SQL cập nhật hàng loạt, **không load entity, không qua change tracker** → nhanh, nhưng **bỏ qua interceptor/audit/domain event** dựa trên SaveChanges.
```csharp
await _db.Quotes.Where(q => q.Status == QuoteStatus.Sent && q.ExpiresAt < now)
    .ExecuteUpdateAsync(s => s.SetProperty(q => q.Status, QuoteStatus.Expired), ct);
```
- **Global query filter**: `modelBuilder.Entity<Order>().HasQueryFilter(o => o.TenantId == _tenant.Id && !o.IsDeleted)` → tự thêm vào mọi query (multi-tenant, soft delete). `IgnoreQueryFilters()` để bỏ khi cần (cẩn thận).
- **Interceptor**: `SaveChangesInterceptor` (audit, set `UpdatedAt`), `DbConnectionInterceptor` (Joblogic set `SESSION_CONTEXT` tenant mỗi lần mở connection).
- **Value converter / owned type**: lưu `Money` value object, enum dạng string; `HasPrecision(18,2)` cho decimal.
- **Compiled query** (`EF.CompileAsyncQuery`): bỏ bước dịch LINQ cho query nóng.
- **Raw SQL an toàn**: `FromSql($"... WHERE Id = {id}")` / `FromSqlInterpolated` → **tham số hoá**; `FromSqlRaw("... " + id)` → **SQL injection**. EF Core 8: `Database.SqlQuery<T>(...)` map SQL thô ra kiểu bất kỳ.
- EF Core ≥ 3 **ném lỗi** khi LINQ không dịch được (bản ≤ 2 âm thầm chạy trong RAM). EF6 vẫn chạy trên .NET 8 nhưng không phát triển thêm (Joblogic còn EF6 ở Core cũ).

### B3.6 Concurrency với EF
```csharp
public class Order { public int Id { get; set; } [Timestamp] public byte[] RowVersion { get; set; } = default!; }
try { await _db.SaveChangesAsync(ct); }
catch (DbUpdateConcurrencyException) { return Conflict(); }   // 409, client tải lại
```
EF sinh `UPDATE ... WHERE Id = @id AND RowVersion = @original`; 0 dòng → exception. Với **atomic update** (trừ tồn kho, tăng `Booked`), dùng `ExecuteUpdateAsync` có điều kiện hoặc SQL thô — không load-sửa-save (lost update, A6.3).

### B3.7 Transaction và retry trong EF
- `SaveChanges` **đã là một transaction**. Tự mở transaction khi: nhiều lần `SaveChanges` phải cùng thành công, trộn SQL thô + EF, hoặc cần `UPDLOCK`.
- **Không** gọi HTTP/email/queue bên trong transaction (giữ lock lâu; gửi email rồi rollback = email sai) → **outbox** (C5).
- `EnableRetryOnFailure()` (Azure SQL/RDS chập chờn): retry tự động **không được** dùng cùng transaction tự mở trừ khi bọc trong **execution strategy**:
```csharp
var strategy = _db.Database.CreateExecutionStrategy();
await strategy.ExecuteAsync(async () =>
{
    await using var tx = await _db.Database.BeginTransactionAsync(ct);
    // ... nhiều bước
    await _db.SaveChangesAsync(ct);
    await tx.CommitAsync(ct);
});   // lỗi tạm thời → chạy lại CẢ khối → khối phải idempotent
```

### B3.8 Dapper — khi nào và bẫy
- **Dapper** = micro-ORM của StackExchange: extension method trên `IDbConnection`, bạn viết SQL, nó map kết quả sang object (sinh IL và cache). Nhanh gần ADO.NET, không có change tracking/migration/LINQ.
- PlaySweeps dùng **Dapper + stored procedure + repository** bọc tên SP và mapping (DI bằng Autofac).
- Chọn: **EF Core** cho CRUD nghiệp vụ, domain model, migration, LINQ an toàn kiểu; **Dapper** cho query đọc phức tạp/báo cáo, SQL tối ưu tay, stored procedure có sẵn. Dùng chung trong một app là bình thường.
- Bẫy Dapper:
  - **Nối chuỗi SQL** → injection. Luôn `@param`.
  - Quên truyền `transaction:` khi đã mở transaction → lệnh chạy ngoài transaction (hoặc lỗi).
  - `WHERE Id IN @ids` với > **2.100 tham số** (giới hạn SQL Server) → dùng TVP (table-valued parameter) hoặc chia lô.
  - `string` mặc định thành `nvarchar` → cột `varchar` bị `CONVERT_IMPLICIT`, mất index seek → `new DbString { Value = x, IsAnsi = true }`.
  - `Query` mặc định **buffered** (đọc hết vào RAM); dữ liệu lớn → `buffered: false` / `QueryUnbufferedAsync`.

### B3.9 Migration an toàn khi deploy không downtime
**Vấn đề:** rolling deploy chạy **bản cũ và bản mới cùng lúc** vài phút → schema phải hợp với **cả hai**.
**Expand → Migrate → Contract** (mỗi bước một lần deploy):
- Thêm cột NOT NULL: (1) thêm cột **NULL** (hoặc có default) → (2) code mới ghi cột đó, job **backfill theo lô** dữ liệu cũ → (3) đổi sang NOT NULL.
- Đổi tên cột `Name` → `CustomerName`: thêm cột mới, ghi cả hai, backfill, chuyển đọc sang cột mới, ngừng ghi cột cũ, deploy sau mới xoá cột cũ.
- Tạo index trên bảng lớn: `CREATE INDEX ... WITH (ONLINE = ON)` (Enterprise/Azure SQL) để không khoá bảng; EF migration cho phép SQL tuỳ chỉnh.
- UPDATE/DELETE hàng loạt: chia lô 1.000–4.000 dòng (tránh **lock escalation** ~5.000, A6.2) và log lớn.
- **Không** gọi `Database.Migrate()` lúc app khởi động ở production (nhiều instance cùng chạy migration, app thiếu quyền DDL nên cấp quyền quá rộng) → chạy ở pipeline: `dotnet ef migrations bundle` (file chạy được) hoặc `dotnet ef migrations script --idempotent`; với Dapper dùng **DbUp/Flyway**.
- Backup/point-in-time restore trước migration lớn; có rollback plan (thường là "rollback app, giữ schema" nhờ expand/contract).

### B3.10 Bẫy hay sai
- Load entity → sửa → save cho trừ tồn kho/balance (lost update).
- `ToList()` rồi mới `Where` / repository trả `IEnumerable` (A3.8).
- `Include` mọi thứ "cho chắc".
- Nghĩ `AsSplitQuery` luôn nhanh hơn (thêm round-trip; ít dòng thì single query tốt hơn).
- `ExecuteUpdate` rồi thắc mắc vì sao audit không ghi.
- `Database.Migrate()` khi startup ở prod.

### B3.11 Câu hỏi phỏng vấn & trả lời mẫu

**Q1. Tracking vs AsNoTracking vs projection?**
> Tracking keeps a snapshot of each loaded entity so SaveChanges can detect what changed and update only those columns — I use it when I'm going to modify the data. For read-only screens, `AsNoTracking` avoids the snapshot cost, and projecting with `Select` into a DTO is better still: EF fetches only the needed columns, joins what it needs, and the query can be served by a covering index.

**Q2. What is the N+1 problem and how do you detect it?**
> One query loads a list and then each item triggers another query — through lazy loading or a query inside a loop — so 50 orders become 51 round trips; at 2 ms each that's 100 ms of pure waiting, growing with the data. I detect it by counting SQL commands per request in the EF command log, Application Insights dependencies or MiniProfiler: a trace with dozens of identical queries in a row is the giveaway. The fix is a projection that computes in the database, an `Include`, or one batched query with `Contains`.

**Q3. When would you use split queries?**
> When I include two or more collections of the same parent: a single query joins them and returns the product of their row counts — 100 transactions times 50 logins is 5,000 rows instead of 150 — so network and materialisation explode. Split query issues one query per collection. The trade-offs are extra round trips and the possibility of inconsistent data if writes happen between the queries, so for small collections a single query is fine.

**Q4. EF Core or Dapper?**
> EF Core for most business code: change tracking, migrations, type-safe LINQ and less boilerplate. Dapper when I want full control of the SQL — complex reporting queries, hand-tuned joins, or existing stored procedures, which is what PlaySweeps used behind repositories. They coexist fine. With Dapper the risks are mine: always parameters, pass the transaction explicitly, watch the 2,100-parameter limit and nvarchar versus varchar parameters.

**Q5. When do you need an explicit transaction, and what shouldn't happen inside it?**
> SaveChanges is already transactional, so I open one explicitly when several SaveChanges calls or raw SQL must commit together, or when I need an update lock. Inside it I never call external services or send emails: it holds locks while waiting on the network, and if we roll back, the email has already gone. Side effects go through an outbox written in the same transaction. If retry-on-failure is enabled, the whole transaction runs inside the execution strategy and has to be idempotent.

**Q6. How do you add a NOT NULL column to a large table without downtime?**
> Expand and contract across deployments: add it as nullable or with a default, deploy code that writes it, backfill old rows in small batches to avoid lock escalation, then make it NOT NULL in a later release. During a rolling deploy old and new versions run side by side, so every schema step has to work for both. Migrations run from the pipeline as a bundle or idempotent script, not from `Database.Migrate()` at startup.

**Q7. How do you prevent SQL injection with raw SQL in EF or Dapper?**
> Never concatenate input into SQL. In EF, `FromSql` or `FromSqlInterpolated` turn interpolated values into parameters, while `FromSqlRaw` with concatenation does not. In Dapper, always use `@parameters`. Dynamic column names for sorting come from a whitelist, never from the request.

### B3.12 Tự kiểm tra
1. `DetectChanges` làm gì? Vì sao track 10.000 entity chậm?
2. Viết lại vòng lặp N+1 ở B3.3 thành một query.
3. `AsSplitQuery`: lợi, hại, khi nào không nên.
4. `ExecuteUpdateAsync` bỏ qua những gì?
5. Kể 4 bẫy Dapper.
6. Đổi tên cột trên bảng 50 triệu dòng mà không downtime: các bước?

---

## B4. REST API design

**Vì sao cần.** Đây là giao điểm lớn nhất giữa SA (tự khai REST) và vị trí C#. Câu hỏi thường là thiết kế cụ thể: "API finalize quote rồi chuyển thành order", "double click tạo order", "hai người sửa cùng lúc", "phân trang danh sách lớn", "versioning cho mobile app". Câu trả lời Senior gắn **ngữ nghĩa HTTP** với **đúng/sai dữ liệu**.

### B4.1 Resource, method, ngữ nghĩa
- **Resource** là danh từ số nhiều, có cấp: `/quotes`, `/quotes/{id}`, `/quotes/{id}/lines`, `/orders/{id}/payments`.
- **Method và tính chất:**
| Method | Safe (không đổi dữ liệu) | Idempotent (gọi N lần = 1 lần) | Dùng cho |
|---|---|---|---|
| GET | ✅ | ✅ | Đọc |
| PUT | ❌ | ✅ | Thay **toàn bộ** resource (client gửi bản đầy đủ) |
| PATCH | ❌ | ❌ (theo định nghĩa; có thể thiết kế idempotent) | Sửa **một phần** (JSON Merge Patch / JSON Patch) |
| DELETE | ❌ | ✅ | Xoá (lần 2 trả 404 hoặc 204, trạng thái server vẫn như nhau) |
| POST | ❌ | ❌ | Tạo mới, hoặc **hành động nghiệp vụ** |
- **Idempotent ≠ safe**: DELETE idempotent nhưng không safe. Idempotent là về **trạng thái server**, không phải response giống nhau.
- **Hành động nghiệp vụ** (chuyển trạng thái có luật) → endpoint hành động: `POST /quotes/{id}/finalize`, `POST /orders/{id}/cancel` (body có lý do). Lý do: không chỉ đổi một field, có kiểm tra luật, audit, side effect. `PATCH /orders/{id} { "status": "Cancelled" }` cho phép client đặt trạng thái tuỳ ý → khó kiểm soát luật chuyển trạng thái.

### B4.2 Status code — chọn đúng và nhất quán
| Code | Khi nào | Ví dụ Ops Hub |
|---|---|---|
| **200 OK** | Thành công có body | GET quote |
| **201 Created** + `Location` | Tạo mới | `POST /orders` → `Location: /orders/981` |
| **202 Accepted** | Nhận việc, xử lý nền | Sinh PDF hợp đồng → `Location: /jobs/77` |
| **204 No Content** | Thành công không body | DELETE |
| **400** | Request sai định dạng/validation | Thiếu `customerName` |
| **401** | **Chưa xác thực** (không có/sai token) | Token hết hạn |
| **403** | Đã xác thực nhưng **không có quyền** | Sales xem báo cáo lợi nhuận |
| **404** | Không tồn tại (hoặc **giấu** resource của tenant khác) | Order của công ty khác → 404 thay vì 403 để không lộ sự tồn tại |
| **409 Conflict** | Xung đột trạng thái/trùng | Finalize quote đã finalize; xe hết chỗ |
| **412 Precondition Failed** | `If-Match` không khớp ETag | Người khác đã sửa đơn |
| **422** | Đúng định dạng nhưng vi phạm luật nghiệp vụ (tuỳ quy ước team) | Deposit lớn hơn tổng đơn |
| **429** + `Retry-After` | Vượt rate limit | |
| **500** | Lỗi không mong đợi | |
| **503** + `Retry-After` | Tạm không phục vụ | Bảo trì, dependency sập |
- **Lỗi** theo **ProblemDetails (RFC 9457)**: `type, title, status, detail, instance` + `errorCode` ổn định (`quote.already_finalized`) để FE xử lý + `traceId`; validation có `errors: { "customerName": ["Required"] }` để React map vào field.
- **Callback/webhook của provider** (Pragmatic, payment): trả theo **spec của provider** (thường 200 + mã lỗi riêng), không theo quy ước REST của mình.

### B4.3 Idempotency-Key cho POST (chống tạo trùng khi retry)
Tình huống: app gửi `POST /orders`, mạng đứt trước khi nhận response → client **không biết** order đã tạo chưa → retry → **2 order**.
Giải pháp (kiểu Stripe):
1. Client sinh **UUID** cho mỗi ý định ("tạo order từ quote 42"), gửi header `Idempotency-Key`. Retry dùng **lại cùng key**.
2. Server: bảng `IdempotencyKeys(Key, UserId, RequestHash, Status, ResponseCode, ResponseBody, CreatedAt)` với **UNIQUE(Key, UserId)**.
3. Xử lý: **INSERT key trước** (trạng thái `InProgress`) **trong cùng transaction** với việc tạo order (hoặc trước, nếu xử lý dài).
   - Trùng key + body giống → **trả lại đúng response lần đầu** (replay), không báo lỗi.
   - Trùng key + body khác → **422** (dùng sai key).
   - Trùng key đang `InProgress` → **409** (đang xử lý, thử lại sau).
4. Giữ key ~24 giờ (API client). Với **ledger tiền** thì transaction id giữ **vĩnh viễn**.
- Với "tạo order từ quote" còn có khoá tự nhiên: **UNIQUE(Orders.QuoteId)** → không cần header vẫn chặn được trùng.

### B4.4 Concurrency: ETag / If-Match (optimistic qua HTTP)
- `GET /orders/42` → response header `ETag: "AAAAAAAAB9E="` (từ `rowversion`).
- `PUT /orders/42` gửi `If-Match: "AAAAAAAAB9E="` → server `UPDATE ... WHERE RowVersion = @etag` → 0 dòng → **412 Precondition Failed** → UI: "Đơn đã bị người khác sửa", tải bản mới, cho so sánh.
- Không có cơ chế này → **lost update** giữa hai nhân viên (người lưu sau đè người lưu trước).

### B4.5 Pagination, filter, sort
- **Offset** `?page=500&size=20` → `OFFSET 9980 ROWS FETCH NEXT 20` → DB vẫn phải **duyệt bỏ 9.980 dòng** → càng sâu càng chậm; có dòng mới chèn → **trùng/sót** giữa các trang. Hợp: màn hình admin cần nhảy trang, dữ liệu nhỏ.
- **Keyset/cursor** `?after=eyJjIjoiMjAyNi0xMC0yOVQxMDowMCIsImlkIjo5ODF9`:
```sql
SELECT TOP (20) Id, CreatedAt, Total FROM Orders
WHERE StoreId = @s AND (CreatedAt < @c OR (CreatedAt = @c AND Id < @id))
ORDER BY CreatedAt DESC, Id DESC;          -- index (StoreId, CreatedAt DESC, Id DESC)
```
  Luôn nhanh (seek rồi đọc 20 dòng), không trùng/sót; sort phải **xác định** (thêm `Id` làm tie-breaker); cursor **opaque** (base64) để đổi cách cài đặt sau. Không nhảy trang tuỳ ý được.
- Tránh `COUNT(*)` mỗi trang trên bảng lớn (trả `hasMore` hoặc count ước lượng).
- Filter/sort: `GET /orders?status=InProduction&storeId=12&sort=-createdAt`; **whitelist** field được sort/filter (không đưa thẳng tên cột vào SQL); giới hạn `size` tối đa (vd. 100).

### B4.6 Versioning và breaking change
- **Breaking**: xoá/đổi tên field, đổi kiểu, thêm field **bắt buộc** ở request, đổi ý nghĩa field/status code, **thêm giá trị enum** mà client cũ không xử lý (tuỳ client).
- **Non-breaking**: thêm field optional, thêm field ở response, thêm endpoint. Client phải là **tolerant reader** (bỏ qua field lạ).
- Cách version: URL `/v1/` (dễ thấy, dễ route, dễ cache — hợp public API, mobile app không ép cập nhật được), header/media type (URL gọn, khó debug). .NET: `Asp.Versioning`.
- Deprecation: header `Deprecation`/`Sunset`, đo traffic theo version, báo trước, chỉ tắt khi traffic về 0.

### B4.7 Việc chậm, file, realtime
- Việc > vài giây (sinh PDF, gọi RTO provider): `202 Accepted` + `Location: /jobs/{id}` → client poll `GET /jobs/{id}` hoặc nhận push (SignalR/WebSocket/webhook).
- Upload/download file lớn: **presigned URL S3** — API chỉ kiểm quyền và cấp URL ngắn hạn; file đi thẳng client ↔ S3, không qua app.

### B4.8 Hợp đồng FE–BE
- **OpenAPI** là hợp đồng (Swashbuckle/NSwag sinh từ code, hoặc viết spec trước — design-first), sinh **TypeScript types/client** (openapi-typescript, NSwag) → FE và BE không lệch nhau. Contract test (Pact) khi nhiều client.

### B4.9 Thiết kế mẫu: finalize quote → tạo order
```
POST /quotes/42/finalize
  → 200 { id, status: "Finalized", total, taxRate, expiresAt, etag }
  → 409 { errorCode: "quote.already_finalized" } | 422 { errorCode: "quote.expired" }

POST /orders            Idempotency-Key: 3f2c...
  body { quoteId: 42, saleType: "RTO" | "Cash", depositAmount }
  → 201 Location: /orders/981   (lines copy từ snapshot của quote đã finalize)
  → 409 { errorCode: "order.exists_for_quote", orderId: 981 }   (UNIQUE QuoteId)
  → 422 { errorCode: "order.deposit_exceeds_total" }

POST /orders/981/cancel   body { reason }   If-Match: "..."
  → 200 | 409 order.cannot_cancel (đã giao) | 412 (đã bị sửa)
```

### B4.10 Bảo mật API
- HTTPS; xác thực (cookie hoặc bearer, C1); **authorization theo resource** mỗi lần (order thuộc tenant/store của user?) — thiếu là **BOLA/IDOR**, lỗi số 1 OWASP API; rate limit; validate input; giới hạn kích thước request; không lộ id tuần tự nhạy cảm; không trả entity (lộ field).

### B4.11 Bẫy hay sai
- POST trả 200 không có `Location`; 401 và 403 lẫn lộn.
- Trả lỗi khi request trùng thay vì replay.
- Idempotency "kiểm tra key rồi mới insert" (check-then-act) thay vì UNIQUE.
- Offset cho infinite scroll bảng lớn; sort không có tie-breaker.
- `PATCH status` cho mọi chuyển trạng thái.

### B4.12 Câu hỏi phỏng vấn & trả lời mẫu

**Q1. Design the API to finalize a quote and convert it to an order.**
> Finalizing is a business transition, so it's `POST /quotes/{id}/finalize`: it validates the quote, snapshots prices and tax, and returns 200 with the new state, 409 if it's already finalized or 422 if it's expired. Creating the order is `POST /orders` with the quote ID and an Idempotency-Key header; it copies lines from the finalized snapshot and returns 201 with a Location header. A unique constraint on the quote ID in the orders table guarantees one order per quote, so a retry or double click gets 409 with the existing order ID — or the replayed 201 if it's the same idempotency key. Errors are ProblemDetails with stable error codes the React app can switch on.

**Q2. What does idempotent mean? Which methods are idempotent?**
> Calling it once or many times leaves the server in the same state. GET, PUT and DELETE are idempotent by definition; POST and PATCH aren't. Idempotent isn't the same as safe — DELETE changes state but repeating it doesn't change it further. For POSTs that move money or create orders, I make them idempotent with a client-generated key stored under a unique constraint, and replay the original response on a retry.

**Q3. Two staff edit the same order at the same time. What does the API do?**
> Each GET returns an ETag from the row version; the update sends it back in If-Match, and the UPDATE includes it in the WHERE clause. If someone saved in between, zero rows are affected and we return 412. The UI then reloads the order and shows what changed, so nobody silently overwrites someone else's work.

**Q4. Offset or cursor pagination?**
> Offset is simple and allows jumping to page 37, but the database still walks past every skipped row, so deep pages get slower, and inserts shift rows so users see duplicates or miss items. Keyset pagination filters on the last seen sort key plus the ID as a tie-breaker, so every page is an index seek and stable under inserts, at the cost of no random page jumps. I'd use offset for small admin lists and keyset for large or infinite-scroll lists like order history.

**Q5. How do you version an API used by a mobile app?**
> I avoid breaking changes as long as possible: add optional fields, never remove or repurpose them, and clients ignore unknown fields. When a breaking change is unavoidable, I add `/v2` alongside `/v1`, mark v1 with Deprecation and Sunset headers, measure traffic per version, and only remove v1 when usage is gone — mobile users don't all update, so the old version can live for months.

**Q6. An operation takes 10 seconds. How do you design the API?**
> I don't hold the request open. The POST validates, enqueues the work and returns 202 Accepted with a Location to a job resource; the client polls it or gets a SignalR push when it's done, and the job result links to the output, like a presigned URL for the generated PDF. The job is idempotent so a retry of the POST doesn't generate it twice.

**Q7. `PATCH /orders/{id} {status}` or `POST /orders/{id}/cancel`?**
> For lifecycle transitions I prefer the explicit action. Cancelling has rules — not after delivery, a reason, maybe a fee — plus audit and side effects like freeing a delivery slot. An action endpoint makes those rules explicit and lets authorization differ per action. PATCH is fine for plain field edits like notes or a phone number.

### B4.13 Tự kiểm tra
1. 401 vs 403; 409 vs 412 vs 422 — mỗi cái một ví dụ Ops Hub.
2. Mô tả luồng Idempotency-Key khi: trùng key cùng body, khác body, đang xử lý.
3. Viết câu SQL keyset cho danh sách payment theo `PaidAt DESC`.
4. Liệt kê 4 breaking change.
5. Vì sao trả 404 thay vì 403 khi truy cập order của tenant khác?

---

## B5. OOP, SOLID, layering, kiến trúc tổng thể ⏳

> ⏳ **Chưa viết lại sâu.** Dưới đây là nội dung bản cũ (số tham chiếu section bên trong là số bản cũ, xem bảng đối chiếu ở 0.2). Claude sẽ viết lại trước khi Hiệp học tới.

JD nhấn: "clean, testable, well-structured code, solid architectural patterns… stable and scalable as it grows". Đây là đất của SA.

### B5.1 Clean architecture / layering
- **Presentation** (Controller, Razor, API) → **Application** (use case, handler, validation, transaction, gọi port) → **Domain** (entity, value object, luật nghiệp vụ, domain event) ← **Infrastructure** (EF, S3, email, payment, HTTP client). Domain **không** phụ thuộc Infrastructure: interface do tầng nghiệp vụ định nghĩa (`IDocumentStorage`, `ITaxCalculator`), hạ tầng implement (**Dependency Inversion**).
- Controller mỏng: nhận request → gọi handler → map kết quả ra HTTP. Không để logic tính giá trong controller hay Razor view.
- **Vertical slice**: tổ chức theo feature (`Quotes/Finalize`, `Orders/Cancel`) thay vì theo tầng kỹ thuật; mỗi slice có handler, validator, DTO. Không giáo điều: handler được dùng `DbContext` trực tiếp.
- Ví dụ thật: Joblogic Web MVC → message → `IHandler<TMsg, OneOf<TRes, Error>>` → service → EF/Dapper. PlaySweeps: repository bọc stored procedure Dapper, DI bằng Autofac.
- **DTO vs domain model vs persistence model**: DTO là hợp đồng API (ổn định, chỉ field cần), domain model chứa luật, persistence model là cách lưu. Với EF thường gộp domain + persistence, nhưng **không trả entity ra API** (lộ dữ liệu, over-posting, khoá schema, vòng tham chiếu, lazy N+1).

### B5.2 SOLID — một câu mỗi chữ + ví dụ Ops Hub
- **S** (Single Responsibility): `QuotePricingService` chỉ tính giá; `QuotePdfRenderer` chỉ render. Lý do thay đổi khác nhau → class khác nhau.
- **O** (Open/Closed): thêm RTO provider/loại thuế mới bằng class mới implement interface, không sửa `if/else` lớn.
- **L** (Liskov): mọi `IPaymentProvider` trả kết quả cùng ngữ nghĩa; không có provider nào throw `NotSupportedException` cho một method trong interface.
- **I** (Interface Segregation): tách `IQuoteReader` / `IQuoteWriter` thay vì repository khổng lồ 40 method.
- **D** (Dependency Inversion): handler phụ thuộc `TimeProvider`, `ITaxCalculator`, `IDocumentStorage`; không `DateTime.Now`, không `new AmazonS3Client()` → **testable**.

### B5.3 Monolith vs microservices
| | Modular monolith | Microservices |
|---|---|---|
| Transaction | Đơn giản (1 DB) | Phân tán: outbox, saga, eventual consistency |
| Deploy | Một artifact | Độc lập từng service |
| Vận hành | Dễ | Cần observability, service discovery, versioning contract |
| Hợp khi | Team nhỏ–vừa, domain còn thay đổi | Nhiều team, scale khác nhau, ranh giới domain rõ |
Câu mẫu:
> For a system like the Ops Hub I'd start with a well-structured modular monolith rather than microservices: clear modules for Quotes, Orders, Contracts, Production and Delivery, each with its own application layer, and communication through interfaces or in-process events. That keeps transactions simple, which matters when money and contracts are involved. To keep it scalable I'd keep the web tier stateless so it can scale horizontally behind a load balancer, push slow work like PDF generation, emails and third-party sync to background workers through a queue, add read replicas or caching for heavy reports, and watch the database with proper indexes and query monitoring. I'd only split a module into a separate service when there's a real reason, like a different scaling profile or a separate team.
Câu đối chiếu kinh nghiệm: Joblogic có ~30 service (team lớn, sản phẩm lâu năm) — Hiệp đã thấy cả lợi (deploy độc lập, scale theo trigger) lẫn chi phí (contract NuGet chung, message trùng phải idempotent, debug xuyên service cần OperationId).

### B5.4 Scale & sẵn sàng (stable and scalable)
- **Horizontal vs vertical**: vertical = máy to hơn (giới hạn, downtime); horizontal = nhiều instance (cần stateless: session/cache ra Redis, file ra S3).
- **Stateless web tier** + load balancer + health check; **background worker** cho việc chậm; **queue** để san tải; **cache** cho dữ liệu đọc nhiều; **read replica** cho báo cáo; **index + query tuning** trước khi nghĩ shard.
- **Một instance chết**: ≥ 2 instance ở 2 AZ, health check gỡ instance lỗi, graceful shutdown (dừng nhận request, xử lý xong việc dở), job nền idempotent để instance khác chạy lại được.
- **Zero-downtime deploy**: rolling/blue-green + migration expand/contract (section 15, 20).
- **Scalability vs performance vs availability vs reliability**: scalability = chịu tải tăng khi thêm tài nguyên; performance = nhanh với tải hiện tại; availability = % thời gian phục vụ được; reliability = làm đúng, không mất dữ liệu.
- **Eventual consistency**: các bản sao/hệ thống sẽ khớp sau một khoảng thời gian. Ví dụ: read model search, báo cáo, số liệu dashboard. **Không** chấp nhận cho số dư/tiền đã thu.
- **CAP thực tế**: khi mạng phân vùng phải chọn trả lời (có thể sai/cũ) hay từ chối. Với tiền → ưu tiên đúng (consistency); với catalog/hiển thị → ưu tiên sẵn sàng.

### B5.5 Câu hỏi luyện (SA)
1. How would you structure a .NET solution for this product? Where does business logic live?
2. Explain SOLID with examples from your work.
3. Monolith or microservices for the Ops Hub? Why?
4. How do you make the system stable and scalable as it grows?
5. What's the difference between a DTO, a domain model and a persistence model? Should a controller return an EF entity?
6. What is dependency inversion and how does it make code testable?
7. How would you design the system so it survives one instance dying?
8. Where would this architecture break first if traffic grew 10×?
9. What's eventual consistency? Where is it acceptable in the Ops Hub and where isn't it?
10. How would you introduce a big architectural change (e.g. move PDF generation to a worker) into a running production system? → strangler, feature flag, chạy song song, đo, chuyển dần, có đường quay lại.
11. Describe an architecture you'd be comfortable owning in production.
12. When would you choose vertical slices over classic layers?

---

## B6. Design patterns ⏳

> ⏳ **Chưa viết lại sâu.** Dưới đây là nội dung bản cũ (số tham chiếu section bên trong là số bản cũ, xem bảng đối chiếu ở 0.2). Claude sẽ viết lại trước khi Hiệp học tới.

Nguyên tắc: **vấn đề → pattern → ví dụ thật/Ops Hub → trade-off**. Đừng đọc định nghĩa sách.

### B6.1 Bảng pattern
| Pattern | Khi nào | Ví dụ để kể | Trade-off |
|---|---|---|---|
| **Strategy** | Nhiều thuật toán đổi được theo cấu hình | Tính giá theo loại sản phẩm; RTO provider khác nhau tính lịch trả khác nhau; Joblogic selling rate theo khung giờ/holiday | Thêm class; đáng khi có ≥ 2 biến thể thật |
| **State / state machine** | Thực thể có vòng đời, mỗi trạng thái cho phép hành động khác | Quote: Draft → Sent → Accepted/Expired; Order: Confirmed → InProduction → Ready → Scheduled → Delivered / Cancelled | Đơn giản thì enum + bảng chuyển trạng thái là đủ; State class cho khi mỗi trạng thái có nhiều hành vi |
| **Factory / Abstract Factory** | Tạo object phức tạp, chọn implementation lúc chạy | `IRtoProviderFactory.Get(companyId)`; DocGen chọn template tenant → fallback hệ thống | — |
| **Builder** | Tạo object nhiều bước/tham số | Dựng quote/test data (test data builder), `WebApplication.CreateBuilder` | — |
| **Template Method** | Các bước giống nhau, chi tiết khác | Sinh tài liệu: lấy data → chọn template → thay tag → xuất PDF | Kế thừa → cứng; có thể thay bằng composition |
| **Decorator** | Thêm hành vi ngang (log, cache, retry) không sửa class gốc | `CachedTaxRateProvider` bọc `TaxApiClient`; MediatR pipeline behavior (validation, logging); `DelegatingHandler` của HttpClient | Debug nhiều lớp bọc |
| **Adapter / Anti-corruption layer** | Tích hợp hệ ngoài có model khác | Map SKU từ configurator, payment, thuế → model nội bộ; đổi provider chỉ sửa adapter | — |
| **Facade** | Che một hệ phức tạp sau API gọn | `IKycService` che Socure (DocV, SSN, decision) | — |
| **Repository + Unit of Work** | Tách data access; UoW = 1 transaction | `DbContext` đã là UoW + repository; PlaySweeps bọc SP Dapper bằng repository | Generic `IRepository<T>` trên EF thường thừa, che mất sức mạnh LINQ |
| **Specification** | Điều kiện nghiệp vụ tái sử dụng/ghép | "RTO option eligible": giá trị tối thiểu, bang, loại sản phẩm | — |
| **Mediator / CQRS** | Tách command/query, pipeline chung | Joblogic message + handler; Replication sang Azure Search = read model | Mediator là **in-process**, không liên quan độ bền message |
| **Observer / domain event** | Một sự kiện kéo theo nhiều việc | OrderDelivered → SMS/email, cập nhật balance, audit. Joblogic: Notification/Audit subscribe event | Luồng khó lần theo; cần đặt tên event rõ |
| **Outbox** | Ghi DB + gửi message nhất quán | Ghi order + outbox row **cùng transaction**, worker gửi sau | Thêm bảng + worker; consumer phải idempotent |
| **Result type** | Lỗi nghiệp vụ là kết quả bình thường | Joblogic `OneOf<TSuccess, Error>` | Code dài hơn try/catch |
| **Singleton** | Một instance cho cả app | Qua DI (`AddSingleton`), không tự viết static; cẩn thận captive dependency | Static singleton khó test |
| **Options pattern** | Cấu hình có kiểu | `IOptions<TaxSettings>` | — |
| **Circuit breaker / Retry** | Gọi hệ ngoài không ổn định | Polly / `Microsoft.Extensions.Http.Resilience` | Retry không idempotent = nguy hiểm |

### B6.2 Câu mẫu (State)
> An order has a clear lifecycle, so I'd model it as a state machine in the domain: the Order entity exposes methods like `Confirm()`, `StartProduction()`, `ScheduleDelivery(date)`, `Cancel(reason)`, and each one checks the current status and the business rules before changing it. The UI only shows the actions that are allowed, but the rule lives in the domain, so an API call or a background job can't put the order in an invalid state. Every transition writes an audit entry with who, when and why — similar to the contract audit trail I built at Joblogic.

Code minh hoạ:
```csharp
public sealed class Order
{
    public OrderStatus Status { get; private set; }
    private readonly List<OrderEvent> _history = new();

    public Result Cancel(string reason, string userId, DateTimeOffset now)
    {
        if (Status is OrderStatus.Delivered or OrderStatus.Cancelled)
            return Result.Fail("order.cannot_cancel");
        Status = OrderStatus.Cancelled;
        _history.Add(new OrderEvent("Cancelled", reason, userId, now));
        return Result.Ok();
    }
}
```

### B6.3 Câu mẫu (Strategy cho RTO)
> Different rent-to-own providers have different rules for eligibility, terms and payment schedules. I'd define an `IRtoProvider` interface with methods like `CheckEligibility` and `BuildPaymentSchedule`, one implementation per provider, and pick it through a factory based on the company's configuration. Adding a provider then means adding a class and a configuration entry, not editing a large switch statement.

### B6.4 Câu bẫy
- "When would you NOT use a pattern?" > When there's only one way of doing it and no sign it will change. A pattern adds indirection, so I add it when the second case actually appears, not up front.
- "Is Repository over EF Core an anti-pattern?" > With EF Core I usually don't add a generic repository — DbSet already is one and DbContext is a unit of work. I add a specific repository when there's a reason: Dapper and stored procedures, multiple stores, or translating unique-key violations into domain results.
- "Singleton pattern vs singleton lifetime?" → pattern tự quản lý instance (static, khó test); lifetime do DI container quản lý.

### B6.5 Câu hỏi luyện
1. Which design patterns do you use most? Give a real example for each.
2. How would you model the order lifecycle? Which pattern?
3. How would you support several RTO providers with different rules?
4. How would you add caching to a tax-rate client without modifying it? (Decorator)
5. How do you integrate a third-party system whose model doesn't match yours? (Adapter/ACL)
6. Explain CQRS. Is it worth it here?
7. Explain the Outbox pattern. How is it different from a mediator?
8. Repository + Unit of Work with EF Core: yes or no?
9. When does a pattern become over-engineering?
10. Strategy vs State — difference?
11. Factory vs DI container — when do you need a factory?

---

## B7. Clean code và code review ⏳

> ⏳ **Chưa viết lại sâu.** Dưới đây là nội dung bản cũ (số tham chiếu section bên trong là số bản cũ, xem bảng đối chiếu ở 0.2). Claude sẽ viết lại trước khi Hiệp học tới.

SA tự khai "Clean Coding". Có thể được đưa một đoạn code để review trực tiếp.

### B7.1 Clean code — nói được bằng ví dụ
- **Đặt tên** theo nghiệp vụ (`CalculateBalanceDue`, `IsEligibleForRto`), không `Process`, `Helper`, `data2`.
- **Hàm nhỏ, một việc**, ít tham số (gom thành object), không flag bool đổi hành vi (`Save(true)`).
- **Guard clause / early return** thay vì if lồng nhau.
- **Không magic number/string**: hằng số, enum, cấu hình.
- **Không lặp logic** (DRY), nhưng đừng gộp hai thứ chỉ giống nhau bề ngoài (AHA / "rule of three").
- **Bất biến** khi có thể: `record`, `init`, value object `Money`.
- **Xử lý lỗi rõ**: Result cho lỗi nghiệp vụ, exception cho bất ngờ; không `catch {}` nuốt lỗi; log có ngữ cảnh.
- **Comment giải thích "vì sao"**, không giải thích "làm gì".
- **Testable**: DI, không static/`DateTime.Now`, logic thuần ở domain.
- **Boy Scout rule / "1% improvements"**: mỗi lần chạm vào code thì để lại tốt hơn một chút (khớp văn hoá JD).

### B7.2 Checklist review PR (thứ tự nói)
1. **Đúng nghiệp vụ**: có làm đúng acceptance criteria, edge case (tiền, thời gian, null, rỗng, trùng)?
2. **Test**: có test cho luật mới và bug đã sửa không?
3. **Thiết kế**: đúng tầng, không lộ entity, không logic trong controller, đặt tên.
4. **Dữ liệu**: transaction boundary, concurrency, migration tương thích ngược, index cho query mới, N+1.
5. **Bảo mật**: authorization theo resource, validate input, không log dữ liệu nhạy cảm, SQL parameter.
6. **Vận hành**: log/metric, timeout/retry khi gọi ngoài, feature flag, rollback được.
7. **Hiệu năng**: async all the way, không `.Result`, phân trang.
Thái độ: comment cụ thể, đề xuất thay vì ra lệnh, tách "blocking" và "nit", khen chỗ tốt. PlaySweeps: lead feature nào review kỹ feature đó; Joblogic: review với team UK trên Azure DevOps.

### B7.3 Bài review code (từ question bank 133–136) — tập nói to
**133.**
```csharp
public async Task<User> GetUser(int id)
{
    var user = await _db.Users.FirstOrDefaultAsync(x => x.Id == id);
    return user;
}
```
Ý: trả `null` khi không có → controller trả **404**; không trả entity ra API → **project sang DTO** (`Select(u => new UserDto(...))`) — chỉ lấy cột cần, không tracking; nếu chỉ đọc mà không project thì `AsNoTracking()`; truyền `CancellationToken`; kiểm tra quyền xem user này (multi-tenant/ownership); đổi tên `GetUserAsync`; kiểu trả về `User?` (nullable reference).

**134.**
```csharp
public async Task ProcessAsync()
{
    var result = _client.GetAsync("/users").Result;
    Console.WriteLine(result);
}
```
Ý: `.Result` là **sync-over-async** → chiếm 2 thread, có thể **thread-pool starvation** (ASP.NET Core) hoặc deadlock (có SynchronizationContext); method `async` mà không `await`. Sửa: `await _client.GetAsync("/users", ct)`, `EnsureSuccessStatusCode`, `ReadFromJsonAsync`, timeout bằng CancellationToken/`HttpClient.Timeout`, retry có backoff (Polly/resilience handler), log bằng `ILogger` không `Console`. `HttpClient` **không tạo mới mỗi request** (cạn socket) → `IHttpClientFactory`/typed client (cũng xử lý DNS đổi).

**135.**
```csharp
public class OrderService
{
    private readonly DbContext _db;
    public OrderService(DbContext db) { _db = db; }
    public async Task CreateAsync(Order order)
    {
        _db.Add(order);
        await _db.SaveChangesAsync();
    }
}
```
Hỏi trước khi approve: validation và luật nghiệp vụ ở đâu (order nhận từ đâu, có phải entity bind thẳng từ request → over-posting)? Có idempotency chống tạo trùng? Transaction boundary: `SaveChanges` đã là 1 transaction; nếu cần gửi email/gọi ngoài → outbox, không gọi trong transaction. Dùng `DbContext` chung chung → nên inject `AppDbContext` cụ thể. Có cần repository không? Với EF thường **không** (DbSet đã là repository, DbContext là UoW); bọc khi Dapper/nhiều store. Thiếu `CancellationToken`, thiếu trả về id/kết quả, thiếu log/audit. Lớp này đang "anemic": logic nên ở `Order.Create(...)` hoặc handler.

**136.**
```csharp
public class CacheService
{
    private readonly Dictionary<string, object> _cache = new();
    public object Get(string key) => _cache.TryGetValue(key, out var v) ? v : null;
    public void Set(string key, object value) => _cache[key] = value;
}
```
Ý: `Dictionary` **không thread-safe** → đọc/ghi đồng thời có thể hỏng cấu trúc, vòng lặp vô hạn, exception. Không có expiration → dữ liệu cũ + **memory leak** (lớn mãi). Nhiều instance → mỗi instance một cache riêng, lệch nhau. `object` → mất type safety. Không giới hạn kích thước. Sửa: `IMemoryCache` (có expiration, size limit, thread-safe) cho cache cục bộ; **Redis/`IDistributedCache`** (hoặc `HybridCache` .NET 9) khi nhiều instance cần thống nhất; key có tenant; chống stampede (lock theo key / `GetOrCreateAsync`).

**Bài thêm (tự luyện, liên quan nghiệp vụ):**
```csharp
public decimal CalculateBalance(Order o)
{
    double total = 0;
    foreach (var l in o.Lines) total += (double)(l.Price * l.Qty);
    total = total * 1.07;                 // tax
    var paid = _db.Payments.Where(p => p.OrderId == o.Id).ToList().Sum(p => p.Amount);
    return (decimal)Math.Round(total - (double)paid, 2);
}
```
Lỗi cần tìm: `double` cho tiền (sai số) → `decimal`; thuế **hard-code 7%** (thuế phụ thuộc địa chỉ/bang, phải lấy từ snapshot của order); `ToList()` trước `Sum` → kéo hết về RAM (dùng `SumAsync` ở DB); query sync trong code lẽ ra async; không trừ refund; làm tròn mặc định là **banker's rounding** (`MidpointRounding.ToEven`) — cần quy tắc rõ; logic tính tiền nằm trong service truy cập DB trực tiếp → khó test, nên tách hàm thuần nhận dữ liệu.

### B7.4 Câu hỏi luyện
1. What does clean code mean to you? Give an example of code you cleaned up.
2. What do you look for when reviewing a pull request?
3. How do you give feedback on a PR from a more senior colleague / from the US partner?
4. How do you handle disagreement in code review?
5. Review this code (các bài trên). What would you change and why?
6. When is duplication better than the wrong abstraction?
7. How do you keep a codebase maintainable over years?
8. What makes code testable?

---

## B8. Unit test, integration test ⏳

> ⏳ **Chưa viết lại sâu.** Dưới đây là nội dung bản cũ (số tham chiếu section bên trong là số bản cũ, xem bảng đối chiếu ở 0.2). Claude sẽ viết lại trước khi Hiệp học tới.

Bằng chứng: PlaySweeps ~200 file test **xUnit + Moq**; Joblogic **MSTest + AutoFixture + AutoMocker** (test audit handler, selling rate, SchedulerController); EIM **Jest** (~3 file — nói ít). Nói đúng tên framework từng nơi.

### B8.1 Kiến thức
- **Unit test**: test một đơn vị logic, cô lập, nhanh, không I/O. **Integration test**: nhiều thành phần thật (DB, HTTP pipeline). **E2E**: qua UI/hệ thống thật.
- **Test pyramid**: nhiều unit (domain, tính tiền, state machine, ngày giờ) → ít integration (`WebApplicationFactory` + DB thật bằng **Testcontainers**) → rất ít E2E (Playwright).
- **Test tốt (FIRST)**: Fast, Independent, Repeatable, Self-validating, Timely. Một hành vi mỗi test; tên `Method_Scenario_ExpectedResult`; Arrange–Act–Assert; không logic phức tạp trong test.
- **Test double**: dummy, stub (trả dữ liệu cố định), fake (implement đơn giản, vd. in-memory), mock (kiểm tra được gọi thế nào), spy.
- **Mock gì**: phụ thuộc ngoài (HTTP, email, clock, queue, payment). **Không mock**: domain object, value object; **không mock `DbContext`/`IQueryable`** để test query (dùng DB thật); EF InMemory provider không giống SQL thật (không transaction, không constraint) → SQLite in-memory hoặc Testcontainers.
- **Thời gian**: `TimeProvider` + `FakeTimeProvider` (.NET 8).
- **Test data builder** / AutoFixture để tạo object; tránh fixture dùng chung bị sửa.
- **Parameterized**: xUnit `[Theory]` + `[InlineData]`/`[MemberData]`; MSTest `[DataRow]`; NUnit `[TestCase]`.
- **Assertion**: FluentAssertions (chú ý license v8) hoặc Shouldly.
- **Test legacy**: characterization test trước, tạo seam, rồi refactor.
- **Coverage**: chỉ là chỉ số phụ; quan trọng là luật nghiệp vụ rủi ro có test. Mutation testing (Stryker) để đo chất lượng test.
- **TDD** (Red–Green–Refactor): dùng khi luật rõ (tính tiền, lịch trả góp).
- **Contract test** cho API giữa FE–BE/partner (Pact) — biết khái niệm.
- **Flaky test**: do thời gian, thứ tự, dữ liệu dùng chung, mạng → cô lập, fake clock, dữ liệu riêng mỗi test.
- Test trong CI: chạy mỗi PR, chặn merge khi fail.

### B8.2 Ví dụ
```csharp
public class BalanceDueTests
{
    [Theory]
    [InlineData(1000.00, 200.00, 0.00, 800.00)]
    [InlineData(1000.00, 1000.00, 0.00, 0.00)]
    [InlineData(1000.00, 1100.00, 100.00, 0.00)] // overpaid then refunded
    public void BalanceDue_NetsPaymentsAndRefunds(decimal total, decimal paid, decimal refunded, decimal expected)
    {
        var order = OrderBuilder.WithTotal(total).Paid(paid).Refunded(refunded).Build();
        order.BalanceDue.Should().Be(expected);
    }

    [Fact]
    public void RtoSchedule_LastInstallmentAbsorbsRounding()
    {
        var schedule = RtoSchedule.Create(total: 1000m, months: 3);
        schedule.Installments.Sum(i => i.Amount).Should().Be(1000m);
        schedule.Installments.Last().Amount.Should().Be(333.34m);
    }
}
```
Integration test API:
```csharp
public class QuotesApiTests(ApiFactory factory) : IClassFixture<ApiFactory>
{
    [Fact]
    public async Task Finalize_Twice_ReturnsConflict()
    {
        var client = factory.CreateClient();
        var id = await factory.SeedDraftQuoteAsync();
        (await client.PostAsync($"/quotes/{id}/finalize", null)).StatusCode.Should().Be(HttpStatusCode.OK);
        (await client.PostAsync($"/quotes/{id}/finalize", null)).StatusCode.Should().Be(HttpStatusCode.Conflict);
    }
}
```

### B8.3 Câu mẫu
> I focus unit tests on business rules where bugs cost money — pricing, balance due, state transitions, date calculations — because those are pure logic and fast to test. For data access and integrations I prefer a few integration tests against a real database rather than mocking EF, since mocked queries give false confidence. At PlaySweeps I wrote unit tests with xUnit and Moq, around two hundred test files across the features I worked on; at Joblogic the team used MSTest with AutoFixture.

### B8.4 Câu hỏi luyện
1. What makes a good unit test?
2. Unit vs integration test? What does your test pyramid look like?
3. What do you mock and what don't you mock?
4. Should you mock DbContext? Is the EF InMemory provider good for tests?
5. How do you test code that depends on the current time?
6. How do you add tests to legacy code with no tests?
7. How do you test a payment webhook handler?
8. What's TDD? Do you use it?
9. Is 100% coverage a good goal?
10. How do you deal with flaky tests?
11. What would you unit test in the quote → order flow?

---

## B9. Frontend (React/TS) và hợp đồng FE–BE ⏳

> ⏳ **Chưa viết lại sâu.** Dưới đây là nội dung bản cũ (số tham chiếu section bên trong là số bản cũ, xem bảng đối chiếu ở 0.2). Claude sẽ viết lại trước khi Hiệp học tới.

SA **gốc frontend**: React, TypeScript, HTML5, CSS, UX/UI, Front-end (pass LinkedIn assessment). JD: frontend là điểm cộng. Hiệp có thật: PlaySweeps React 18 + Redux (~340 commit), EIM React + TanStack Query + Ant Design, Altar React 18 + Redux, admin Vue 3 + Pinia, Joblogic Razor + jQuery + Vue nhúng, Next.js storefront.
**Thái độ:** không nói "frontend chỉ là phụ"; thể hiện nghĩ cho người dùng cuối.

### B9.1 JavaScript / TypeScript
- `let`/`const` vs `var` (block scope vs function scope, hoisting); `==` vs `===`; closure; `this`; arrow function.
- **Event loop**: call stack, microtask (Promise) chạy trước macrotask (setTimeout); JS đơn luồng. So với .NET: Node dùng event loop + libuv; .NET dùng thread pool + async I/O — cả hai đều không chặn khi chờ I/O.
- Promise, `async/await`, `Promise.all` vs `allSettled`; xử lý lỗi `try/catch`.
- TypeScript: `interface` vs `type`, union, generic, `unknown` vs `any`, `strict` mode, utility types (`Partial`, `Pick`, `Omit`, `Record`), type narrowing, discriminated union (hợp với ProblemDetails/Result).
- Module ES, bundler (Vite, webpack), tree shaking.

### B9.2 React
- Component, props, state; **hooks**: `useState`, `useEffect` (dependency array, cleanup), `useMemo`, `useCallback`, `useRef`, `useContext`, custom hook.
- Re-render khi state/props đổi; `key` trong list (không dùng index khi list đổi thứ tự); `React.memo`.
- **State**: local state → lift state up → Context → Redux/Zustand cho global UI state. **Server state** khác client state → **TanStack Query** (cache, refetch, invalidate sau mutation, retry, stale time). Redux Toolkit/RTK Query.
- **Form**: React Hook Form + Zod/Yup; hiển thị lỗi theo field từ ProblemDetails.
- **Optimistic update** + rollback khi lỗi.
- Performance: code splitting (`React.lazy`), virtualized list (danh sách lớn như production queue), debounce search, tránh re-render thừa.
- React 18: concurrent rendering, automatic batching, `Suspense`. React 19 / Server Components (biết khái niệm), Next.js SSR/SSG.
- Testing: React Testing Library, Jest/Vitest, Playwright cho E2E.

### B9.3 HTML/CSS/UX
- Semantic HTML (`<button>` không phải `<div onClick>`), **accessibility** (label cho input, alt cho ảnh, keyboard navigation, contrast, ARIA khi cần).
- CSS: box model, flexbox, grid, responsive (media query, mobile-first), specificity; CSS modules / Tailwind / styled-components; design system (Ant Design, MUI).
- UX từ góc backend: **loading / empty / error state**, thông báo lỗi dễ hiểu (không hiện stack), xác nhận hành động nguy hiểm (huỷ đơn), **undo** khi có thể, phân trang/infinite scroll, timezone hiển thị theo cửa hàng, định dạng tiền theo locale (`Intl.NumberFormat`), không cho submit 2 lần.

### B9.4 Hợp đồng FE–BE & bảo mật frontend
- OpenAPI → sinh TypeScript types/client (openapi-typescript, NSwag). DTO ổn định, versioning.
- Validation hai phía: FE để UX nhanh, **BE là nguồn sự thật**.
- **Token**: ưu tiên **HttpOnly + Secure + SameSite cookie** (JS không đọc được → giảm rủi ro XSS lấy token) + CSRF protection; localStorage dễ bị XSS đánh cắp. SPA có thể dùng BFF (backend-for-frontend) giữ token phía server.
- **CORS**: chỉ mở origin cần, không `*` khi có credentials. CORS không phải cơ chế bảo mật cho server, chỉ là chính sách trình duyệt.
- XSS: React tự escape; nguy hiểm `dangerouslySetInnerHTML` → sanitize (DOMPurify); CSP header.
- Thao tác chậm: 202 + poll hoặc SignalR/WebSocket push (trạng thái sinh PDF, cập nhật production board realtime).
- File upload lớn: upload thẳng lên S3 bằng presigned URL, backend chỉ cấp URL + xác nhận.

### B9.5 Razor MVC vs React SPA
| | Razor (server render) | React SPA |
|---|---|---|
| Hợp | Form nội bộ, CRUD, ít tương tác, SEO | Màn hình tương tác cao: production board kéo-thả, lịch giao hàng, cấu hình sản phẩm |
| Ưu | Đơn giản, một codebase, auth cookie sẵn | UX mượt, tách FE/BE, tái sử dụng API cho mobile |
| Nhược | Tương tác phức tạp phải thêm JS | Thêm build pipeline, state, bảo mật token, SEO |
| Thực tế | Joblogic dùng Razor + Vue nhúng cho phần tương tác | PlaySweeps, EIM dùng React |

### B9.6 Câu hỏi luyện
1. How do you manage server state vs UI state in React?
2. When does a React component re-render? How do you avoid unnecessary re-renders?
3. `useEffect` — common mistakes?
4. Where do you store the auth token in a SPA and why?
5. What is CORS? Is it a security feature?
6. How do you prevent XSS in React?
7. How would you build a drag-and-drop production queue that two people may edit at once?
8. How do you show validation errors from the API on a form?
9. How would you design the UI/API around a 10-second PDF generation?
10. When would you choose Razor over React?
11. What makes a good error message for users?
12. How do you make a page accessible?
13. JavaScript event loop vs .NET thread pool?
14. TypeScript `interface` vs `type`? `any` vs `unknown`?
15. How would you display dates and money for stores in different time zones?

---

## C1. Authentication: stateful vs stateless, session cookie vs JWT ⏳

> ⏳ **Chưa viết lại sâu.** Nội dung cũ nằm ở C2 mục "AuthN / AuthZ". Sẽ viết lại sâu: stateful vs stateless, session cookie vs JWT, refresh token, revoke, CSRF/XSS.

---

## C2. Security: OWASP, secret, bảo vệ tiền trước người nội bộ ⏳

> ⏳ **Chưa viết lại sâu.** Dưới đây là nội dung bản cũ (số tham chiếu section bên trong là số bản cũ, xem bảng đối chiếu ở 0.2). Claude sẽ viết lại trước khi Hiệp học tới.

### C2.1 OWASP API Top 10 (2023) — nói được 5–6 cái với ví dụ Ops Hub
1. **Broken Object Level Authorization (BOLA/IDOR)**: `GET /orders/123` không kiểm tra order thuộc tenant/store của user → **kiểm tra quyền theo resource** mọi lần, không chỉ đăng nhập. Rủi ro số 1 của SaaS multi-tenant.
2. **Broken Authentication**: token yếu, không hết hạn, không rate limit login → MFA, khoá tạm/exponential backoff (PlaySweeps).
3. **Broken Object Property Level Authorization**: lộ field nhạy cảm trong response / cho sửa field không được phép (over-posting) → DTO riêng.
4. **Unrestricted Resource Consumption**: không giới hạn page size, upload, rate → limit.
5. **Broken Function Level Authorization**: user thường gọi được endpoint admin → policy theo role/permission.
6. **Unrestricted access to sensitive business flows**: bot spam đặt hàng/quote → rate limit, CAPTCHA.
7. **SSRF**: server fetch URL do user gửi (vd. ảnh từ URL) → whitelist.
8. **Security misconfiguration**: CORS `*`, lỗi lộ stack trace, header bảo mật thiếu.
9. **Improper inventory management**: API cũ/không tài liệu vẫn chạy.
10. **Unsafe consumption of APIs**: tin dữ liệu từ bên thứ ba mà không validate.
Thêm (web): **SQL injection** (luôn parameterize; Dapper `@param`; không nối chuỗi), **XSS** (encode output, sanitize rich text, CSP), **CSRF** (anti-forgery token với cookie auth, SameSite).

### C2.2 AuthN / AuthZ
- **Authentication** = bạn là ai; **Authorization** = bạn được làm gì. 401 vs 403.
- **Cookie** (server-side session/ticket, hợp MVC, cần CSRF protection) vs **JWT bearer** (stateless, hợp API/mobile; khó thu hồi → hết hạn ngắn + refresh token xoay vòng; không lưu dữ liệu nhạy cảm trong payload vì chỉ base64).
- **OAuth 2.0** (uỷ quyền) / **OpenID Connect** (đăng nhập, id token); Authorization Code + PKCE cho SPA/mobile.
- ASP.NET Core: `[Authorize]`, **policy-based** (`RequireClaim`, requirement + handler), **resource-based** (`IAuthorizationService.AuthorizeAsync(user, order, "CanEdit")`).
- **RBAC** (role) vs permission chi tiết (Joblogic: permission mapping) vs ABAC (thuộc tính: store, region).
- Multi-tenant: tenant từ claim, không từ request.

### C2.3 Lưu password & dữ liệu nhạy cảm
- Password: **hash chậm có salt** — Argon2id, bcrypt, PBKDF2 (ASP.NET Core Identity `PasswordHasher` dùng PBKDF2). Không MD5/SHA256 thuần, không mã hoá hai chiều.
- Dữ liệu nhạy cảm (SSN, thông tin tín dụng của khách RTO): mã hoá at rest (KMS, TDE, Always Encrypted), in transit (TLS), **không log**, mask khi hiển thị, giới hạn quyền xem, giữ tối thiểu. Thẻ thanh toán → để provider giữ (tokenization), mình không lưu số thẻ (PCI DSS).
- Secret: không trong code/git; Secrets Manager; xoay vòng; secret scanning.

### C2.4 Bảo vệ API khỏi lạm dụng
- Rate limiting theo user/IP/API key/tenant (fixed/sliding window, token bucket) ở gateway hoặc app (.NET `AddRateLimiter`), lưu counter ở Redis khi nhiều instance; trả 429 + `Retry-After`.
- Exponential backoff cho login/OTP (PlaySweeps), CAPTCHA, WAF, giới hạn kích thước request/page size, timeout.

### C2.5 File upload
Kiểm tra loại file (magic bytes, không tin extension), giới hạn kích thước, quét virus, lưu S3 private với tên ngẫu nhiên, không thực thi, presigned URL để tải.

### C2.6 Câu hỏi luyện
1. What are the most common security risks in a backend API? Give examples here.
2. Authentication vs authorization?
3. How do you stop a user from seeing another company's order? (BOLA)
4. Cookie vs JWT? How do you revoke a JWT?
5. How should passwords be stored?
6. How do you prevent SQL injection, XSS and CSRF?
7. How do you protect sensitive customer data (SSN, credit information)?
8. How do you protect a public API from abuse?
9. How do you handle file uploads securely?
10. Where do you store secrets?

---

## C3. Concurrency dữ liệu và idempotency ⏳

> ⏳ **Chưa viết lại sâu.** Dưới đây là nội dung bản cũ (số tham chiếu section bên trong là số bản cũ, xem bảng đối chiếu ở 0.2). Claude sẽ viết lại trước khi Hiệp học tới.

### C3.1 Ý chốt (đây là chỗ Hiệp hay mất điểm)
- **Lost update**: đọc-sửa-ghi trong bộ nhớ app. Chuẩn: **atomic UPDATE** `UPDATE ... SET Qty = Qty - 1 WHERE Id=@id AND Qty >= 1` (kiểm tra rowcount).
- Thứ tự ưu tiên: **atomic UPDATE / UNIQUE constraint → optimistic concurrency (rowversion) → pessimistic lock (UPDLOCK) → distributed lock (Redis)** cuối cùng.
- **Check-then-act** là lỗi: "SELECT xem có chưa, chưa thì INSERT" → hai request cùng qua check. Luôn nói: **"INSERT with a UNIQUE constraint in the same transaction"**; bắt lỗi 2627/2601 → coi là trùng.
- **Idempotency key ≠ concurrency control**: key chống retry của **cùng** yêu cầu; atomic UPDATE chống các yêu cầu **khác nhau** chạy đồng thời.
- Trùng request → **replay response cũ**, không trả lỗi.
- Key chọn đúng độ mịn: transaction reference của provider (không phải roundId); `(playerId, questId, period)` cho thưởng lặp.
- Giữ key: API client ~24h; ledger tiền giữ vĩnh viễn.
- Redis lock không có **fencing token** → process bị dừng lâu vẫn ghi sau khi lock hết hạn → DB phải là trọng tài cuối.
- Double submit trên web: disable nút + PRG (MVC) + Idempotency-Key (API) + UNIQUE ở DB.

### C3.2 Câu mẫu
> The database should decide who wins a race, not application code. For a one-off action like creating an order from a quote, I'd put a unique constraint on the quote ID in the orders table and insert in the same transaction as the rest of the work, so a double click or a retry simply hits the constraint and we return the order that already exists. For updates like stock or capacity, I'd use an atomic conditional UPDATE and check the row count. A distributed lock is my last resort, because it doesn't protect you if a process pauses past the lock's expiry.

### C3.3 Câu hỏi luyện
1. Two requests try to decrement the same inventory at the same time. What happens and how do you fix it?
2. The same webhook arrives twice. How do you make sure the payment is applied once?
3. A background job sometimes processes the same item twice. Why and how do you fix it?
4. The service works with one instance but fails with five. What could be wrong? (in-memory cache/lock/state, scheduled job chạy 5 lần, session cục bộ, file cục bộ)
5. Optimistic vs pessimistic locking — when each?
6. When would you use a distributed lock? What's wrong with Redis locks?
7. Your API receives the same request twice. What do you do?
8. How do you prevent a user from submitting an order twice?

---

## C4. Redis: persistence, sự cố, distributed lock, cache ⏳

> ⏳ **Chưa viết lại sâu.** Nội dung cũ về cache nằm ở C5 mục "Caching" và distributed lock ở C3. Sẽ viết lại sâu: Redis single-thread, persistence RDB/AOF, replication/Sentinel/Cluster, khi Redis chết, RedLock và fencing token, cache stampede.

---

## C5. Messaging, background job, outbox, saga, caching ⏳

> ⏳ **Chưa viết lại sâu.** Dưới đây là nội dung bản cũ (số tham chiếu section bên trong là số bản cũ, xem bảng đối chiếu ở 0.2). Claude sẽ viết lại trước khi Hiệp học tới.

### C5.1 Messaging
- **Vì sao queue**: tách tải (san đỉnh), việc chậm ra khỏi request, retry, tách hệ thống.
- **At-least-once** (phổ biến) → message có thể đến 2 lần → **consumer idempotent**. At-most-once (có thể mất). Exactly-once thực tế = at-least-once + idempotent.
- **DLQ**: message lỗi quá N lần → hàng chờ chết → alert, xem, sửa, đẩy lại.
- **Competing consumers** (nhiều worker chia việc một queue) vs **pub/sub** (mỗi subscriber nhận một bản).
- **Thứ tự**: Service Bus session / SQS FIFO message group theo key (vd. orderId) — một consumer mỗi lúc cho cùng key. SessionId **không** chống trùng.
- **Poison message**: luôn lỗi → DLQ, không retry vô hạn.
- **Transactional Outbox**: ghi dữ liệu nghiệp vụ + bản ghi outbox **trong cùng transaction**; relay đọc outbox gửi đi (at-least-once) → consumer idempotent. Giải quyết "lưu DB xong, gửi message thì crash" (hoặc ngược lại). **Không phải Mediator** (MediatR là in-process).
- **Inbox**: bên nhận lưu message id đã xử lý (UNIQUE) để chống trùng.
- **Saga**: chuỗi transaction cục bộ + **compensation** khi một bước lỗi (orchestration vs choreography). Ví dụ: tạo order → giữ inventory → thu deposit; thu tiền lỗi → nhả inventory, huỷ order.
- **Distributed transaction (2PC)**: tránh trong microservices (khoá lâu, phụ thuộc coordinator) → outbox + saga.
- Thư viện .NET: MassTransit, NServiceBus, Wolverine, Rebus.

### C5.2 Background job trong ASP.NET Core
- `BackgroundService` + `Channel<T>` cho việc nội bộ đơn giản (mất khi restart nếu không bền).
- Bền / định kỳ: **Hangfire**, Quartz.NET, hoặc queue (SQS) + worker, EventBridge Scheduler.
- Mỗi lần xử lý tạo **scope** mới (DbContext Scoped).
- Nhiều instance → job định kỳ chạy N lần → khoá phân tán/leader election hoặc scheduler trung tâm; job **idempotent**.
- Graceful shutdown qua `stoppingToken`.

### C5.3 Caching
- **Vì sao**: giảm latency, giảm tải DB/API ngoài. **Cái giá**: dữ liệu cũ, invalidation khó, bộ nhớ.
- **Cache-aside** (đọc cache → miss thì đọc DB → ghi cache) là phổ biến; write-through; TTL.
- **Cục bộ** `IMemoryCache` (nhanh, mỗi instance riêng) vs **phân tán** Redis/`IDistributedCache` (chung) vs **HybridCache** (.NET 9: L1 + L2 + chống stampede).
- **Cache stampede**: key hết hạn, ngàn request cùng đi DB → lock theo key/single-flight, TTL có jitter, refresh trước hạn.
- **Invalidation**: xoá key khi dữ liệu đổi (event), hoặc TTL ngắn; nhiều instance cục bộ → pub/sub để xoá.
- **Key có tenant** (`tenant:{id}:taxrate:{zip}`).
- **Không cache**: số dư, trạng thái thanh toán cần chính xác; dữ liệu nhạy cảm không mã hoá.
- Cache nên cho Ops Hub: bảng giá/catalog, mức thuế theo zip (TTL), cấu hình tenant, template.
- HTTP caching: `Cache-Control`, ETag/304, CDN cho static.

### C5.4 Câu hỏi luyện
1. Why use a message queue? What problems does it introduce?
2. What's at-least-once delivery? How do you handle duplicates?
3. What's a dead-letter queue? What do you do with messages in it?
4. Explain the Outbox pattern. What problem does it solve?
5. Explain the Saga pattern with an order example.
6. Competing consumers vs pub/sub?
7. How do you keep message ordering per order?
8. How would you implement a background worker in ASP.NET Core?
9. A scheduled job runs on every instance. How do you make it run once?
10. How would you cache data in a multi-instance API?
11. What's a cache stampede and how do you prevent it?
12. What would you cache in the Ops Hub, and what would you never cache?

---

## C6. Scale và load balancer ⏳

> ⏳ **Chưa viết lại sâu.** Nội dung cũ nằm ở B5 mục "Scale & sẵn sàng". Sẽ viết lại sâu: L4/L7, các thuật toán phân phối (round robin, weighted, least connections, least response time, IP hash, consistent hashing), sticky session, health check, connection draining, CAP.

---

## C7. SQL vs NoSQL ⏳

> ⏳ **Chưa viết lại sâu.** Chưa có nội dung cũ. Sẽ viết: mô hình dữ liệu document vs quan hệ, ACID vs BASE, khi nào MongoDB/Cosmos DB, khi nào SQL, ví dụ PlaySweeps (Cosmos DB cho quest state), Joblogic (MongoDB cho audit).

---

## C8. Tích hợp bên thứ ba và resilience ⏳

> ⏳ **Chưa viết lại sâu.** Dưới đây là nội dung bản cũ (số tham chiếu section bên trong là số bản cũ, xem bảng đối chiếu ở 0.2). Claude sẽ viết lại trước khi Hiệp học tới.

Ops Hub có nhiều tích hợp (payment, thuế, RTO provider, configurator, SMS/email). SA từ Urbanise (tích hợp ngân hàng) có thể hỏi.

### C8.1 Webhook vào
1. **Xác thực chữ ký** (HMAC, so sánh constant-time, kiểm timestamp chống replay) — giống Pragmatic hash.
2. **Lưu raw event** (bảng inbox, UNIQUE event id).
3. **Trả 2xx nhanh** (provider có timeout ngắn, sẽ retry).
4. Xử lý **async** (queue), **idempotent** theo event id; xử lý được **sai thứ tự** (kiểm tra version/timestamp, trạng thái hiện tại).
5. Màn hình/bảng **integration errors** để vận hành xem và retry tay (mapping SKU sai…).
6. Job **đối soát** định kỳ với API provider (Joblogic: đối soát Stripe hằng ngày) để bắt event bị mất.

### C8.2 Gọi ra ngoài
- **Timeout** cho mọi lời gọi (mặc định HttpClient 100s là quá dài).
- **Retry** có exponential backoff + jitter, **chỉ cho lỗi tạm thời** (5xx, 408, 429, timeout) và **chỉ khi thao tác idempotent** (hoặc có idempotency key của provider).
- **Circuit breaker**: lỗi liên tục → mở mạch, fail nhanh, thử lại sau → bảo vệ hệ thống mình và provider.
- **Bulkhead**: giới hạn số lời gọi đồng thời tới một provider để không ăn hết thread/connection.
- **Fallback / graceful degradation**: API thuế sập → dùng mức thuế cache gần nhất và đánh dấu "cần xác nhận"; RTO provider sập → lưu yêu cầu "pending", xử lý lại sau, báo người dùng.
- .NET: `IHttpClientFactory` + `Microsoft.Extensions.Http.Resilience` (`AddStandardResilienceHandler`) / Polly v8.
- **Anti-corruption layer**: adapter dịch model ngoài → model nội bộ; lỗi provider → lỗi nghiệp vụ rõ.
- Log + correlation id + metric theo provider (latency, error rate).
- Rate limit của provider → hàng đợi, batch.
- Secret của provider ở Secrets Manager, xoay vòng.

### C8.3 Câu mẫu
> For outgoing calls I always set a timeout, retry only transient errors with exponential backoff and jitter, and only when the operation is idempotent or I can pass the provider an idempotency key. A circuit breaker stops us from hammering a provider that's down. For the user, the request isn't lost: we save it as pending and process it when the provider recovers. For incoming webhooks, I verify the signature, store the raw event with a unique event ID, return 200 quickly and process it asynchronously, so a retried or out-of-order webhook can't apply a payment twice.

### C8.4 Câu hỏi luyện
1. The RTO provider API is down for 30 minutes during business hours. What does the user see? What happens to pending requests?
2. An external API is occasionally slow. How do you protect your system?
3. Explain retry, timeout, circuit breaker and bulkhead.
4. Why must every external HTTP call have a timeout?
5. When is retrying dangerous?
6. How do you receive webhooks reliably? What if they arrive out of order?
7. How do you know if you missed a webhook?
8. How do you integrate a provider whose data model doesn't match yours?
9. How do you test an integration with a third-party API?
10. What is graceful degradation? Give an example here.

---

## C9. Observability và chẩn đoán request chậm ⏳

> ⏳ **Chưa viết lại sâu.** Dưới đây là nội dung bản cũ (số tham chiếu section bên trong là số bản cũ, xem bảng đối chiếu ở 0.2). Claude sẽ viết lại trước khi Hiệp học tới.

### C9.1 Ba trụ cột
- **Logs**: sự kiện rời rạc, structured (JSON, template `{OrderId}`), có correlation/trace id, tenant id, user id; **không log** secret/PII. Mức: Debug/Info/Warning/Error/Critical.
- **Metrics**: số liệu tổng hợp theo thời gian (request rate, error rate, latency p50/p95/p99, queue length, CPU, memory, thread pool). **RED** (Rate, Errors, Duration) cho service; **USE** (Utilization, Saturation, Errors) cho tài nguyên.
- **Traces**: đường đi của một request qua nhiều service (span); W3C `traceparent`; **OpenTelemetry**.
- Công cụ đã dùng: **Application Insights, Grafana Loki, Splunk** (PlaySweeps); AWS: CloudWatch + X-Ray.
- **Alert** theo triệu chứng người dùng (error rate, latency SLO), không theo mọi thứ; runbook đi kèm.
- **SLI/SLO/SLA**: chỉ số / mục tiêu nội bộ / cam kết hợp đồng.

### C9.2 Quy trình điều tra sự cố (nói theo khung)
1. **Tác động**: ai bị, bao nhiêu, từ khi nào (dashboard, alert). Có cần giảm tác động ngay (rollback, tắt feature flag, scale)?
2. **Thay đổi gần đây**: deploy, config, migration, traffic, provider.
3. **Khoanh vùng**: endpoint nào, tenant nào, instance nào; trace một request chậm.
4. **Xác nhận nguyên nhân** bằng dữ liệu (log, metric, query plan, dump).
5. **Xử lý tạm** → **xử lý gốc** → **phòng ngừa** (test, alert, runbook) → postmortem không đổ lỗi.

### C9.3 Tình huống kinh điển
| Tình huống | Hướng điều tra |
|---|---|
| API đột nhiên chậm | Trace → thời gian ở DB/HTTP ngoài/app? DB: Query Store, blocking, plan đổi (parameter sniffing), statistics; app: thread pool starvation (`dotnet-counters`), GC; ngoài: latency provider |
| Prod 10s, local 500ms | Khối lượng dữ liệu khác (index, plan), mạng (DB khác region), cấu hình (log level, pool), tải đồng thời, cold start, provider thật chậm |
| CPU cao | `dotnet-counters` → `dotnet-trace` (flame graph): vòng lặp nóng, regex, serialize lớn, GC nhiều (cấp phát nhiều), lock contention |
| Memory tăng mãi | `dotnet-counters` (gc-heap-size, gen2) → `dotnet-gcdump`/`dotnet-dump` so 2 thời điểm: cache không giới hạn, static list, event handler, captive DbContext |
| Latency cao, CPU thấp | **Thread-pool starvation** (`.Result`) hoặc chờ I/O/lock/connection pool |
| Lỗi chỉ ở một tenant | Dữ liệu đặc biệt, cấu hình tenant, dữ liệu lớn (noisy neighbor) |
| Không tái hiện local | Log/trace theo correlation id, dựng lại hành trình (PlaySweeps: Splunk BI event), dữ liệu prod (ẩn danh), feature flag/cấu hình khác |
| Trả về bản ghi trùng | JOIN nhân dòng, phân trang offset không ổn định (sort không xác định), retry tạo trùng (thiếu UNIQUE) |

### C9.4 Performance
- Đo trước khi tối ưu (BenchmarkDotNet cho code, load test k6/JMeter cho API).
- Thứ tự hay gặp: query/index → N+1 → payload lớn (projection, phân trang, nén) → cache → async/parallel hợp lý → scale.
- Response compression, `AsNoTracking`, keyset pagination, tránh `ToList()` sớm, stream file lớn.

### C9.5 Câu hỏi luyện
1. What should a backend service log? What should it never log?
2. Logs vs metrics vs traces?
3. An API suddenly becomes slow. Walk me through your investigation.
4. An endpoint takes 10 s in production but 500 ms locally. Why?
5. CPU is high on a .NET service. What do you check?
6. Memory keeps growing. How do you find the leak?
7. How would you make the Ops Hub observable enough to debug an incident?
8. Tell me about an incident you handled on call.
9. What do you alert on?

---

## C10. CI/CD, deploy an toàn, build .NET nhanh hơn ⏳

> ⏳ **Chưa viết lại sâu.** Dưới đây là nội dung bản cũ (số tham chiếu section bên trong là số bản cũ, xem bảng đối chiếu ở 0.2). Claude sẽ viết lại trước khi Hiệp học tới.

SA tự khai **CI/CD** ở vai trò hiện tại. Kinh nghiệm thật của Hiệp: làm việc **trong** pipeline do DevOps sở hữu; từng **sửa config Jenkins/Helm values**; Joblogic dùng Azure DevOps (PR, nhánh uat) + Sonar. **Không** nhận đã dựng pipeline. (Nếu Hiệp từng tự viết YAML pipeline nào, bổ sung vào đây.)

### C10.1 Khái niệm
- **CI** (Continuous Integration): merge thường xuyên vào nhánh chính, mỗi lần build + test tự động.
- **Continuous Delivery**: luôn ở trạng thái deploy được, bước lên prod bấm tay. **Continuous Deployment**: tự động lên prod khi pass.
- **Artifact**: build **một lần**, promote cùng artifact qua môi trường (dev → staging → prod), không build lại.
- **Environment config** tách khỏi artifact (12-factor): biến môi trường, Secrets Manager/Parameter Store.

### C10.2 Pipeline chuẩn cho .NET trên AWS
1. **PR build**: `dotnet restore` → `dotnet build -c Release` → `dotnet test` (unit + integration với Testcontainers) → `dotnet format --verify-no-changes`, analyzer (warning as error), scan dependency (`dotnet list package --vulnerable`), SonarQube/SAST; **bắt buộc pass mới merge** (branch protection, required review).
2. **Main build**: build Docker image (multi-stage, image runtime nhỏ), tag theo **commit SHA**, đẩy lên **ECR**; tạo migration bundle (`dotnet ef migrations bundle`) hoặc script idempotent.
3. **Deploy dev/staging** tự động: chạy migration (expand) → deploy app (ECS Fargate/Elastic Beanstalk/App Runner) → smoke test.
4. **Deploy prod** (duyệt tay hoặc tự động): migration → rolling hoặc **blue/green** (ECS + CodeDeploy) có health check → theo dõi error rate/latency (CloudWatch alarm) → tự rollback nếu alarm.
5. **Sau deploy**: smoke test, dashboard, thông báo Slack.
- Công cụ: GitHub Actions, AWS CodePipeline/CodeBuild/CodeDeploy, Azure DevOps, Jenkins, GitLab CI — nguyên lý như nhau. IaC: Terraform, AWS CDK, CloudFormation.

Ví dụ GitHub Actions rút gọn (để hiểu cấu trúc, không nói là đã từng viết):
```yaml
on:
  pull_request:
  push: { branches: [main] }
jobs:
  build-test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: actions/setup-dotnet@v4
        with: { dotnet-version: '8.0.x' }
      - run: dotnet restore
      - run: dotnet build -c Release --no-restore
      - run: dotnet test -c Release --no-build
  deploy:
    if: github.ref == 'refs/heads/main'
    needs: build-test
    runs-on: ubuntu-latest
    environment: staging
    steps:
      - run: echo "build image, push to ECR, run migration bundle, update ECS service"
```

### C10.3 Chiến lược phát hành & rollback
- **Rolling**: thay dần instance; bản cũ và mới chạy song song → API + DB phải tương thích ngược.
- **Blue/green**: dựng môi trường mới, chuyển traffic một lần, rollback = chuyển lại.
- **Canary**: chuyển % nhỏ traffic, đo, tăng dần.
- **Feature flag**: deploy code tắt, bật dần theo tenant/user; **tách deploy khỏi release**; rollback = tắt flag. Dọn flag cũ.
- **Rollback có migration**: nhờ **expand/contract**, rollback app không cần rollback DB (schema mới vẫn tương thích bản cũ). Không viết migration phá huỷ (drop cột) cùng release dùng nó.
- **Hotfix**: nhánh hotfix từ tag prod hoặc fix trên main + cherry-pick; vẫn đi qua pipeline (nhanh hơn, không bỏ test).
- **Zero-downtime**: graceful shutdown (xử lý xong request đang chạy, `stoppingToken`), readiness probe, connection draining ở load balancer.

### C10.4 Chất lượng trong pipeline
- Unit + integration test, coverage gate hợp lý, static analysis, secret scanning, dependency scanning, container image scanning (ECR scan).
- Code review bắt buộc, branch protection.
- DORA metrics: deployment frequency, lead time for changes, change failure rate, time to restore.

### C10.5 Câu trả lời trung thực mẫu
> I haven't owned a pipeline end to end; in my previous teams DevOps owned it and I worked inside it: I've edited Jenkins and Helm configuration for my services, and I own the parts a developer should — tests that run in the pipeline, backward-compatible migrations, feature flags, and checking metrics after a release. If I set one up for the Ops Hub, I'd build one image per commit, promote the same image through environments, run migrations as a separate expand/contract step, and keep rollback to a single action.

### C10.6 Câu hỏi luyện
1. Walk me through the pipeline from a merged PR to production.
2. Continuous delivery vs continuous deployment?
3. Why build once and promote the same artifact?
4. How do you run database migrations in a pipeline? Why not at app startup?
5. A release breaks production and included a migration. How do you roll back?
6. Blue/green vs rolling vs canary?
7. What's a feature flag? How does it help release safely?
8. What checks should block a merge?
9. How do you manage secrets in CI/CD?
10. How do you ship a hotfix quickly without skipping safety?
11. What have you done with CI/CD yourself? (trả lời trung thực 20.5)
12. How do you achieve zero-downtime deployment?
13. What's infrastructure as code? Have you used it?

---

## C11. AWS (map từ Azure) ⏳

> ⏳ **Chưa viết lại sâu.** Dưới đây là nội dung bản cũ (số tham chiếu section bên trong là số bản cũ, xem bảng đối chiếu ở 0.2). Claude sẽ viết lại trước khi Hiệp học tới.

SA có AWS (AgilityIO), JD ghi AWS/cloud. Kinh nghiệm thật: Azure (PlaySweeps, Joblogic); AWS **KMS, S3, SES** trên project Go (Altar).

### C11.1 Bảng map
| Nhu cầu | AWS | Azure (đã dùng) | Ghi chú |
|---|---|---|---|
| Chạy web app container | **ECS Fargate** / App Runner / EKS | App Service / AKS | Fargate không quản lý server |
| Chạy web app PaaS | Elastic Beanstalk | App Service | |
| Function | **Lambda** (.NET 8 runtime, giới hạn 15 phút) | Azure Functions | Cold start |
| Queue | **SQS** Standard (at-least-once, không đảm bảo thứ tự) / **FIFO** (thứ tự theo message group, dedup 5 phút) | Service Bus queue (session) | Visibility timeout, DLQ (redrive policy) |
| Pub/sub | **SNS** (+ SQS fan-out) / **EventBridge** (rule, schedule) | Service Bus topic, Event Grid | |
| DB quan hệ | **RDS** SQL Server / PostgreSQL / **Aurora** | Azure SQL | Multi-AZ, read replica, automated backup, PITR |
| NoSQL | DynamoDB / DocumentDB | Cosmos DB / Mongo | |
| Cache | ElastiCache (Redis/Valkey) | Azure Cache for Redis | |
| File | **S3** + presigned URL, lifecycle, versioning, SSE-KMS | Blob + SAS | Bucket private, Block Public Access |
| Secret | **Secrets Manager** (xoay vòng) / SSM **Parameter Store** / **KMS** (khoá mã hoá) | Key Vault | |
| Quyền | **IAM role** (task role cho ECS, execution role cho Lambda), least privilege | Managed Identity + RBAC | Không để access key trong code |
| Monitoring | **CloudWatch** Logs/Metrics/Alarms + **X-Ray** (hoặc OpenTelemetry → ADOT) | App Insights | |
| Email / SMS | **SES** / SNS SMS / Pinpoint | SendGrid / Twilio | |
| API gateway / LB | API Gateway, **ALB**, CloudFront (CDN), WAF | API Management, Front Door, App Gateway | |
| Lịch chạy job | EventBridge Scheduler | Timer trigger | |
| Mạng | VPC, subnet public/private, security group, NAT gateway | VNet, NSG | DB ở private subnet |
| CI/CD | CodePipeline / CodeBuild / CodeDeploy, ECR | Azure DevOps, ACR | |
| IaC | CloudFormation / CDK / Terraform | ARM / Bicep / Terraform | |
| Auth người dùng | Cognito | Entra ID / B2C | |
| Search | OpenSearch | Azure AI Search | |
| Cấu hình động / feature flag | AppConfig | App Configuration | |

### C11.2 Kiến trúc tham khảo Ops Hub trên AWS
- Route 53 → CloudFront (static React) + **ALB** → **ECS Fargate** (ASP.NET Core API/MVC, ≥ 2 task ở 2 AZ, auto scaling theo CPU/request).
- **RDS SQL Server Multi-AZ** (+ read replica cho báo cáo), **ElastiCache Redis** (cache, rate limit).
- **S3** (PDF hợp đồng, ảnh giao hàng; private, presigned URL, versioning, lifecycle).
- **SQS** (+ DLQ) cho việc nền: sinh PDF, gửi email/SMS, đồng bộ bên thứ ba; worker là ECS service hoặc Lambda.
- **SNS/EventBridge** cho event fan-out; EventBridge Scheduler cho job định kỳ (nhắc thanh toán, hết hạn quote).
- **Secrets Manager** cho connection string/API key; **IAM task role**; KMS mã hoá.
- **CloudWatch** logs + alarms, **X-Ray**/OpenTelemetry tracing.
- SES email, SNS/Pinpoint SMS.
- Webhook từ bên thứ ba: API Gateway hoặc ALB → endpoint → ghi SQS → xử lý async.

### C11.3 Kiến thức hay hỏi
- **SQS visibility timeout**: message bị ẩn khi đang xử lý; quá hạn chưa xoá → hiện lại → xử lý lần 2 → consumer idempotent; nhận quá `maxReceiveCount` → DLQ.
- **SQS vs SNS vs EventBridge**: queue (1 consumer group, kéo) vs pub/sub (đẩy tới nhiều subscriber) vs event bus có rule lọc/định tuyến + schedule.
- **Lambda vs ECS**: Lambda cho việc ngắn, theo sự kiện, tải không đều (≤ 15 phút, cold start); ECS cho API chạy liên tục, việc dài, cần kiểm soát runtime.
- **S3 presigned URL**: URL có chữ ký, hết hạn ngắn, cấp quyền GET/PUT một object mà không lộ credential; backend kiểm tra quyền trước khi cấp.
- **IAM**: user (người) vs role (service đảm nhận, credential tạm thời); policy least privilege; không hard-code key.
- **RDS Multi-AZ** (sẵn sàng, failover tự động) vs **read replica** (scale đọc, có độ trễ).
- **Availability Zone vs Region**.
- Chi phí: NAT gateway, data transfer, CloudWatch logs có thể tốn; Fargate Spot/Savings Plans.
- .NET SDK: `AWSSDK.S3`, `AWSSDK.SQS`, `Amazon.Extensions.Configuration.SystemsManager`, `AWS.Logger`/Serilog sink, `Amazon.Lambda.AspNetCoreServer`.

### C11.4 Câu mẫu
> Most of my production cloud work was on Azure, and I've used AWS directly for KMS, S3 and SES on a Go project. The concepts map closely — Service Bus to SQS and SNS, Functions to Lambda, Key Vault to Secrets Manager, App Insights to CloudWatch and X-Ray — so I'd expect to be productive quickly and I'd learn the team's specific setup first.

### C11.5 Câu hỏi luyện
1. How would you host this .NET app on AWS?
2. SQS vs SNS vs EventBridge?
3. What's the SQS visibility timeout? What happens if processing takes longer?
4. Lambda or ECS for the PDF generator? For the main API?
5. How do you let a user download a private file from S3 securely?
6. Where do secrets live? How does the app get AWS credentials?
7. Multi-AZ vs read replica?
8. How would you monitor the system on AWS?
9. What AWS services have you actually used?
10. How would you make the system survive an AZ failure?
11. How would you receive webhooks reliably on AWS?

---

## C12. Multi-tenant SaaS ⏳

> ⏳ **Chưa viết lại sâu.** Dưới đây là nội dung bản cũ (số tham chiếu section bên trong là số bản cũ, xem bảng đối chiếu ở 0.2). Claude sẽ viết lại trước khi Hiệp học tới.

### C12.1 Ý chốt
- Mô hình: **Silo** (DB/tenant) – **Bridge** (schema/tenant) – **Pool** (chung bảng, cột TenantId) – **Shard** (pool chia nhiều DB). Trade-off: cô lập/chi phí/vận hành.
- Tenant context lấy từ **token/claim đăng nhập**, không từ tham số client gửi; đi theo mọi message, job, cache key, file path.
- Lớp phòng thủ: middleware resolve tenant → global query filter (EF) hoặc RLS/view (DB) → FK kèm TenantId → cache key có tenant → S3 prefix theo tenant → test với 2 tenant.
- Joblogic: shard theo tenant (ShardKey ở License DB), `SESSION_CONTEXT('TenantId')` đặt mỗi lần mở connection, đọc qua **view `dbo`** lọc tenant, ghi bị **RLS block predicate** chặn, PK/FK `(TenantId, Id)`, Depot là phạm vi con trong tenant.
- Cấu hình theo tenant (thuế, template, quy trình), **feature theo gói** (Joblogic: 60+ AppModule; FeatureManagement + TargetingFilter theo tenant).
- **Noisy neighbor**: đo theo tenant (metric có tag tenant), rate limit theo tenant, tách tenant lớn sang shard riêng, replica cho báo cáo, job nền chia lô theo tenant.
- Migration nhiều shard: expand → deploy → contract theo đợt.
- Job nền: quét tenant hợp lệ → fan-out message theo tenant.
- Di chuyển tenant giữa shard: copy → khoá ghi ngắn → copy phần chênh → đổi mapping → xoá cache mapping mọi instance.

### C12.2 Câu mẫu
> At Joblogic, tenant isolation was enforced in the database, not just in application code. When a connection opens, an interceptor sets the tenant ID in SQL Server's session context; the application reads through views that filter by it, and row-level security block predicates stop writes to another tenant's rows. Primary and foreign keys include the tenant ID, so a job can't point to another tenant's customer. For the Ops Hub I'd at least use an EF Core global query filter plus tenant-aware cache keys and S3 prefixes, and add tests that run with two tenants.

### C12.3 Câu hỏi luyện
1. How would you isolate tenant data? Pros and cons of database-per-tenant vs shared tables?
2. A customer sees another company's order. How do you investigate and prevent it?
3. One big tenant slows everyone down. What do you do?
4. How do you roll out a schema change across all tenants?
5. How do you support per-tenant configuration and features by plan?
6. Where does the tenant ID come from in a request? Why not from the URL?
7. How do background jobs know which tenant they're working for?

---

## C13. System design nhỏ ⏳

> ⏳ **Chưa viết lại sâu.** Dưới đây là nội dung bản cũ (số tham chiếu section bên trong là số bản cũ, xem bảng đối chiếu ở 0.2). Claude sẽ viết lại trước khi Hiệp học tới.

Khung 45 phút (rút gọn 15–20 phút nếu hỏi trong vòng tech):
1. **Làm rõ yêu cầu** (chức năng + phi chức năng: số tenant, số đơn/ngày, độ trễ, độ chính xác tiền).
2. **Ước lượng** con số (vd. 500 công ty × 20 đơn/ngày = 10k đơn/ngày ≈ 0,1 đơn/giây trung bình → tải thấp, rủi ro là **đúng** chứ không phải **nhanh**).
3. **API + mô hình dữ liệu**.
4. **Kiến trúc** (sơ đồ), luồng chính.
5. **Điểm khó**: concurrency, idempotency, thời gian, tiền, lỗi tích hợp.
6. **Vận hành**: monitor, scale, bảo mật, test.
7. **Trade-off** và cái sẽ làm sau.

### C13.1 Đề 1: Lên lịch giao hàng (delivery scheduling)
- Yêu cầu: chọn ngày giao, tài xế/xe, tối đa N đơn/xe/ngày, vùng giao, thông báo khách, driver app xác nhận.
- Dữ liệu: `Delivery(OrderId UNIQUE, Date date, StoreTimeZone, TruckId, DriverId, Status, Window)`, `TruckDayCapacity(TruckId, Date, Booked, Max)`.
- Chống overbook: `UPDATE TruckDayCapacity SET Booked = Booked + 1 WHERE TruckId=@t AND Date=@d AND Booked < Max` (rowcount = 0 → hết chỗ), cùng transaction với tạo Delivery.
- Đổi lịch: giải phóng chỗ cũ + giữ chỗ mới trong một transaction; event → push driver app + SMS khách (outbox).
- Thời gian: `date` + timezone cửa hàng; DST.
- Driver app offline: version số cho delivery, đồng bộ lại, xung đột → văn phòng thắng + báo tài xế.

### C13.2 Đề 2: Lịch trả góp RTO
- Input: tổng, số kỳ, phí ban đầu, ngày bắt đầu, provider.
- Sinh lịch: chia đều làm tròn 2 số, **kỳ cuối bù**; ngày đến hạn theo lịch (ngày 31 → cuối tháng); lưu snapshot lịch trong contract.
- Strategy theo provider; provider có thể là nguồn sự thật → mình chỉ lưu bản sao + đối soát.
- Thanh toán từng kỳ qua webhook → ledger, idempotent; trễ hạn → job nhắc (EventBridge Scheduler), phí trễ theo luật provider.
- Test: tổng = hợp đồng, tháng 2, năm nhuận, DST không ảnh hưởng ngày lịch.

### C13.3 Đề 3: Sinh tài liệu PDF (quote/contract/invoice)
- API: `POST /orders/{id}/documents` → 202 + job id; `GET /documents/{id}` → trạng thái + presigned URL.
- Worker (SQS → ECS/Lambda): lấy document model đã tính (domain lo nghiệp vụ), chọn template tenant → fallback hệ thống, render (QuestPDF/HTML→PDF), lưu S3 (`tenant/{id}/orders/{id}/...`), cập nhật trạng thái.
- Cache theo checksum dữ liệu + template version; tài liệu đã ký bất biến (hash).
- Lỗi ký tự đặc biệt: escape, font Unicode; test với dữ liệu xấu.
- Scale: nhiều worker, giới hạn đồng thời; DLQ cho job lỗi.

### C13.4 Đề 4: Notification (email/SMS khi trạng thái đơn đổi)
- Domain event (OrderScheduled, OrderDelivered) → outbox → queue → notification service → chọn kênh theo cấu hình tenant + opt-in khách → template → SES/SNS/Twilio.
- Idempotent theo (eventId, recipient, channel); retry backoff; DLQ; log trạng thái gửi (delivered/bounced).
- Giờ yên lặng theo timezone khách; rate limit theo provider.

### C13.5 Đề 5: Payment API / ghi nhận thanh toán
- `POST /orders/{id}/payments` với Idempotency-Key → tạo payment intent ở provider → webhook xác nhận → ledger → cập nhật balance due.
- Không tin client; số tiền tính từ server; trạng thái Pending → Succeeded/Failed; đối soát hằng ngày.
- Chất liệu thật: Pragmatic wallet, Nexus, Stripe ở Joblogic Payment service.

### C13.6 Đề khác trong question bank (biết khung)
Rate limiter đa instance (Redis sliding window/token bucket, Lua script atomic), order processing, file upload service (presigned PUT, quét virus, metadata), URL shortener (ít liên quan).

### C13.7 Câu hỏi luyện
1. Design delivery scheduling with truck capacity limits.
2. Design an RTO payment schedule and payment tracking.
3. Design PDF document generation for quotes and contracts.
4. Design notifications when an order's status changes.
5. Design a payment API.
6. Design a rate limiter for a multi-instance API.
7. How would you design the system for 10× more companies?

---

## D1. Giới thiệu bản thân, câu hỏi cá nhân ⏳

> ⏳ **Chưa viết lại sâu.** Dưới đây là nội dung bản cũ (số tham chiếu section bên trong là số bản cũ, xem bảng đối chiếu ở 0.2). Claude sẽ viết lại trước khi Hiệp học tới.

### D1.1 Pitch 60 giây
> I'm a full-stack developer with about four years of experience, strongest on the .NET backend. Most recently I worked on PlaySweeps, a US sweepstakes gaming platform with over two million registered players, on .NET 8, SQL Server, Azure and React. I was a feature lead there: I wrote technical designs, delivered features like the Quest Engine and the KYC integration with Socure, and handled on-call incidents. In parallel, I worked part-time for a UK field-service SaaS called Joblogic, on ASP.NET MVC and a .NET microservice platform, where I delivered features in the Projects and Jobs modules such as cost breakdowns, customer contracts with audit trails, and job spend limits. What attracts me to ShedPro is that the Ops Hub is a business-heavy product, quoting, contracts, production, delivery, which is very close to what I did at Joblogic, and I like working closely with a product manager to understand why a feature matters.

Bản 30 giây (khi bị giục):
> I'm a .NET full-stack developer with about four years of experience. I've worked on a US sweepstakes gaming platform with over two million players, where I led features end to end, and on a UK field-service SaaS with quoting, contracts and cost tracking, which is close to what the Ops Hub does.

### D1.2 Timeline phải thuộc (đừng nói sai)
| Giai đoạn | Thời gian |
|---|---|
| Astraler — Backend Intern (Node.js, lead nhóm 4 intern) | 07/2022 – 11/2022 |
| Geargames — Junior Fullstack → Fullstack Engineer | 12/2022 – 09/2026 |
| ↳ Game config platform (NestJS, React) | 12/2022 – 11/2023 |
| ↳ EIM (NestJS, TypeScript, MySQL, React) | 11/2023 – 05/2024 |
| ↳ Altar of Sacrifice (Go, MongoDB, AWS KMS/S3/SES, React) | 05/2024 – 12/2024 |
| ↳ PlaySweeps (.NET 8, SQL Server, Azure, React) | 01/2025 – 09/2026 |
| Joblogic — part-time freelance (ASP.NET MVC, .NET 8) | 01/2026 – 06/2026 |
| Rời Geargames (công ty tái cấu trúc) | 09/2026 |
Kinh nghiệm: tính từ 07/2022 → ~4 năm 3 tháng; full-time từ 12/2022 → ~3 năm 10 tháng. Nói "about four years".

### D1.3 Câu hỏi cá nhân hay gặp
| Câu hỏi | Ý trả lời |
|---|---|
| Why are you leaving / why did you leave? | > The company restructured and my position was affected in September. I'm now looking for a product team where I can own a business-critical system for the long term. (Không nói thêm chi tiết, không chê công ty cũ.) |
| Why SEADEV / why this role? | Sản phẩm nhiều nghiệp vụ (quote, contract, production, delivery) giống Joblogic; làm sát PM; tiếp quản và phát triển dài hạn; .NET là thế mạnh; làm với đối tác Mỹ đã quen (PLAYSTUDIOS). 🟢 Thêm purpose "Create jobs, improve lives, make awesome stuff" và value 1% Improvement / Customer Success (bản đầy đủ: `S-seadev-culture.md` 4.2). |
| What do you know about ShedPro / Ops Hub? | Chỉ nói phạm vi JD: SaaS cho doanh nghiệp bán shed/carport ở Bắc Mỹ; Ops Hub quản lý quoting, sales orders, rent-to-own contracts, production tracking, delivery scheduling; đang tiếp quản từ đối tác Mỹ. > From the job description, the Ops Hub is the operational back office for shed and carport businesses in North America — quoting, sales orders, rent-to-own contracts, production tracking and delivery scheduling — and the codebase is being taken over from a US partner. |
| Strengths? | Backend .NET, hiểu nghiệp vụ và edge case, tự đào sâu (TDD Quest Engine, tiếp quản Socure), on-call bình tĩnh. Kèm một ví dụ. |
| Weakness? | Chọn điểm yếu thật nhưng đang cải thiện, không phạm vào yêu cầu cốt lõi. Ví dụ: tiếng Anh nói (đang học PTE), hoặc chưa tự dựng CI/CD pipeline từ đầu (đang học). > My spoken English is less fluent than my reading and listening, so I'm preparing for PTE Academic and I practise explaining technical designs in English. In my last role I wrote technical designs in English and joined design meetings with the US team. |
| Where do you see yourself in 3–5 years? | Senior/tech lead cho một mảng sản phẩm, sở hữu kiến trúc và chất lượng của module, mentor người mới. Gắn với vai trò "leading new feature development". |
| What does a senior developer mean to you? | Sở hữu kết quả chứ không chỉ task: hiểu nghiệp vụ, thiết kế có trade-off, chất lượng (test, review), vận hành (monitor, on-call), giúp team. |
| How do you learn new technology quickly? | Ví dụ thật: Go + AWS (KMS, S3, SES) ở Altar; Socure tự đọc dashboard/decision module; Rive làm với designer nước ngoài. Cách học: đọc tài liệu chính thống → làm prototype nhỏ → áp dụng vào task thật → ghi lại. |
| Expected salary? | [Hiệp điền con số]. Khung: nói khoảng (range) dựa trên thị trường Senior .NET Đà Nẵng, mở thương lượng tổng gói. > Based on my experience and the market for this role, I'm looking for a range of [X–Y] gross per month, and I'm open to discussing the full package. |
| Notice period / start date? | Đã rời Geargames 09/2026 → có thể bắt đầu sớm. [Hiệp xác nhận]. |
| Are you interviewing elsewhere? | Thật lòng, ngắn gọn; nhấn SEADEV là lựa chọn ưu tiên vì nghiệp vụ phù hợp. |
| Remote or onsite? | [Hiệp điền mong muốn]. |
| Do you have any questions? | Xem section 29. **Luôn có câu hỏi.** |

### D1.4 Câu hỏi luyện
1. Tell me about yourself. (60 giây, rồi 30 giây)
2. Walk me through your CV.
3. Why did you leave your last company?
4. Why should we hire you over other candidates?
5. What's the most valuable thing you built?
6. What do you know about our product?
7. What kind of team do you work best in?

---

## D2. Kể dự án trong CV + bị đào sâu ⏳

> ⏳ **Chưa viết lại sâu.** Dưới đây là nội dung bản cũ (số tham chiếu section bên trong là số bản cũ, xem bảng đối chiếu ở 0.2). Claude sẽ viết lại trước khi Hiệp học tới.

SA và PO sẽ chọn một dòng trong CV và đào: "tell me more about X → how did you design it → what went wrong → what would you change → how would you apply it here". Mỗi câu chuyện 60–90 giây theo khung **bối cảnh → vấn đề → bạn làm gì → kết quả → bài học / nối sang Ops Hub**.

### D2.1 PlaySweeps (01/2025 – 09/2026)
Sự thật: client PLAYSTUDIOS (NASDAQ: MYPS), 2M+ registered players; backend .NET 8 (~150 project, ~1.330 commit của Hiệp, nhiều nhất team), Dapper + stored procedure + LINQ, repository bọc SP, Autofac; Cosmos DB, Redis; Azure Functions, Service Bus, Event Hub, Key Vault, App Insights; web React 18 + Redux (~340 commit). Vai trò feature lead, review chéo PR, on-call. Scrum + Jira (~354 ticket). ~200 file test xUnit + Moq.

**Kiến trúc 1 phút:**
> PlaySweeps is a .NET 8 backend with around 150 projects, a React web client, SQL Server accessed through Dapper and stored procedures, Cosmos DB for some feature state, Redis for caching and distributed locks, and Azure Functions with Service Bus and Event Hub for background processing. Player balances for Sweeps Coin are owned by a PLAYSTUDIOS service called Nexus; we sent it deltas with a unique transaction ID and kept a local mirror.

**Câu chuyện chính:**
| Feature | Ý chính để kể | Câu đào sâu dự kiến |
|---|---|---|
| **Quest Engine V2** | Viết TDD (07/2026), làm từ thiết kế đến release, lên production. Công thức nghiệp vụ (ncalc) do client thiết kế, Hiệp làm rõ requirement. Cosmos DB lưu state, Redis + RedLock, **idempotency key cho claim** | Vì sao Cosmos? Vì sao cần lock? RedLock có vấn đề gì (không có fencing token)? Chống claim 2 lần thế nào? Reward async hay sync? |
| **Socure KYC** | Tiếp quản tích hợp do đồng nghiệp làm (10/2024), tự tìm hiểu dashboard/decision module, phát hiện prototype của client có giả định sai, sửa lại tới khi chạy ổn trên production. DocV (ID + selfie), SSN, soft KYC/manual review | Tiếp quản thế nào? Webhook/callback từ vendor xử lý ra sao? Trạng thái KYC lưu thế nào? |
| **Pragmatic Play seamless wallet** | Hook bet/result/refund/promo-win/free-spin/buy-bonus; xác thực hash; khoá pending wager; idempotency | Key idempotency là gì (transaction reference, không phải roundId)? Trùng thì trả gì (replay response)? Refund đến trước bet? |
| **Nexus balance** | Gửi delta + TransactionId GUID; Nexus kiểm idempotency + kiểm số dư + cập nhật trong 1 transaction; bản SQL local là mirror ghi giá trị tuyệt đối | Điểm yếu của mirror? (response về không theo thứ tự → cần sequence check) |
| **Exponential rate limiting** | Cho API nhạy cảm (đăng nhập, OTP…) | Đa instance thì lưu counter ở đâu (Redis)? Thuật toán? |
| **MFA + trusted device, multi-account abuse, spend limit, redemption (Skrill, ACH, Prizeout, Paysafe)** | Nghiệp vụ tiền + bảo mật | Spend limit tính theo cửa sổ thời gian nào? Chống race khi 2 request cùng lúc? |
| **On-call** | Theo dõi exception spike, điều tra bằng App Insights, Grafana Loki, Splunk (theo BI event để dựng lại hành trình user), hotfix, chốt với tech lead và QA | Kể 1 vụ cụ thể **[Hiệp điền: chọn 1 sự cố có con số]** |
| **3 TDD** | Quest Engine V2, Banner System (09/2025), CRM Direct-Target Offers (08/2026) | TDD gồm những phần gì? Ai review? |

Câu mẫu Quest Engine (dẫn dắt feature):
> I led Quest Engine V2 from design to production. The client defined the reward formulas, so my first job was to clarify the requirements with them and write the technical design. Quest progress was stored in Cosmos DB, updates for the same player were serialized with a Redis lock, and claiming a reward used an idempotency key so a retry or a double click could never pay twice. I wrote unit tests around progress calculation and claim rules, and after release I monitored it in Application Insights.

Câu tự phản biện (Senior hay được hỏi "what would you change"):
> If I did it again, I'd rely less on the distributed lock for correctness: a Redis lock has no fencing token, so a paused process could still write after its lock expired. I'd make the database the arbiter — a unique constraint on the claim key and an optimistic concurrency check on the progress document — and keep the lock only to reduce contention.

### D2.2 Joblogic (01/2026 – 06/2026, part-time freelance)
**Kiến trúc 2 phút:**
> Joblogic is a multi-tenant field-service management SaaS in the UK. The front apps are ASP.NET Core on .NET 8 — a large MVC back-office with Razor views and embedded Vue components, a customer portal and a Web API for mobile and partners. Behind them are around thirty backend services running as Azure Functions, which they call "Jicroservices": Core, Audit, DocGen, Notification, Payment, Schedule and so on. Queries go over HTTP, commands go over Service Bus queues, and events are published to topics so several services can react. Handlers return a result type, OneOf success or error, instead of throwing for business errors. Data is SQL Server sharded by tenant, plus MongoDB for audit and offline mobile data, Redis and Blob storage. Tenant isolation is enforced in the database: every connection sets the tenant ID in SQL Server session context, reads go through views filtered by it, and writes are blocked by row-level security if the tenant doesn't match.

**4 feature (khung: vấn đề → nghiệp vụ → thiết kế → edge case → kết quả → nối Ops Hub)**
| Feature | Nội dung thật | Edge case để kể | Nối sang Ops Hub |
|---|---|---|---|
| **Project Cost Breakdown** (01/2026) | Tab Summary: Actual vs Estimated theo 10 loại chi phí, Cost Variance, Actual/Estimated Profit & Margin, đa tiền tệ. Estimated từ dòng của Project Quote Sections, Actual từ job cost lines + PO. Sửa `GetProjectJobCostHandler` | Đa tiền tệ (quy đổi), margin vs markup, project lớn chậm | Giá quote, margin, balance due |
| **Customer Contract cho Project** (01–04/2026) | Dropdown Customer Contract ở Project/Quote; ẩn/hiện theo tenant có subscribe app; **audit có version** lưu MongoDB; **DocX tags** mới cho template Invoice/Application/Quote; logic **Previously Claimed** khi invoice cộng dồn | Tài liệu đã phát hành không được đổi khi template đổi; feature gating theo gói | RTO/cash sale contract template theo công ty, History Notes |
| **Selling Rate Times & Holidays** (03–04/2026) | Lưới tuần: khoảng thời gian gắn giá bán, loại (pay band / holiday), kéo-thả, read-only; logic "chargeable"; sửa nhiều bug critical; có unit test | Ca vắt qua nửa đêm, ngày lễ, chồng lấn khoảng thời gian | Tính giá theo thời gian, lịch giao, DST |
| **Job Spend Limit** (05–06/2026, làm cùng một đồng nghiệp) | Banner OverLimit/InLimit: visit 1 so với hạn mức, **visit 2+ so với phần còn lại**; cờ **RedeployRequired** khi hạn mức đổi sau khi visit đã xuống thiết bị; **BO notification** fan-out theo role, idempotent theo `EventIdempotentId`; Customer Portal cho khách sửa spend limit; permission mới | Đổi hạn mức sau khi đã deploy xuống mobile; trùng event → gửi 2 thông báo | Approval/ngưỡng, thông báo email/SMS, phân quyền |

Câu mẫu Job Spend Limit (edge case nghiệp vụ, PO rất thích):
> The requirement looked simple: warn when a visit's estimated spend goes over the job's spend limit. When I walked through real scenarios, two edge cases came up. First, for the second and later visits, the comparison had to be against the remaining limit after earlier visits, not the full limit. Second, a visit could already be deployed to the engineer's mobile device when the office changed the limit, so the data on the device was stale; we added a "redeploy required" flag. The back-office notification was fan-out to the right roles and idempotent on the event ID, so a retried event didn't notify people twice.

Câu đào sâu Joblogic hay gặp:
1. Why Azure Functions instead of normal web services? (Họ chọn sẵn; nói lợi: scale theo trigger, timer/queue trigger tiện; hại: cold start, giới hạn thời gian chạy, debug khó.)
2. How do services communicate and what if a message is processed twice? (At-least-once → consumer idempotent theo OperationId/EventIdempotentId.)
3. How is tenant isolation enforced? (SESSION_CONTEXT + view + RLS block predicate + FK kèm TenantId.)
4. Why return OneOf instead of throwing? (Lỗi nghiệp vụ là kết quả bình thường; exception cho bất ngờ; caller buộc xử lý.)
5. How did you work with the UK team? (Azure DevOps PR, code review, nhánh uat; giao tiếp async.)
6. EF Core or EF6? > The core domain still uses EF6 running on .NET 8, newer parts use EF Core, plus Dapper for read-heavy queries.
7. How did you generate documents? (DocGen: Core trả document model đã tính sẵn → chọn template tenant → fallback hệ thống → thay tag `@@Tag@@` bằng Xceed DocX → Aspose.Words xuất PDF/DOCX → cache theo checksum.)

### D2.3 Dự án khác (khả năng bị hỏi thấp, chuẩn bị 2 câu mỗi cái)
- **EIM** (NestJS, TypeScript, TypeORM, MySQL, Redis, JWT, Swagger; React + TanStack Query + Ant Design): module nghỉ phép, overtime, accrued leave hours, lock record, notification. 39 module, 46 entity, 26 migration.
- **Game config platform**: NestJS, MariaDB, Protobuf có version, import/export Excel blueprint, JSON diff trước khi deploy config.
- **Altar of Sacrifice** (client Immutable): Go (Gin), MongoDB, Redis, AWS KMS/S3/SES; recipe engine, mint cap, webhook burn/mint qua Redis queue có tracking lỗi. **Đây là bằng chứng AWS thật.**
- **Astraler**: lead nhóm 4 intern, Node.js.

### D2.4 Câu hỏi luyện
1. Tell me about the most complex feature you built.
2. Draw the architecture of PlaySweeps / Joblogic. Where would it break first under 10× load?
3. What was your exact role in the Quest Engine? What did you decide and what did others decide?
4. You took over the Socure integration — what was wrong and how did you find out?
5. How did you prevent double payouts in the wallet integration?
6. What would you do differently in the Joblogic spend-limit feature?
7. How did you ensure a signed contract document doesn't change when the template changes?
8. How did the margin calculation handle multiple currencies?
9. Tell me about a time a requirement changed late. (Gợi ý: Job Spend Limit, RedeployRequired.)
10. How much of PlaySweeps backend did you know? (~150 project; feature mình lead thì nắm sâu, phần khác nắm luồng chính.)

---

## D3. Nghiệp vụ Ops Hub ⏳

> ⏳ **Chưa viết lại sâu.** Dưới đây là nội dung bản cũ (số tham chiếu section bên trong là số bản cũ, xem bảng đối chiếu ở 0.2). Claude sẽ viết lại trước khi Hiệp học tới.

Chỉ dùng phạm vi **công khai trong JD**. Nói dạng "I'd assume… and I'd confirm with the PM". SA có nền Urbanise (SaaS vận hành: tiền định kỳ, workflow bảo trì, tài liệu, đối soát ngân hàng) → rất có thể hỏi tiền, workflow, tài liệu.

### D3.1 Thuật ngữ
| Từ | Nghĩa |
|---|---|
| Shed / carport | Nhà kho / mái che xe đúc sẵn, bán qua đại lý (dealer/store) ở Bắc Mỹ |
| Quote | Báo giá: sản phẩm, kích thước, option, giá, thuế, phí giao, hết hạn |
| Finalize / lock quote | Khoá báo giá: giá và nội dung không đổi nữa (snapshot) |
| Sales order | Đơn hàng sau khi khách chấp nhận |
| Cash sale | Mua trả thẳng (có thể trả deposit trước, phần còn lại khi giao) |
| **RTO (rent-to-own)** | Thuê-mua: khách trả góp hằng tháng, đủ kỳ thì sở hữu; thường qua công ty RTO bên thứ ba duyệt (eligibility, credit check) |
| Deposit / down payment | Tiền đặt cọc |
| **Balance due** | Số còn phải trả |
| Production queue / build list | Hàng đợi sản xuất, thứ tự đóng |
| Delivery scheduling | Lên lịch giao: ngày, tài xế/xe, tuyến, cửa sổ thời gian |
| Driver app | App tài xế: lịch, xác nhận giao, ảnh, chữ ký, thu tiền |
| Inventory | Hàng có sẵn (đã đóng) để bán ngay |
| Markup vs margin | Markup = lợi nhuận / giá vốn; margin = lợi nhuận / giá bán. Giá vốn 100, bán 125 → markup 25%, margin 20% |
| Sales tax (Mỹ) | Theo bang/quận/thành phố, theo địa chỉ giao; Canada: GST/PST/HST |
| Audit trail / history notes | Ai làm gì, lúc nào, trước/sau |

### D3.2 Luồng chính và dữ liệu
Quote (sản phẩm, option, giá, thuế, hết hạn) → **Finalize/Accept** (khoá giá, snapshot) → Sales Order (cash sale hoặc **RTO**) → Contract (template, chữ ký) → Production (queue, trạng thái) → Delivery (lịch, tài xế, xác nhận, ảnh, thu tiền còn lại) → Closed.
Mô hình dữ liệu gợi ý:
- `Company` (tenant) → `Store`/`Region` → `User` (role).
- `Customer`, `Product`/`Option`/`PriceList` (master data, 3NF).
- `Quote` + `QuoteLine` (**snapshot** ProductName, UnitPrice, TaxRate, phí) + `QuoteRevision`.
- `Order` (status, loại: Cash/RTO) + `OrderLine` (copy từ quote đã finalize).
- `Payment` / ledger (`OrderTransaction`: Deposit, Payment, Refund, Adjustment) → balance due tính từ ledger.
- `Contract` (template id + version, file PDF đã sinh, trạng thái ký, dữ liệu snapshot).
- `ProductionJob` (queue, vị trí, trạng thái), `Delivery` (ngày lịch + timezone, tài xế, xác nhận, ảnh).
- `AuditEntry` (entity, field, old/new, user, thời điểm UTC).

### D3.3 Tiền
- **`decimal`**, không `double`/`float` (0.1 + 0.2 ≠ 0.3 với double). DB: `DECIMAL(18,2)` (hoặc 19,4 cho đơn giá), EF `HasPrecision(18,2)`.
- **Làm tròn một chỗ**, quy tắc rõ: `Math.Round(x, 2, MidpointRounding.AwayFromZero)` (mặc định C# là **ToEven/banker's**). Làm tròn theo dòng hay theo tổng → **hỏi PO/kế toán**, khác nhau vài cent.
- **Snapshot** giá/thuế trên quote/order khi finalize; đổi bảng giá không ảnh hưởng quote đã gửi.
- **Balance due = total (gồm thuế, phí) − tổng payment đã ghi nhận + refund đã trả lại (nếu tính ngược) ± adjustment**. Tính từ **ledger chỉ ghi thêm** (append-only), không lưu một con số rồi cộng trừ tay → tránh lệch. Nếu cần lưu số dư để query nhanh: cập nhật trong **cùng transaction** với ledger + job đối soát.
- **Trả góp (RTO)**: chia kỳ làm tròn, **kỳ cuối bù chênh lệch**; unit test: tổng các kỳ = tổng hợp đồng. Lịch trả có thể do công ty RTO tính → hỏi PO ai là nguồn sự thật.
- **Thuế** theo địa chỉ giao (không phải địa chỉ cửa hàng), có thể lấy từ API thuế bên thứ ba → cache + snapshot mức thuế vào order; khách miễn thuế (tax-exempt).
- **Thanh toán qua provider** (Stripe hoặc tương tự): webhook → xác thực chữ ký → **idempotent theo event id** → cập nhật ledger. Không tin số tiền từ client.
- **Refund / huỷ**: bút toán ngược trong ledger, không xoá payment.
- **Value object** `Money(Amount, Currency)`: cộng trừ chỉ khi cùng currency, làm tròn tập trung.

Câu mẫu:
> I'd never store the balance as a number that we add to and subtract from in different places. Payments, refunds and adjustments go into an append-only ledger, and the balance due is the order total — locked when the quote was finalized, including tax — minus the net of that ledger. Money is `decimal`, rounding happens in one place with an explicit rule, and payment webhooks are applied idempotently by event ID. That way, if a number looks wrong, we can explain every cent.

### D3.4 Thời gian / múi giờ / DST
- Lưu **instant** (đã xảy ra: created, paid, delivered-at) bằng UTC (`DateTimeOffset`/`datetime2` UTC).
- **Ngày giao dự kiến là ngày lịch**, không phải instant → `DateOnly`/SQL `date` + timezone của cửa hàng/khách (IANA, vd. `America/Chicago`). Không lưu "nửa đêm UTC".
- Bắc Mỹ: nhiều múi giờ (ET, CT, MT, PT, Alaska, Hawaii; Arizona **không** DST) + DST (2026: bắt đầu **08/03**, kết thúc **01/11**). Tính "+N ngày" theo lịch địa phương (`TimeZoneInfo` hoặc NodaTime), không cộng 24h × N.
- Bug kinh điển: lưu `2026-11-02 00:00` giờ địa phương thành UTC rồi hiển thị ở múi giờ khác → lệch 1 ngày; cộng 24h qua ngày đổi giờ → lệch 1 giờ, có thể nhảy ngày.
- Hiển thị: server trả UTC (ISO 8601 có `Z`) cho instant, trả `yyyy-MM-dd` cho ngày lịch; frontend hiển thị theo timezone của **cửa hàng** (không phải trình duyệt) cho dữ liệu vận hành.
- Test: `TimeProvider` giả (`FakeTimeProvider`) với ngày DST, cuối tháng, năm nhuận, 23:30 ở Pacific (= hôm sau UTC).
- "Hết hạn quote sau 30 ngày" → 30 ngày lịch theo timezone cửa hàng, hết hạn lúc cuối ngày địa phương.

Câu mẫu:
> A delivery date is a calendar date, not an instant, so I'd store it as a date plus the store's time zone, and only convert to UTC for actual timestamps like "delivered at". Off-by-one-day bugs usually come from storing local midnight as UTC and then rendering it in another zone, or from adding 24 hours across a DST change.

### D3.5 Tài liệu PDF / hợp đồng / chữ ký
- Template theo công ty (tenant) → fallback template hệ thống; tag thay thế (Joblogic `@@Tag@@`).
- Tài liệu **đã ký/đã phát hành phải bất biến**: lưu file PDF đã sinh + **phiên bản template** + **snapshot dữ liệu** + hash file. Đổi template chỉ ảnh hưởng tài liệu mới.
- Sinh PDF ở **background worker** nếu chậm (202 + trạng thái); cache theo checksum dữ liệu (Joblogic DocGen); file lưu **S3**, tải bằng **presigned URL** ngắn hạn sau khi kiểm tra quyền.
- **Escape** ký tự đặc biệt (`&`, `<`, ký tự Unicode, emoji) khi đưa dữ liệu vào template/HTML; font hỗ trợ ký tự; kiểm tra layout với dữ liệu dài (tên dài, nhiều dòng).
- Rich text (T&C) → **sanitize HTML** trước khi render (XSS).
- Thư viện .NET: QuestPDF, iText, Aspose, Playwright/Chromium HTML→PDF, DinkToPdf. Joblogic dùng Xceed DocX + Aspose.Words.
- E-signature: lưu ai ký, lúc nào, IP/thiết bị, hash tài liệu tại thời điểm ký; nhiều trang/nhiều bên ký.

Câu mẫu:
> Once a contract is signed, it's a legal record, so it must never be regenerated from current data. I'd store the generated PDF in S3 together with the template version and a snapshot of the data used, plus a hash. If the company updates its template, only new contracts use it. If a customer disputes a contract a year later, we show exactly the file they signed, and the audit trail shows who sent it and when it was signed.

### D3.6 Production & delivery

Bối cảnh: shed (nhà kho gỗ/kim loại) được **đóng theo đơn** ở xưởng rồi chở bằng xe chuyên dụng (xe kéo/xe "mule") tới sân nhà khách. Vòng đời sau khi order được xác nhận: **vào hàng đợi sản xuất → đóng → kiểm tra → lên lịch giao → giao + xác nhận → (thu nốt tiền)**. Mỗi bước có một nhóm người dùng khác: quản lý xưởng, thợ, điều phối giao hàng, tài xế, khách. Đây là phần "vận hành", PO rất hay hỏi tình huống ở đây. Chi tiết ShedPro thật mình chưa biết, nên khi trả lời hãy nói "I'd assume… and confirm with the PO".

Tóm tắt 5 ý:
- Production queue: thứ tự đóng có thể kéo-thả thủ công → lưu `Position` (số thực/khoảng trống hoặc rank) + optimistic concurrency khi hai người cùng sắp xếp.
- Trạng thái sản xuất cập nhật từ xưởng (có thể qua tablet) → audit.
- Delivery: ràng buộc (xe chở tối đa N đơn/ngày, vùng giao, cửa sổ thời gian, điều kiện mặt bằng). Chống đặt quá → atomic UPDATE bộ đếm hoặc `UPDLOCK` trên dòng (xe, ngày) (`notes/03`).
- Driver app: có thể offline → dữ liệu trên máy là bản chụp; văn phòng đổi lịch → push + đồng bộ lại (giống RedeployRequired ở Joblogic); xác nhận giao + ảnh + chữ ký + thu tiền → idempotent khi app retry.
- Thông báo khách: SMS/email khi lên lịch, trước ngày giao, khi giao xong; tôn trọng opt-out; gửi qua queue, idempotent.

#### D3.6.1 Production queue: lưu thứ tự kéo-thả

**Vấn đề.** Quản lý xưởng kéo đơn A lên trên đơn B (gấp, khách VIP, thiếu vật tư thì đẩy xuống). Cần lưu thứ tự sao cho: (1) di chuyển 1 đơn không phải ghi lại cả 500 dòng, (2) hai người cùng sắp xếp không làm hỏng thứ tự.

**Ba cách lưu thứ tự** (đi từ đơn giản lên):

| Cách | Di chuyển 1 đơn | Nhược điểm |
|---|---|---|
| Số nguyên liên tiếp 1,2,3… | UPDATE mọi dòng giữa vị trí cũ và mới (O(n)) | Nhiều dòng bị khoá, dễ deadlock khi 2 người cùng kéo |
| Số có khoảng trống (1000, 2000, 3000) hoặc `decimal`: chèn vào giữa = trung bình hai bên | Ghi **1 dòng** | Sau nhiều lần chèn vào cùng một chỗ thì hết khoảng (1000 → 1500 → 1250…) → cần **rebalance** (đánh lại 1000, 2000…) |
| Rank dạng chuỗi (LexoRank kiểu Jira, "fractional indexing") | Ghi 1 dòng, sinh chuỗi nằm giữa hai chuỗi | Phức tạp hơn, cần thư viện; chỉ đáng khi danh sách rất dài và kéo liên tục |

Với xưởng shed (vài chục tới vài trăm đơn đang chờ mỗi xưởng), **số có khoảng trống + rebalance** là đủ. Nói được "I'd pick the simplest one that fits the size" là điểm Senior.

```csharp
public class ProductionJob
{
    public Guid Id { get; set; }
    public Guid PlantId { get; set; }          // mỗi xưởng một hàng đợi
    public Guid OrderId { get; set; }
    public decimal Position { get; set; }      // DECIMAL(20,10)
    public ProductionStatus Status { get; set; }
    public byte[] RowVersion { get; set; } = default!; // SQL Server rowversion
}

// Client gửi: "đặt job X nằm giữa beforeId và afterId" (không gửi số Position)
public async Task MoveAsync(Guid jobId, Guid? beforeId, Guid? afterId, byte[] rowVersion)
{
    var job = await _db.ProductionJobs.SingleAsync(j => j.Id == jobId);
    _db.Entry(job).Property(j => j.RowVersion).OriginalValue = rowVersion;

    decimal? prev = beforeId is null ? null :
        await _db.ProductionJobs.Where(j => j.Id == beforeId).Select(j => (decimal?)j.Position).SingleAsync();
    decimal? next = afterId is null ? null :
        await _db.ProductionJobs.Where(j => j.Id == afterId).Select(j => (decimal?)j.Position).SingleAsync();

    job.Position = (prev, next) switch
    {
        (null, null) => 1000m,
        (null, var n) => n!.Value - 1000m,      // lên đầu
        (var p, null) => p!.Value + 1000m,      // xuống cuối
        var (p, n) => (p!.Value + n!.Value) / 2 // chèn giữa
    };

    try { await _db.SaveChangesAsync(); }
    catch (DbUpdateConcurrencyException)
    {
        throw new ConflictException("Queue changed, please refresh"); // → HTTP 409
    }
    // nếu khoảng cách (next - prev) < 0.0001 → đẩy job nền rebalance cho PlantId này
}
```

Điểm cần nói:
- **Client gửi ý định ("đặt giữa A và B"), không gửi con số** → server tự tính, tránh client cũ ghi đè.
- **Optimistic concurrency** (`rowversion` / EF `IsRowVersion()`): người thứ hai lưu bản cũ → `DbUpdateConcurrencyException` → trả **409 Conflict**, UI tải lại hàng đợi. Chọn optimistic vì xung đột hiếm (vài người sắp xếp), không cần giữ khoá trong lúc người dùng kéo.
- Mức chặt hơn: concurrency theo **cả hàng đợi** (một cột `QueueVersion` trên bảng `Plant`, tăng mỗi lần sắp xếp), vì A kéo job 1 và B kéo job 2 cùng lúc có thể đều "thành công" nhưng kết quả không phải điều ai muốn. Hỏi PO mức nào đủ.
- Realtime: sau khi lưu, đẩy sự kiện qua **SignalR** tới các màn hình khác đang mở hàng đợi xưởng đó → giảm 409.
- Index `(PlantId, Status, Position)` để lấy hàng đợi theo thứ tự.

Câu mẫu:
> For a drag-and-drop production queue I'd store a sortable position with gaps, so moving one job means updating one row: the new position is the midpoint between its new neighbours, and a background job rebalances when the gaps get too small. The client sends "put job X between A and B", not a number. Each save checks a row version, so if two managers reorder at the same time, the second one gets a 409 and a refreshed queue instead of silently overwriting the first. I'd push the change over SignalR so other screens stay in sync. If the queue were thousands of items reordered constantly, I'd look at a string rank like Jira's LexoRank, but I'd start simple.

#### D3.6.2 Trạng thái sản xuất từ xưởng + audit

**Vấn đề.** Thợ/quản lý xưởng cập nhật trạng thái bằng tablet (thường dùng chung, đeo găng tay, wifi xưởng chập chờn): `Queued → InProgress → Built → QualityChecked → ReadyForDelivery` (có thể có `OnHold`, `Cancelled`). Văn phòng và khách cần biết đơn đang ở đâu; khi có tranh chấp ("ai đánh dấu xong khi chưa sơn?") cần truy vết.

**Thiết kế:**
- **State machine rõ ràng**, chuyển trạng thái chỉ qua method của entity, không cho set thẳng `Status`. Chuyển sai (Queued → Delivered) → lỗi 409/422.
- Mỗi lần chuyển ghi **audit**: ai, lúc nào (UTC), từ trạng thái nào sang trạng thái nào, ghi chú/ảnh, thiết bị nào. Với tablet dùng chung → đăng nhập nhanh bằng **PIN theo người** để audit có nghĩa (hỏi PO).
- Chuyển trạng thái phát **domain event** (`JobBuilt`) → bước tiếp (cho phép lên lịch giao, báo khách) chạy qua **outbox** để không mất sự kiện khi DB commit mà gửi message lỗi.
- Bấm 2 lần / wifi chập chờn retry → chuyển trạng thái phải **idempotent**: đã `Built` mà nhận lại "mark Built" → trả OK, không ghi audit lần 2.

```csharp
public void MarkBuilt(Guid userId, DateTimeOffset now, string? note)
{
    if (Status == ProductionStatus.Built) return;              // retry → không làm gì
    if (Status != ProductionStatus.InProgress)
        throw new InvalidTransitionException(Status, ProductionStatus.Built);

    var from = Status;
    Status = ProductionStatus.Built;
    BuiltAt = now;
    _history.Add(new ProductionStatusChange(Id, from, Status, userId, now, note));
    AddDomainEvent(new JobBuilt(Id, OrderId));                 // → outbox
}
```

Audit lưu ở đâu: bảng `ProductionStatusChange` (append-only) là đủ cho lịch sử trạng thái; audit chung mọi field có thể dùng EF `SaveChangesInterceptor` (Joblogic lưu audit ở MongoDB). Không cần event sourcing cả hệ thống, nói được lý do là điểm cộng.

Câu mẫu:
> I'd model production status as an explicit state machine, so the only way to change it is through methods like `MarkBuilt`, which reject invalid transitions. Every transition writes an append-only history row with who, when in UTC, from and to, and an optional note or photo. Shop-floor tablets are often shared, so I'd ask the PO whether staff sign in with a quick PIN; otherwise the audit says "tablet 3" and that's not very useful in a dispute. Transitions are idempotent, because flaky Wi-Fi means the same tap can arrive twice, and the "job built" event goes through an outbox so scheduling and customer notifications are never lost.

#### D3.6.3 Lên lịch giao: ràng buộc + chống đặt quá (overbooking)

**Ràng buộc thực tế** (hỏi PO cái nào cần ngay, cái nào để sau):
- **Năng lực**: xe/tài xế chở tối đa N chuyến/ngày (shed to, mỗi chuyến 1–2 cái), có thể theo **kích thước** (shed 12x24 cần xe/thiết bị riêng).
- **Vùng giao**: theo ZIP/khoảng cách từ xưởng; ngoài vùng tính thêm phí theo dặm.
- **Cửa sổ thời gian**: sáng/chiều; khách phải có mặt hay không.
- **Điều kiện mặt bằng** (site readiness): nền đã san phẳng, lối vào đủ rộng, không vướng dây điện/cây → checklist trước giao; không đạt → giao lại, có phí.
- **Thứ tự phụ thuộc**: chỉ lên lịch khi `ReadyForDelivery` (hoặc dự kiến xong trước ngày giao) và **đã trả đủ tiền / RTO đã duyệt** (hỏi PO).
- Ngày giao là **ngày lịch + timezone xưởng** (xem 8.4).

**Chống đặt quá: bản chất là race condition "check-then-act".** Hai điều phối viên cùng thấy xe A ngày 05/11 còn 1 chỗ (2/3), cùng bấm lưu → 4/3. Đọc `COUNT(*)` rồi mới INSERT là sai, kể cả trong transaction ở mức Read Committed (cả hai đều đọc được 2).

Cách 1: **atomic UPDATE bộ đếm** (đơn giản, nhanh nhất). Có bảng `TruckDay(TruckId, Date, Capacity, Booked)`:

```csharp
await using var tx = await _db.Database.BeginTransactionAsync();

var rows = await _db.Database.ExecuteSqlInterpolatedAsync($@"
    UPDATE TruckDay SET Booked = Booked + 1
    WHERE TruckId = {truckId} AND Date = {date} AND Booked < Capacity");

if (rows == 0)
    throw new ConflictException("Truck is full on that day");   // → 409, UI gợi ý ngày khác

_db.Deliveries.Add(new Delivery(orderId, truckId, date, window));
await _db.SaveChangesAsync();
await tx.CommitAsync();
```

Câu `UPDATE ... WHERE Booked < Capacity` kiểm tra và tăng trong **một câu lệnh**; SQL Server giữ khoá ghi trên dòng đó tới hết transaction → người thứ hai phải chờ, sau đó điều kiện sai → 0 dòng. Huỷ/dời lịch → `Booked - 1` trong cùng transaction. Dòng `TruckDay` chưa có → tạo trước (job sinh lịch 60 ngày tới) hoặc `MERGE`/insert bắt lỗi unique.

Cách 2: **khoá dòng cha bằng `UPDLOCK`** khi ràng buộc phức tạp hơn một con số (tổng kích thước, cửa sổ thời gian không chồng nhau):

```sql
BEGIN TRAN;
SELECT * FROM TruckDay WITH (UPDLOCK, HOLDLOCK)
WHERE TruckId = @truckId AND Date = @date;   -- người thứ 2 chờ ở đây
-- đọc các Delivery của (xe, ngày), kiểm tra luật trong C#, rồi INSERT
COMMIT;
```

`UPDLOCK` để hai người không cùng đọc rồi cùng ghi; `HOLDLOCK` giữ tới cuối transaction (và khoá cả phạm vi nếu dòng chưa tồn tại). Transaction phải **ngắn** (không gọi API ngoài bên trong).

Cách 3: **rowversion trên `TruckDay`** (optimistic): đọc, kiểm tra luật, tăng `Booked`, lưu; xung đột → retry hoặc 409. Hợp khi ít tranh chấp.

Không dùng: `lock` trong C# (nhiều instance thì vô dụng), nâng cả transaction lên `Serializable` (deadlock nhiều), distributed lock Redis (DB đã có sẵn khoá, thêm Redis chỉ thêm điểm hỏng; Hiệp dùng RedLock ở Quest Engine vì ở đó không có một dòng DB chung để khoá).

Cách xác nhận bug có thật: test tích hợp bắn 10 request song song vào xe còn 1 chỗ (`Task.WhenAll`) với DB thật (Testcontainers) → đúng 1 thành công, 9 nhận 409. Trên production: query đếm `Delivery` theo (xe, ngày) > `Capacity`.

Câu mẫu:
> Overbooking is a classic check-then-act race: two dispatchers both see one slot left and both save. Counting in the application doesn't fix it, even inside a transaction. I'd keep a capacity row per truck per day and book with a single conditional update — `SET Booked = Booked + 1 WHERE Booked < Capacity` — in the same transaction as inserting the delivery. If zero rows were updated, the truck is full and we return a 409 with other dates. If the rules get richer, like total shed size or time windows, I'd lock that truck-day row with `UPDLOCK, HOLDLOCK`, check the rules and insert, keeping the transaction short. I'd prove it with an integration test that fires ten parallel bookings at the last slot and expects exactly one success.

#### D3.6.4 Driver app offline + đồng bộ lại

**Vấn đề.** Tài xế đi vùng nông thôn Mỹ, mất sóng. App phải chạy offline: xem lộ trình hôm nay, chụp ảnh, lấy chữ ký, ghi nhận thanh toán, rồi đồng bộ khi có mạng. Dữ liệu trên máy là **bản chụp** tại lúc tải; văn phòng có thể đổi lịch, đổi địa chỉ, huỷ đơn sau đó.

**Luồng xuống (văn phòng → máy):**
- Mỗi delivery có `Version` (tăng mỗi lần sửa). App lưu bản chụp + version vào SQLite trên máy.
- Văn phòng đổi lịch → tăng version, gửi **push** (FCM/APNS) "lộ trình đã đổi" → app có mạng thì kéo lại (pull) các delivery có version mới. Push chỉ là **tín hiệu**, không chứa dữ liệu, không đảm bảo tới → app vẫn kéo định kỳ và khi mở app.
- Thay đổi quan trọng với delivery đã giao cho tài xế → đánh dấu cần xác nhận lại (giống cờ **RedeployRequired** Hiệp làm ở Joblogic: hạn mức đổi sau khi visit đã deploy xuống thiết bị kỹ thuật viên, nên phải deploy lại). Văn phòng thấy "tài xế chưa nhận bản mới" → gọi điện.
- Chỉ tải phần thay đổi (delta theo version / `updatedSince`); dữ liệu tham chiếu thì so hash (Joblogic tính **library hash** để thiết bị chỉ tải lại thư viện đã đổi).

**Luồng lên (máy → server) và idempotency:**
- Mỗi hành động trên máy (xác nhận giao, thu tiền) sinh **`ClientOperationId` (GUID) ngay trên máy**, lưu vào hàng đợi outbox của app, gửi lại tới khi server trả thành công.
- Server lưu id đã xử lý (unique index) → nhận lại lần 2 thì trả kết quả cũ, **không thu tiền 2 lần** (cùng mẫu với Pragmatic idempotency của Hiệp).
- Ảnh gửi riêng, lớn: upload thẳng lên S3 bằng **presigned URL**, có thể resume; bản ghi xác nhận tham chiếu tới key ảnh.
- Ghi **thời điểm thực tế trên máy** (`OccurredAt`, kèm GPS) tách khỏi thời điểm server nhận (`ReceivedAt`), vì đồng bộ có thể muộn vài giờ.

**Xung đột** (văn phòng huỷ đơn trong khi tài xế đang offline giao xong): không có công thức chung, phải hỏi PO. Nguyên tắc: **sự kiện thực tế ngoài đời thắng** (shed đã nằm ở sân khách thì ghi nhận đã giao), nhưng tạo **cảnh báo cho văn phòng xử lý** thay vì máy tự gộp âm thầm. So version: lệnh từ máy mang `BaseVersion`; khác version hiện tại → đưa vào danh sách cần người xem.

```csharp
[HttpPost("deliveries/{id}/complete")]
public async Task<IActionResult> Complete(Guid id, CompleteDeliveryRequest req)
{
    var existing = await _db.ProcessedOperations.FindAsync(req.ClientOperationId);
    if (existing is not null) return Ok(existing.Result);       // retry → kết quả cũ

    var delivery = await _db.Deliveries.SingleAsync(d => d.Id == id);
    var outcome = delivery.Complete(req.OccurredAt, req.SignatureKey, req.PhotoKeys, req.BaseVersion);
    // outcome = Completed hoặc CompletedWithConflict (đơn đã bị huỷ/đổi) → tạo task cho văn phòng

    _db.ProcessedOperations.Add(new ProcessedOperation(req.ClientOperationId, outcome));
    await _db.SaveChangesAsync();   // cùng transaction; unique key chặn 2 request song song
    return Ok(outcome);
}
```

Thu tiền tại chỗ: tốt nhất qua thiết bị/SDK của payment provider (Stripe Terminal…), tiền thật do provider xác nhận qua webhook; app chỉ ghi "đã nhận séc/tiền mặt" kèm ảnh → kế toán đối soát. Không để app offline tự quyết định số dư.

Câu mẫu:
> I'd treat what's on the driver's phone as a snapshot with a version number. When the office reschedules, we bump the version and send a push, but the push is only a hint; the app also pulls changes whenever it's online, and the office can see which drivers haven't picked up the latest version. It's the same idea as the "redeploy required" flag I built at Joblogic, where engineers' devices held a copy of the visit. Going the other way, every action on the phone gets an operation ID created on the device, and the server stores processed IDs, so a retry after a dropped connection never records a delivery or a payment twice. If the office cancelled an order that the driver had already delivered offline, I wouldn't merge it silently: the real-world event wins, and we raise a task for the office.

#### D3.6.5 Thông báo khách (SMS/email)

**Khi nào gửi:** đã lên lịch giao (ngày + cửa sổ giờ), nhắc trước 1–2 ngày (nhắc chuẩn bị mặt bằng), "tài xế đang trên đường" (tuỳ), đã giao xong (kèm ảnh, link hoá đơn/số dư), đổi lịch/huỷ.

**Thiết kế:**
- Gửi **qua queue/background**, không gọi Twilio/SendGrid trong request lên lịch: provider chậm/lỗi không được làm hỏng việc lưu lịch. Sự kiện `DeliveryScheduled` → outbox → worker gửi.
- **Idempotent**: key = `(DeliveryId, NotificationType, ScheduleVersion)`, unique index trên bảng `NotificationLog`. Queue at-least-once gửi lại message → kiểm tra log, không nhắn khách 2 lần. Đổi lịch → version mới → tin mới hợp lệ.
- **Nhắc trước ngày giao**: job định kỳ quét delivery ngày mai **theo timezone của khách/xưởng**, gửi trong giờ hợp lý (không nhắn 6 giờ sáng); trước khi gửi kiểm tra lại lịch còn đúng không (đã dời thì bỏ).
- **Opt-out / đồng ý**: Mỹ có luật **TCPA** (SMS cần đồng ý), trả lời **STOP** phải ngừng (Twilio tự xử lý STOP và báo lại) → lưu trạng thái đồng ý theo kênh; email marketing khác email giao dịch. Mình không phải luật sư → "check with the PO/legal", nhưng biết từ khoá là điểm cộng.
- Template theo tenant (tên công ty bán shed, logo), số điện thoại theo định dạng **E.164** (`+1…`).
- Retry có backoff khi provider lỗi tạm thời; lỗi vĩnh viễn (số sai) → ghi lại, hiện cho văn phòng; dead-letter queue.
- Lưu lịch sử gửi (đã gửi, đã tới, thất bại từ webhook trạng thái của provider) → hỗ trợ trả lời "tôi không nhận được tin".

```csharp
public async Task Handle(DeliveryScheduled e, CancellationToken ct)
{
    var key = $"{e.DeliveryId}:{NotificationType.Scheduled}:{e.ScheduleVersion}";
    if (await _db.NotificationLogs.AnyAsync(n => n.Key == key, ct)) return;   // đã gửi

    var customer = await _customers.GetAsync(e.CustomerId, ct);
    if (!customer.SmsConsent) return;                                          // tôn trọng opt-out

    var msgId = await _sms.SendAsync(customer.PhoneE164, _templates.Render(e), ct);
    _db.NotificationLogs.Add(new NotificationLog(key, msgId, _time.GetUtcNow()));
    await _db.SaveChangesAsync(ct);   // unique index trên Key chặn worker song song
}
```

Lưu ý trung thực: giữa "đã gửi SMS" và "đã ghi log" vẫn có khe nhỏ (crash đúng lúc đó → gửi lại 1 lần). Gửi tin nhắn ra ngoài không thể exactly-once tuyệt đối; giảm bằng cách ghi log trạng thái `Sending` trước, hoặc truyền idempotency key cho provider nếu provider hỗ trợ. Nói được giới hạn này là mức Senior.

Câu mẫu:
> Notifications are a side effect, so they shouldn't be able to break scheduling. The scheduling transaction writes an event to an outbox, and a worker sends the SMS or email. The queue delivers at least once, so each message has a key — delivery, notification type and schedule version — with a unique index, so a redelivered message doesn't text the customer twice, but a reschedule still sends a new one. Reminders run per the customer's time zone at a sensible hour, and re-check the schedule just before sending. We store consent per channel and honour STOP replies, which matters in the US under TCPA. Strictly speaking, sending to an external provider can't be exactly-once, so I'd aim for "at most one duplicate in a rare crash" and log every send for support.

#### D3.6.6 Câu hỏi luyện + tự kiểm tra (Mid vs Senior)

1. *Two managers reorder the production queue at the same time. What happens?*
   Mid: "dùng transaction". Senior: đặt tên lost update, rowversion → 409 + refresh, SignalR, cân nhắc version theo cả hàng đợi.
2. *How would you prevent overbooking a delivery truck?*
   Mid: "kiểm tra số lượng trước khi lưu". Senior: gọi tên check-then-act race, atomic conditional UPDATE / `UPDLOCK`, vì sao `lock` C# và Serializable không ổn, test song song chứng minh.
3. *The office reschedules a delivery while the driver is offline.* → version + push là tín hiệu + pull + cảnh báo khi tài xế chưa nhận, xung đột cho người xử lý.
4. *The driver app retried and the payment was recorded twice. How do you fix and prevent it?* → idempotency key sinh trên máy, unique index, script sửa dữ liệu có audit, báo PO số đơn bị ảnh hưởng.
5. *A customer says they got the delivery SMS three times.* → at-least-once queue không có khoá idempotent; thêm `NotificationLog` unique key; kiểm tra log provider; nói về giới hạn exactly-once.
6. *How do you know who marked a shed as built?* → state machine + bảng history append-only + đăng nhập PIN trên tablet dùng chung.
7. *What would you ask the PO before building delivery scheduling?* → năng lực tính theo chuyến hay kích thước, vùng giao và phí, có yêu cầu trả đủ tiền trước giao không, site readiness, ai được dời lịch, thông báo khách những lúc nào, giao lại có phí không.

### D3.7 Inventory
- Hàng có sẵn bán ngay; trạng thái Available → Reserved (đang có quote/order giữ) → Sold. Chống bán 2 lần: atomic UPDATE `WHERE Status='Available'` hoặc rowversion.
- Giữ chỗ có hạn (reservation expiry) → job nền giải phóng.

### D3.8 Multi-tenant settings
Mỗi công ty bán shed là một tenant (có store/region bên trong): cấu hình thuế, template, quy trình, RTO provider được bật, feature theo gói. Cô lập dữ liệu → section 17.

### D3.9 Tích hợp bên thứ ba (phạm vi chung)
Payment provider, API thuế, công ty RTO, configurator 3D/website bán hàng, SMS/email, kế toán (QuickBooks…), Zapier/webhook ra ngoài. Nguyên tắc → section 22.

### D3.10 Câu hỏi luyện (domain)
1. Walk me through how a quote becomes a delivered order. What data changes at each step?
2. A customer paid a deposit, then the quote was revised. How do you keep the balance due correct?
3. Balance due is wrong for some orders. How do you investigate and fix? (xem 9.2)
4. Prices go up after a quote was sent. What happens to the quote?
5. How would you store money and handle rounding?
6. How do you calculate a rent-to-own payment schedule so the total matches exactly?
7. Delivery dates show one day off for some customers. Why, and how do you fix it?
8. How do you store and display dates across North American time zones?
9. A contract was signed and then the template changed. A customer disputes it a year later. What do you show?
10. PDF generation takes 10 seconds and sometimes breaks with special characters. How do you fix it?
11. Two dealers try to sell the same inventory unit at the same time. What happens?
12. The driver app is offline when the office reschedules a delivery. How do you handle it?
13. How would you prevent overbooking a delivery truck?
14. How would you model order statuses and who can change them?
15. How would you add a new RTO provider?
16. What would you ask the PM before building "cancel order"?
17. How do you make sure every change to an order is traceable?
18. Sales tax: whose address, when is it locked, what if the rate changes?
19. Markup vs margin — what's the difference? Which would the dealer see?
20. How would you design an owner/customer portal that shows payments and balance? (Urbanise có owner portal — dễ bị hỏi)

---

## D4. Câu hỏi PO ⏳

> ⏳ **Chưa viết lại sâu.** Dưới đây là nội dung bản cũ (số tham chiếu section bên trong là số bản cũ, xem bảng đối chiếu ở 0.2). Claude sẽ viết lại trước khi Hiệp học tới.

🟢 Nối value: **Driven by Customer Success** (xem mục tiêu của khách như của mình, khách nội bộ gồm cả PM), **1% Improvement** (từng phân đoạn thay vì phiên bản hoàn hảo, linh hoạt khi đổi yêu cầu), **Enjoy Problem Solving** (80/20, biết hỏi giúp), **Be Accountable** (báo sớm, chính trực).
Khung: **làm rõ (hỏi lại) → đề xuất phương án nhỏ giao trước → edge case → đo kết quả**. PO đánh giá: hiểu "vì sao", hỏi đúng câu, giao tiếp rõ, không tự ý làm thêm, chịu trách nhiệm.

### D4.1 Bảng tình huống
| Câu hỏi | Ý chính |
|---|---|
| Quote đã gửi, bảng giá tăng | Quote là snapshot có hạn; giữ giá tới hết hạn; muốn cập nhật thì tạo **revision** mới, khách thấy so sánh. Hỏi PO chính sách |
| Balance due sai ở một số đơn | Lấy danh sách đơn sai, tìm điểm chung (có refund? đổi thuế? sửa đơn sau deposit? làm tròn?), so ledger vs số lưu, sửa công thức + **script sửa dữ liệu có audit**, test hồi quy, báo khách bị ảnh hưởng |
| Huỷ đơn khi đã vào sản xuất | Hỏi: phí huỷ? hoàn deposit bao nhiêu? sản phẩm dở thành inventory? ai được duyệt? thông báo ai? RTO contract huỷ thế nào? có giới hạn thời gian? |
| Ngày giao lệch 1 ngày | Section 8.4 |
| Yêu cầu mơ hồ | Hỏi "vấn đề người dùng là gì", viết acceptance criteria + ví dụ cụ thể (Given/When/Then), mock nhanh, xác nhận lại trước khi code |
| Đổi yêu cầu giữa sprint | Nêu ảnh hưởng (thời gian, rủi ro), để PO chọn đổi phạm vi; không âm thầm làm thêm |
| Feature lớn | Cắt **lát dọc** (vertical slice), feature flag, giao bản tối thiểu dùng được trước ("1% improvements") |
| Không đồng ý với PO | Đưa dữ liệu/rủi ro, đề xuất phương án thay thế; PO quyết về giá trị, dev chịu trách nhiệm về cách làm; quyết xong thì cam kết |
| Ưu tiên bug vs feature | Theo tác động: tiền sai / dữ liệu sai / khách bị chặn trước; còn lại vào backlog có mức ưu tiên |
| Ước lượng | Chia nhỏ, nêu giả định và rủi ro, khoảng (range) thay vì một con số, cập nhật sớm khi lệch |
| Trễ deadline | Báo sớm, nêu nguyên nhân, đề xuất cắt phạm vi hoặc lùi ngày, không im lặng |
| Khách yêu cầu tính năng chỉ cho họ | Hỏi vấn đề gốc; có thể giải bằng cấu hình chung theo tenant thay vì code riêng |
| Feature đã release mà không ai dùng | Đo (analytics), hỏi người dùng, cải thiện hoặc gỡ |
| PO muốn làm nhanh, bạn thấy rủi ro kỹ thuật | Nêu rủi ro cụ thể (mất tiền, mất dữ liệu), đề xuất phương án nhỏ an toàn, ghi lại nợ kỹ thuật có ticket |

### D4.2 Câu mẫu "balance due sai"
> First I'd get the list of affected orders and look for what they have in common — refunds, a tax change, an edit after the deposit, or a rounding difference. I'd compare the stored balance with what the payment ledger says, find the rule that's wrong, and write a failing test for it. Then I'd fix the calculation, and correct the affected orders with a reviewed script that writes audit entries, so we can explain every change. Finally I'd tell the PM how many customers were affected, so support can contact them if needed.

### D4.3 Câu mẫu "yêu cầu mơ hồ"
> I'd start by asking what problem the user has, not how the screen should look. Then I'd write acceptance criteria with two or three concrete examples, including the awkward ones — a partial payment, a cancelled order, a different time zone — and confirm them with you before I start. If it's still unclear, I'd build the smallest version behind a feature flag and get feedback early.

### D4.4 Câu mẫu "làm việc với PM"
> I like being involved early, when a feature is still a problem rather than a spec, because that's when edge cases are cheap to find. At Joblogic, the spend-limit feature looked simple until we walked through real scenarios — later visits and data already on engineers' devices. At PlaySweeps, the client designed the quest formulas and I clarified the requirements with them before writing the technical design.

### D4.5 Edge case checklist (dùng cho mọi feature PO hỏi)
- Null / rỗng / rất lớn / số âm / 0.
- Trùng (double click, retry, webhook gửi 2 lần).
- Đồng thời (2 người sửa, 2 đại lý bán cùng một hàng).
- Thời gian (múi giờ, DST, cuối tháng, hết hạn, quá khứ).
- Tiền (làm tròn, refund, trả quá, tiền tệ, thuế đổi).
- Trạng thái (huỷ giữa chừng, sửa sau khi khoá, quay lại bước trước).
- Quyền (ai được làm, tenant khác, store khác).
- Tích hợp lỗi (bên thứ ba chậm/sập/trả sai).
- Dữ liệu cũ (record tạo trước khi có feature → migration/backfill).
- Thông báo (gửi ai, gửi mấy lần, opt-out).
- Báo cáo/audit (ai cần thấy thay đổi này).

### D4.6 Câu hỏi luyện (PO)
1. How do you work with a product manager?
2. A requirement is unclear. What do you do?
3. The requirement changes in the middle of the sprint. What do you do?
4. How do you break a large feature into deliverable pieces?
5. You disagree with a product decision. What do you do?
6. How do you prioritise bugs against new features?
7. How do you estimate? What if you're wrong?
8. You'll miss a deadline. When and how do you tell me?
9. A customer reports wrong numbers. Walk me through your response.
10. What would you ask me before building "cancel order" / "reschedule delivery" / "partial refund"?
11. How do you know a feature you shipped was successful?
12. What does "1% improvements" mean to you? Give an example.
13. Tell me about a time you found an edge case nobody had thought of.
14. How do you explain a technical problem to a non-technical person?
15. Give an example of taking ownership beyond your task.

---

## D5. Refactoring và tiếp quản code từ đối tác Mỹ ⏳

> ⏳ **Chưa viết lại sâu.** Dưới đây là nội dung bản cũ (số tham chiếu section bên trong là số bản cũ, xem bảng đối chiếu ở 0.2). Claude sẽ viết lại trước khi Hiệp học tới.

JD ghi thẳng "taking over from a US partner". Gần như chắc chắn có câu "2 tuần đầu".

### D5.1 Code smell hay gặp & cách sửa
| Smell | Refactoring |
|---|---|
| Method dài, controller béo | Extract Method / Extract Class → service/handler |
| `switch` theo loại lặp ở nhiều nơi | Replace Conditional with Polymorphism (Strategy) |
| Primitive obsession (`decimal price`, `string status`) | Value object `Money(amount, currency)`, enum/state |
| Logic tính tiền lặp ở UI, PDF, API | Gom về 1 domain service; PDF đọc kết quả đã tính |
| `DateTime.Now` khắp nơi | Inject `TimeProvider` (.NET 8) |
| God class / static helper | Tách theo use case, DI |
| Feature envy (method dùng dữ liệu của class khác nhiều hơn của mình) | Move Method |
| Shotgun surgery (một thay đổi phải sửa nhiều nơi) | Gom trách nhiệm |
| Comment giải thích code rối | Đổi tên, tách hàm |
| Dead code, code bị comment | Xoá (git giữ lịch sử) |
| `ToList()` sớm, N+1, query trong vòng lặp | Projection, Include, batch |
| `catch (Exception) {}` | Xử lý cụ thể + log |

### D5.2 Cách refactor an toàn (nói theo thứ tự)
1. **Characterization test** (golden master): test chụp lại hành vi hiện tại (kể cả "lạ") trước khi sửa. Ví dụ: chạy 200 quote mẫu, lưu kết quả tổng tiền, so sánh sau refactor.
2. **Bước nhỏ**, mỗi commit một thay đổi, chạy test sau mỗi bước; **tách PR refactor và PR đổi hành vi**.
3. Tạo **seam**: interface quanh phụ thuộc khó test (DB, thời gian, API ngoài) để chèn test double.
4. **Strangler fig**: phần mới viết cạnh phần cũ, chuyển dần route/feature, **feature flag** để quay lại.
5. **Branch by abstraction**: đưa interface vào trước, hai implementation song song, chuyển dần.
6. Đo trước/sau nếu refactor vì performance.
7. **Không big-bang rewrite** (rủi ro cao, mất tri thức nghiệp vụ ẩn trong code cũ).

### D5.3 "2 tuần đầu khi tiếp quản" — câu mẫu
> In the first two weeks I'd focus on understanding before changing. First, get the system running locally and through the deployment pipeline, and get access to logs and monitoring. Second, map the main business flows end to end — quote, order, contract, production, delivery — with the PM, and draw a simple architecture and data diagram. Third, ask the US partner for a knowledge-transfer session with a prepared list of questions: known bugs, risky areas, why certain decisions were made, how deployments and secrets are managed. Fourth, pick up a few small bugs so I learn the code by working in it. And I'd write down what I find as living documentation. I won't start a big rewrite; improvements go in small steps backed by tests. I did something similar at PlaySweeps when I took over the Socure KYC integration from a colleague: I studied the vendor dashboard and decision module, found that the initial prototype had wrong assumptions, and reworked it until it ran stably in production.

Danh sách câu hỏi chuẩn bị cho buổi bàn giao với partner Mỹ:
- Kiến trúc, môi trường (dev/staging/prod), cách deploy, ai giữ secret/tài khoản cloud.
- Known bugs, vùng rủi ro, phần "đừng đụng vào".
- Test hiện có, coverage, test chạy ở đâu.
- Tích hợp bên thứ ba: tài khoản, webhook, giới hạn, liên hệ.
- Job nền, cron, cách vận hành khi lỗi; runbook sự cố.
- Quyết định kiến trúc quan trọng và lý do (ADR nếu có).
- Dữ liệu: schema, migration, backup/restore, dữ liệu nhạy cảm.
- Khi nào họ còn hỗ trợ, kênh liên lạc, chênh múi giờ.

Khi tiếp quản legacy, kiểm tra kỹ thuật đầu tiên: FK có index không, `ToList()` sớm/client evaluation (EF ≤ 2), `.Result`/`.Wait()`, `DateTime.Now`, `double` cho tiền, secret trong code/config, log, test.

### D5.4 "Bug gấp trên production, code chưa có test"
> First I'd reproduce it and limit the impact — for example a feature flag or a data fix if customers are blocked. Then I'd write a test that reproduces the bug, even a narrow one, make the smallest fix that passes it, and get a review. After the hotfix, I'd add a follow-up ticket to cover that area properly and look for the root cause, not only the symptom.

### D5.5 "Code của partner chất lượng kém, bạn làm gì?"
> I'd avoid judging it before I understand the constraints they had. I'd list the problems by business risk — for example money calculations without tests come first, naming issues last — agree the priorities with the PM, and improve the risky areas in small steps alongside feature work, rather than asking for a separate rewrite project.

### D5.6 Câu hỏi luyện
1. You inherit a codebase from a US partner with no tests. What do you do in the first two weeks?
2. How do you refactor a 400-line controller action safely?
3. What's a characterization test?
4. Explain the strangler fig pattern. When would you use it here?
5. Production bug, no tests, customers blocked. Walk me through it.
6. How do you convince the PM to spend time on refactoring? (gắn với rủi ro/tốc độ giao feature, làm kèm feature, đo bằng số bug/thời gian)
7. The previous team made a design decision you disagree with. What do you do?
8. How do you document a system you're learning?
9. What code smells do you look for first?
10. Rewrite or refactor? When is a rewrite justified?

---

## D6. Behavioral STAR (tiếng Anh) ⏳

> ⏳ **Chưa viết lại sâu.** Dưới đây là nội dung bản cũ (số tham chiếu section bên trong là số bản cũ, xem bảng đối chiếu ở 0.2). Claude sẽ viết lại trước khi Hiệp học tới.

🟢 Bộ câu chuyện theo từng core value (và bảng câu chuyện × value) nằm ở `notes/S-seadev-culture.md` mục 3 và 5 — dùng chung cho cả vòng tech.
STAR: **Situation** (1–2 câu) → **Task** (1 câu) → **Action** (nhiều nhất, dùng "I") → **Result** (con số, hậu quả) → bài học. 60–90 giây.

### D6.1 Bộ câu chuyện
| Câu hỏi | Chất liệu | Ghi chú |
|---|---|---|
| Inherited a system / hard to maintain (Q141) | **Socure KYC**: tiếp quản từ đồng nghiệp, tự đọc dashboard/decision module, prototype client có giả định sai, sửa đến khi ổn định | Kể rõ giả định sai là gì **[Hiệp điền chi tiết]** |
| Led a feature end to end | **Quest Engine V2**: TDD, Cosmos, Redis lock, idempotency claim, lên prod | Có thể nói số project/ticket |
| Hardest production bug / on-call (Q137) | Incident điều tra bằng App Insights + Loki + Splunk | **[Hiệp điền: 1 vụ cụ thể, triệu chứng, công cụ, nguyên nhân, fix, con số]** |
| Bug không tái hiện ở local (Q142) | Dùng Splunk BI event để dựng lại hành trình user | **[Hiệp điền]** |
| Performance problem (Q138) | Tối ưu fetch/cache AVA config | **[Hiệp điền con số trước/sau]** |
| Edge case from understanding business | **Job Spend Limit** (visit 2+, RedeployRequired) | Câu mẫu ở 2.2 |
| Disagreement with a technical decision (Q140) | **[Hiệp điền]** — gợi ý: lock vs DB constraint, sync vs async reward | Kết: đưa dữ liệu, chấp nhận quyết định chung |
| Incident caused by a design decision (Q139) | **[Hiệp điền]** — gợi ý: mirror balance ghi giá trị tuyệt đối | Nói bài học, không đổ lỗi |
| Working remotely with a foreign team | PLAYSTUDIOS (Mỹ): Slack hằng ngày, họp technical design; Joblogic (UK): code review Azure DevOps | Chênh múi giờ, giao tiếp async |
| Learning quickly | Go + AWS (KMS, S3, SES) ở Altar; Rive với designer nước ngoài | JD: "learn quickly and adapt" |
| Proactive improvement / 1% | Exponential rate limiting cho API nhạy cảm; tối ưu cache AVA | |
| Mentoring / leading | Lead nhóm 4 intern ở Astraler; review PR feature mình lead | |
| Failure / mistake | **[Hiệp điền]** — chọn lỗi thật, nhỏ, đã rút kinh nghiệm | Không chọn lỗi làm mất tiền khách lớn |
| Tight deadline | **[Hiệp điền]** | |
| Conflict with a colleague | **[Hiệp điền]** | Tập trung vào vấn đề, không vào người |
| Handover from client with good feedback | Altar: client phản hồi tốt khi bàn giao | |

### D6.2 Mẫu Socure (điền chi tiết thật trước khi dùng)
> **S:** At PlaySweeps we needed identity verification for US players, using Socure — document checks, SSN verification and manual review. The first integration had been started by a colleague, based on a prototype from the client. **T:** I took over the integration and had to get it working reliably in production. **A:** I didn't know Socure, so I studied their dashboard and decision module and compared what the vendor actually returned with what the prototype assumed. I found the prototype's assumptions were wrong [Hiệp điền: ví dụ cụ thể], so I reworked the flow, handled the different decision outcomes explicitly, and tested the edge cases with the client's team. **R:** The KYC flow then ran stably in production for all US players. **Lesson:** when taking over an integration, verify the vendor's real behaviour instead of trusting the existing code.

### D6.3 Tiếng Anh — lỗi hay mắc
- **-s ngôi 3**: "it depends", "the service calls", "the user pays".
- Không "is depend", không "will be encountered" (bị động thừa) → "we'll hit this problem".
- Dùng thì quá khứ khi kể: "I built", "we found", "it ran".
- Câu ngắn, mỗi câu một ý. Khi chưa nghe rõ: "Sorry, could you repeat the last part?" / "Just to make sure I understand, you're asking about…".
- Khi cần nghĩ: "That's a good question — let me think for a second."
- Khi không biết: "I haven't used that directly, but here's how I'd approach it…"

### D6.4 Câu hỏi luyện
1. Tell me about the most difficult production bug you investigated.
2. Tell me about a performance problem you solved.
3. Tell me about a production incident caused by a design decision.
4. Tell me about a time you disagreed with a technical decision.
5. Tell me about a system you inherited that was difficult to maintain.
6. Tell me about a bug you couldn't reproduce locally.
7. Tell me about a feature you led from design to release.
8. Tell me about a mistake you made and what you learned.
9. Tell me about working with a team in another time zone.
10. Tell me about a time you learned a new technology quickly.
11. Tell me about a time you improved something nobody asked you to.
12. Tell me about a time you had to push back on a deadline or requirement.

---

## D7. Git, Agile/Scrum, làm việc remote với Mỹ ⏳

> ⏳ **Chưa viết lại sâu.** Dưới đây là nội dung bản cũ (số tham chiếu section bên trong là số bản cũ, xem bảng đối chiếu ở 0.2). Claude sẽ viết lại trước khi Hiệp học tới.

- **Workflow**: feature branch → PR → review → merge vào main; trunk-based (nhánh ngắn, feature flag) vs GitFlow (develop/release/hotfix). Joblogic: Azure DevOps PR + nhánh uat; PlaySweeps: review chéo PR.
- **merge vs rebase**: merge giữ lịch sử thật (merge commit); rebase viết lại commit lên đầu nhánh mới → lịch sử thẳng. **Không rebase/force-push nhánh chung.** `--force-with-lease` an toàn hơn `--force` trên nhánh của mình.
- **Squash merge**: gộp PR thành 1 commit trên main.
- **revert vs reset**: `revert` tạo commit đảo ngược (an toàn cho nhánh đã push/prod); `reset` dời con trỏ (chỉ dùng local). `reset --soft/--mixed/--hard`.
- **cherry-pick**: lấy một commit sang nhánh khác (hotfix sang release branch).
- **Conflict**: hiểu cả hai thay đổi, hỏi tác giả nếu cần, chạy test sau khi giải.
- `git stash`, `git bisect` (tìm commit gây lỗi bằng nhị phân), `git blame` (hiểu ngữ cảnh, không để đổ lỗi), `git reflog` (cứu commit "mất"), tag cho release.
- Commit message rõ (imperative, giải thích vì sao), commit nhỏ có ý nghĩa; Conventional Commits.
- `.gitignore`, không commit secret (nếu lỡ: xoay secret ngay, xoá lịch sử là phụ).
- Branch protection, required reviewers, CI pass.

Câu hỏi luyện:
1. Merge vs rebase — when each?
2. How do you undo a commit that's already in production?
3. How do you ship a hotfix to a release branch?
4. You committed a secret. What do you do?
5. How do you find which commit introduced a bug? (`git bisect`)
6. What branching strategy do you prefer and why?
7. How do you resolve a conflict in a file you don't own?

- **Scrum**: sprint (1–2 tuần), sprint planning, daily stand-up (đã làm gì, sẽ làm gì, vướng gì), sprint review/demo, retrospective, backlog refinement. Vai trò: PO (giá trị, ưu tiên), Scrum Master (quy trình), Dev team (cách làm).
- **Kanban**: luồng liên tục, giới hạn WIP — hợp team vận hành/bảo trì.
- **User story** "As a [role], I want [x] so that [y]" + **acceptance criteria** (Given/When/Then); **INVEST**.
- **Estimate**: story point (độ phức tạp tương đối, planning poker) vs giờ; velocity; nêu giả định, chia nhỏ, spike cho việc chưa rõ.
- **Definition of Ready / Done**: DoD = code + test + review + deploy staging + tài liệu/monitoring.
- **Tech debt**: ghi ticket, dành % mỗi sprint, gắn với rủi ro/tốc độ.
- PlaySweeps: Scrum + Jira (~354 ticket WIN-xxxx).
- **Remote với Mỹ** (chênh ~11–15 giờ với Việt Nam tuỳ múi giờ và DST): giao tiếp **async** viết rõ (bối cảnh, câu hỏi cụ thể, phương án đề xuất để họ chỉ cần chọn), gom câu hỏi trước giờ trùng nhau, ghi lại quyết định, demo bằng video/ảnh, không để bị chặn: làm phần khác trong lúc chờ, nêu giả định rõ.
- Câu mẫu:
> With a 12-hour gap, I try to make every message self-contained: the context, the specific question, and my proposed option, so the PM can just say yes or pick another option when they wake up. While I wait, I keep working on parts that don't depend on the answer, and I write down my assumption so it's easy to adjust. At PlaySweeps I worked daily with the PLAYSTUDIOS team in the US over Slack and joined technical design meetings in the overlap hours.

Câu hỏi luyện:
1. Describe your Scrum process in your last team.
2. How do you estimate a story? What if the estimate is wrong?
3. What's your Definition of Done?
4. How do you handle tech debt in sprints?
5. How do you work with a team 12 hours behind?
6. What makes a good user story / acceptance criteria?
7. What do you do in a retrospective when something went badly?

---

## D8. Câu hỏi ngược cho interviewer ⏳

> ⏳ **Chưa viết lại sâu.** Dưới đây là nội dung bản cũ (số tham chiếu section bên trong là số bản cũ, xem bảng đối chiếu ở 0.2). Claude sẽ viết lại trước khi Hiệp học tới.

Chọn 2–3 câu mỗi người, đừng hỏi những gì JD đã ghi.

Cho SA:
1. What does the current architecture of the Ops Hub look like — monolith or services, MVC or a React front end — and which parts are you most concerned about after the handover from the US partner?
2. What does the CI/CD and release process look like today, and what would you most like to improve first?
3. Who owns the API contract between the front end and the back end, and how are changes coordinated?
4. Is the plan to keep building on the existing codebase or to gradually modernise parts of it?
5. How is testing set up today, and what level of coverage do the critical money flows have?
6. What would you most like a new developer to improve in the codebase in the first three months?
7. How are architecture decisions made between Seadev and the US partner?

Cho PO:
1. What are the biggest pain points your customers report in the Ops Hub right now?
2. How do you and the developers work together — how early am I involved in shaping a feature?
3. What would a successful first three months look like for this role?
4. How do you measure whether a feature was successful?
5. What's on the roadmap for the next six months?

Gắn core value (dùng được cho cả SA/PO):
- How do 1% improvements usually happen in this team — can a developer just propose a small refactor or process change?
- When something goes wrong in production, how does the team handle it — what does "coach, not police" look like in practice?

Chung (cuối buổi):
- What are the next steps in the process?
- Is there anything in my background you'd like me to clarify?

Tránh: lương/phúc lợi ở vòng tech (để HR), câu hỏi lộ ra là đã đọc release notes nội bộ của ShedPro, câu hỏi về hồ sơ cá nhân interviewer.

---

## D9. Checklist trước giờ phỏng vấn, phụ lục ⏳

> ⏳ **Chưa viết lại sâu.** Dưới đây là nội dung bản cũ (số tham chiếu section bên trong là số bản cũ, xem bảng đối chiếu ở 0.2). Claude sẽ viết lại trước khi Hiệp học tới.

### D9.1 Một ngày trước
- [ ] Đọc lại section 1, 2 (pitch, câu chuyện), nói to 2 lần.
- [ ] Điền hết các chỗ **[Hiệp điền]** (incident on-call, Socure chi tiết, lương, bất đồng, sai lầm).
- [ ] Đọc bảng 0.2, xem lướt "Câu hỏi luyện" của mọi section.
- [ ] Chuẩn bị giấy/bảng trắng (vẽ kiến trúc), nước, tai nghe; test mic/camera nếu online.
- [ ] Mở sẵn CV (bản đã gửi) để khớp chính xác.

### D9.2 Lỗi Hiệp hay mắc — tự nhắc
- Check-then-act → luôn nói "**INSERT with a UNIQUE constraint in the same transaction**" hoặc atomic UPDATE.
- Trùng request → **replay response cũ**, không trả lỗi.
- Message liên quan tiền/hợp đồng **không được mất** → outbox / at-least-once + idempotent.
- Nhầm **Outbox với Mediator** (mediator là in-process).
- Nêu **trade-off** (sync vs async, monolith vs service), không trả lời một chiều.
- Sự cố: **tên vấn đề + công cụ điều tra + xử lý tạm + xử lý gốc + phòng ngừa**.
- Đưa **con số** (2M+ player, ~150 project, ~1.330 commit, ~200 file test, ~30 service, 10 loại chi phí).
- Diễn đạt chính xác cơ chế (vd. thread pool **bơm thread chậm**, không phải "tạo quá nhiều thread").
- Chọn key idempotency đúng độ mịn.
- Tiếng Anh: "-s" ngôi 3, không "is depend", tránh bị động thừa.
- Không nhắc chi tiết nội bộ ShedPro; không chê code Joblogic; nói đúng công nghệ thật (EF6, MSTest, Vue, Jenkins/Helm config).
- Không nói quá về CI/CD, AWS, microservice architecture.
- Interviewer gốc frontend → tôn trọng UX, không coi nhẹ FE.
- Không biết thì nói thật + cách tiếp cận (= value **Be Accountable / chính trực**).
- Khi kể sự cố/bất đồng: **coach, not police**, không đổ lỗi, không nói xấu người khác (value **Love our People**).

### D9.3 Trong phòng
- Nghe hết câu hỏi, hỏi lại nếu chưa rõ ("Just to make sure…").
- Trả lời ngắn trước (1–2 câu), rồi hỏi "Would you like me to go deeper into X?".
- Vẽ khi nói kiến trúc.
- Ghi chú câu hỏi để hỏi ngược.

### D9.1 Bảng con số của Hiệp
| Số | Ý nghĩa |
|---|---|
| ~4 năm | Kinh nghiệm (từ 07/2022) |
| 2M+ | Registered players PlaySweeps |
| ~150 | Project trong backend PlaySweeps |
| ~1.330 | Commit backend của Hiệp (nhiều nhất team) |
| ~340 | Commit web React của Hiệp |
| ~200 | File test xUnit + Moq |
| ~354 | Ticket Jira |
| 3 | TDD đã viết (Quest Engine V2, Banner System, CRM Direct-Target Offers) |
| ~30 | Service (Azure Functions) ở Joblogic |
| ~139 | Commit Joblogic |
| 4 | Feature lớn ở Joblogic |
| 10 | Loại chi phí trong Cost Breakdown |
| 39 / 46 / 26 | Module / entity / migration ở EIM |
| 4 | Intern Hiệp lead ở Astraler |

### D9.2 Câu tiếng Anh hữu dụng
- "Let me make sure I understand the question…"
- "There are two options here, and the trade-off is…"
- "In my last project we did X; for the Ops Hub I'd assume Y and confirm with the PM."
- "I haven't used that directly, but here's how I'd approach it."
- "The short answer is…, and the reason is…"
- "If I had to pick one, I'd go with… because…"
- "What I'd do differently next time is…"
- "That's a good point — I hadn't considered that. In that case I'd…"

### D9.3 Thuật ngữ nhanh (EN → VI)
idempotent (gọi nhiều lần cùng kết quả) · race condition (tranh chấp) · lost update (mất cập nhật) · optimistic concurrency (khoá lạc quan) · backfill (điền dữ liệu cũ) · expand/contract (mở rộng rồi thu gọn schema) · characterization test (test chụp hành vi) · strangler fig (thay dần) · seam (điểm chèn) · noisy neighbor (tenant gây ồn) · graceful degradation (suy giảm êm) · circuit breaker (ngắt mạch) · dead-letter queue (hàng chờ chết) · outbox (hộp thư đi) · ledger (sổ cái) · snapshot (bản chụp) · balance due (số còn nợ) · down payment / deposit (đặt cọc) · installment (kỳ trả góp) · eligibility (đủ điều kiện) · audit trail (dấu vết kiểm toán) · feature flag (cờ tính năng) · rollback (quay lui) · blue/green (hai môi trường xanh/lục) · canary (thả dần) · presigned URL (URL ký sẵn).

### D9.4 Đối chiếu JD → section (kiểm tra không sót)
| Yêu cầu JD | Section |
|---|---|
| ≥ 4 năm C#/.NET, .NET Core | 1.2, 11, 12, 13 |
| ASP.NET MVC và/hoặc Web API | 13, 14, 4 |
| AWS / cloud | 21, 20 |
| HTML/CSS/JS, React/Angular/Vue | 19 |
| Design patterns + refactoring | 6, 7 |
| Clean, testable, well-structured code; architectural patterns; stable & scalable | 3, 5, 18 |
| Readable, maintainable code | 5, 7 |
| Git | 27 |
| Agile | 28, 9 |
| RESTful API | 4 |
| Unit test | 18 |
| English | 10.3, 31.2 |
| Tiếp quản code partner Mỹ | 7, 28 |
| Leading new feature development | 2.1 (Quest Engine), 9, 10 |
| Performance, quality, long-term maintainability | 25, 5, 15 |
| Learn quickly and adapt | 1.3, 10 |
| Hiểu nghiệp vụ, làm sát PM, "1% improvements", accountable | 8, 9, 10 |
| 5 core values (1% Improvement, Customer Success, Problem Solving, Accountable, Love People & Communities) | `S-seadev-culture.md`; nối ở 1.3, 9, 10, 29 |
| Quoting, sales orders, RTO contracts, production tracking, delivery scheduling | 8, 26 |
| Profile SA: Software Architecture, CI/CD, AWS, REST, Clean Coding, React/TS, UX | 3, 20, 21, 4, 5, 19 |
| Nền SA từ Urbanise: tiền định kỳ, workflow, tài liệu, tích hợp ngân hàng, owner portal | 8.3, 6 (State), 8.5, 22, 8.10 câu 20 |
