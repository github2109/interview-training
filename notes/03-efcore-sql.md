# Buổi 3 — EF Core, SQL, transaction (tóm tắt)

## A. Deferred execution, IQueryable vs IEnumerable
- Query là "công thức"; chỉ chạy khi tiêu thụ (ToList/First/Count/Any/Sum/foreach). Where/Select/OrderBy/Take/Include chỉ ghép thêm.
- Dùng nhiều lần → nhiều SQL + dữ liệu có thể lệch giữa các lần → materialize một lần, hoặc để DB tính aggregate.
- `IQueryable` + `Expression<Func>` = cây biểu thức (dữ liệu) → provider EF đọc và dịch sang SQL. `IEnumerable` + `Func` = IL đã compile, EF không thấy → EF chỉ bị duyệt cả bảng (`SELECT *`), lọc trong RAM. C# chọn `Where` theo **kiểu biến lúc compile**.
- Bẫy legacy: repository trả `IEnumerable`, `ToList()`/`AsEnumerable()` quá sớm → "đúng nhưng chậm", tăng theo dữ liệu. Quy tắc: ToList là bước cuối.
- EF Core 3+ throw khi không dịch được (EF ≤2 âm thầm client-eval → kiểm tra khi tiếp quản code cũ). Sửa: viết lại cho dịch được, hoặc lọc ở DB trước rồi mới AsEnumerable.
- Điều tra chậm: `ToQueryString`/log `Database.Command` (có thời gian) → DB hay app → execution plan → projection `Select`, `AsNoTracking`, phân trang, index khớp filter+sort (INCLUDE), `AsSplitQuery` khi Include nhiều collection (tích Descartes).
- User trả lời đúng cả 2 câu kiểm tra (Mid+).

## Ôn async gắn với EF (user hỏi thêm)
- `ToList()` trong async method: **0 thread mới, 1 thread bị chặn** (socket read đồng bộ). `await ToListAsync`: 0 bị chặn. `.Result`: 1 thread ngủ trên wait handle **và cần thêm 1 thread rảnh** để chạy continuation đánh thức nó → khi mọi thread đều ngủ trong `.Result`, continuation kẹt trong hàng đợi → starvation (pool chỉ bơm ~1–2 thread/s). ASP.NET cũ/WPF: deadlock thật (SynchronizationContext).
- Không thể `await IEnumerable` (lỗi compile). `foreach`/`Count()`/`First()` trên IQueryable = I/O đồng bộ. Stream dữ liệu lớn: `AsAsyncEnumerable` + `await foreach` + `AsNoTracking` (giữ connection suốt vòng lặp).
- Trả IQueryable/IEnumerable lười ra khỏi `using` → chạy khi context đã dispose.
- Async method chạy **đồng bộ tới await chưa xong đầu tiên**; compiler sinh state machine (`MoveNext`, `state`, biến cục bộ thành field); `await` = đăng ký continuation rồi return, **không tạo thread**.
- Fire-and-forget: 0 thread mới; lỗi bị cất vào Task bỏ rơi (UnobservedTaskException, không crash); DbContext/HttpContext đã dispose; race "second operation"; mất khi shutdown; không giới hạn. `Task.Run` chỉ mượn thread pool.
- `async void`: exception thoát ra → ném lại trên thread pool → **crash process** (không có SyncContext). Sweeps "chưa thấy crash" có thể do: try/catch bao thân method, chạy ở Unity/UI context, app crash rồi tự restart (xem restart count), lỗi chưa xảy ra.
- `try { X(); } catch` không await: **không bắt được gì**, kể cả lỗi trước await (state machine cất mọi exception vào Task). try/catch **bên trong** method thì bắt được (scope try giữ qua await) — nhưng chỉ biến lỗi im lặng thành có log; vẫn cần Channel + BackgroundService (scope riêng) hoặc Outbox/job queue.

