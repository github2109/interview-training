# Buổi 3 — EF Core, SQL, transaction (tóm tắt)

## A. Deferred execution, IQueryable vs IEnumerable
- Query là "công thức"; chỉ chạy khi tiêu thụ (ToList/First/Count/Any/Sum/foreach). Where/Select/OrderBy/Take/Include chỉ ghép thêm.
- Dùng nhiều lần → nhiều SQL + dữ liệu có thể lệch giữa các lần → materialize một lần, hoặc để DB tính aggregate.
- `IQueryable` + `Expression<Func>` = cây biểu thức (dữ liệu) → provider EF đọc và dịch sang SQL. `IEnumerable` + `Func` = IL đã compile, EF không thấy → EF chỉ bị duyệt cả bảng (`SELECT *`), lọc trong RAM. C# chọn `Where` theo **kiểu biến lúc compile**.
- Bẫy legacy: repository trả `IEnumerable`, `ToList()`/`AsEnumerable()` quá sớm → "đúng nhưng chậm", tăng theo dữ liệu. Quy tắc: ToList là bước cuối.
- EF Core 3+ throw khi không dịch được (EF ≤2 âm thầm client-eval → kiểm tra khi tiếp quản code cũ). Sửa: viết lại cho dịch được, hoặc lọc ở DB trước rồi mới AsEnumerable.
- Điều tra chậm: `ToQueryString`/log `Database.Command` (có thời gian) → DB hay app → execution plan → projection `Select`, `AsNoTracking`, phân trang, index khớp filter+sort (INCLUDE), `AsSplitQuery` khi Include nhiều collection (tích Descartes).
- User trả lời đúng cả 2 câu kiểm tra (Mid+).