## B. DbContext, tracking, N+1, concurrency, transaction (đã dạy, user bỏ qua bài kiểm tra)
- Tracking: snapshot → DetectChanges → UPDATE đúng cột đổi; AsNoTracking cho đọc. `ExecuteUpdate/Delete` (EF7+) bỏ qua tracker/interceptor/audit.
- N+1: lazy loading hoặc query trong vòng lặp → projection, Include, batch `Contains`. Phát hiện: đếm số SQL mỗi request.
- Optimistic `[Timestamp]` rowversion → `DbUpdateConcurrencyException` → 409; MVC phải gửi RowVersion qua hidden field và gán OriginalValue. Pessimistic cho thao tác ngắn tranh chấp cao.
- SaveChanges đã là transaction; tự mở khi nhiều SaveChanges/trộn SQL thô; giữ ngắn, không gọi HTTP/email bên trong (dùng Outbox); `EnableRetryOnFailure` → bọc trong `CreateExecutionStrategy`.

## C. Isolation, query chậm, connection pool, index
- Anomaly: dirty read / non-repeatable / phantom. SQL Server mặc định Read Committed (lock); **Azure SQL bật RCSI mặc định** (đọc bản đã commit, không bị chặn) — kiểm tra `sys.databases`. Không nâng cả transaction lên Serializable; khoá đúng chỗ (`UPDLOCK, HOLDLOCK` trên dòng cha) hoặc atomic UPDATE bộ đếm (vd. xe chở tối đa 3 đơn/ngày). `NOLOCK` có thể đọc trùng/sót → không dùng cho số liệu tiền, dùng RCSI.
- Điều tra: Query Store (top theo tổng duration) → `sys.dm_exec_requests` (blocking, wait type LCK/PAGEIOLATCH/CPU) → actual plan → sửa → đo lại `STATISTICS IO`.
- Plan: Scan bảng lớn → index; Key Lookup lặp → INCLUDE; estimated ≪ actual → statistics cũ / parameter sniffing; CONVERT_IMPLICIT → sai kiểu tham số.
- Lưu trữ: trang 8KB; clustered index = bảng xếp theo PK (B-tree, ~3 tầng); nonclustered = mục lục (key + clustered key). Seek = nhảy thẳng; Key Lookup = mỗi dòng quay về bảng (tính theo **số dòng**, đọc random); Scan = tính theo **số trang**, đọc tuần tự + read-ahead. Ít dòng → seek+lookup thắng; nhiều dòng rải khắp bảng (đại lý 80k đơn) → scan thắng.
- **Parameter sniffing**: plan lập theo tham số lần chạy đầu, cache, dùng lại cho mọi giá trị. Triệu chứng: lúc nhanh lúc chậm, restart/rebuild thì khỏi, chạy SSMS (literal) thì nhanh. Xác nhận: estimated vs actual rows, compiled vs runtime value, Query Store nhiều plan. Sửa: covering index, phân trang, `OPTION(RECOMPILE)` cho query hiếm, `OPTIMIZE FOR UNKNOWN`.
- Index tạo **một lần** bởi `CREATE INDEX` (scan+sort+ghi B-tree vào file DB, kèm statistics), cập nhật **đồng bộ** trong cùng transaction mỗi INSERT/UPDATE/DELETE (page split) → không bao giờ cũ; cái giá là ghi chậm. Lần query đầu chỉ tạo **plan cache** + nạp **buffer pool** (RAM, mất khi restart). Statistics có thể cũ (tự cập nhật theo ngưỡng). Production: `ONLINE = ON`. Tìm index thừa: `sys.dm_db_index_usage_stats`.
- Không có index phù hợp → scan. SQL Server/PostgreSQL **không tự index FK**; **EF Core migration có**. DB tạo tay/legacy hay thiếu → kiểm tra đầu tiên khi tiếp quản (thiếu còn làm DELETE bảng cha scan bảng con). Missing index DMV chỉ là gợi ý.
- **Composite index** = danh bạ (Họ, Tên), ngầm thêm clustered key. Seek được: `A=`, `A= AND B range`, `A= ORDER BY B` + TOP (không Sort, dừng sớm, hợp keyset). Không seek: chỉ `B`. Range ở cột trước → cột sau chỉ lọc lại. Thứ tự **E → S → R**. Key để tìm/sắp xếp, INCLUDE để hiển thị. `(A)` thừa khi có `(A,B)`.
- Connection pool: Dispose = trả về pool; cạn (mặc định 100, chờ 15s) do không dispose, transaction dài, starvation, song song quá mức, pod×pool > giới hạn DB. Xem `sys.dm_exec_sessions` (nhiều sleeping), `dotnet-counters` SqlClient. Tăng Max Pool Size chỉ là giảm đau.
