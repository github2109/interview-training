# Joblogic — câu hỏi business theo feature (cho vòng SA + PO của SEADEV)

Nguồn sự thật: `context/joblogic.md` (kiểm từ code, 139 commit), `notes/J-joblogic-architecture.md` (DocGen, SAS + proxy), `notes/J-multitenant-deep.md`. Chỗ nào chưa kiểm chứng được ghi **[Hiệp điền]** hoặc **[Hiệp xác nhận]**: điền bằng chi tiết thật trước buổi phỏng vấn, không thì bỏ câu đó đi.

Cách dùng: mỗi feature có (1) bối cảnh nghiệp vụ bằng tiếng Việt, (2) câu chuyện 60 giây bằng tiếng Anh, (3) câu hỏi hay gặp và câu trả lời ngắn, (4) câu nối sang Ops Hub. **Câu in đậm trong mỗi câu trả lời là câu cần thuộc**, phần còn lại nói theo ý.

---

## 0. Nói đúng trước khi nói hay (đọc kỹ)

Hiệp định nói "I implemented PDF generation for quotes, create and update quote". Theo code đã kiểm:

| Câu định nói | Sự thật trong code | Nên nói |
|---|---|---|
| "Implemented PDF generation for quotes" | Platform **đã có sẵn** service DocGen (Core dựng dữ liệu → thay tag trong template DOCX bằng Xceed DocX → Aspose.Words xuất PDF/DOCX). Hiệp **thêm DocX tags mới** cho template **Project Quote, Project Invoice, Application for Payment**, cập nhật system template + guideline, viết logic **Previously Claimed** từng dòng | "I **extended** the document generation for project quotes, invoices and applications for payment" |
| "Create / update quote" | Hiệp thêm **Customer Contract** vào form tạo/sửa **Project Details và Project Quote**, kèm audit có version và ẩn/hiện theo gói | "I changed the create and edit flow of projects and project quotes to link a customer contract" |

Lý do: SA sẽ hỏi tiếp "Which library? How did you handle page breaks / fonts?". Nếu nói "I built it" mà không trả lời được thì mất điểm trung thực, thứ mà SEADEV coi trọng (value Accountable). Nói "extended" mà giải thích được **cả pipeline** thì điểm còn cao hơn, vì chứng tỏ hiểu hệ thống.

Nếu Hiệp còn làm phần quote nào khác chưa có trong `context/joblogic.md` (ví dụ sửa tính tổng quote, trạng thái quote): **[Hiệp điền]** rồi mình bổ sung câu trả lời.

---

## 1. Chọn feature nào để kể (đã xếp theo giá trị cho Ops Hub)

| # | Feature | Vì sao đáng kể | Nối sang Ops Hub (theo JD) |
|---|---|---|---|
| A | **Tài liệu Quote / Invoice / Application for Payment** (DocX tags + Previously Claimed) | Đúng thứ Hiệp muốn nói; Ops Hub sống bằng tài liệu (quote, contract PDF) | Quote PDF, contract PDF theo từng công ty |
| B | **Gắn Customer Contract vào Project / Project Quote** (form tạo/sửa, gating theo gói, audit) | Có đủ 3 thứ SA thích: thay đổi model dữ liệu, feature gating, audit trail | Quote → order → contract, lịch sử thay đổi |
| C | **Project Cost Breakdown** (dự toán từ quote vs thực tế, lợi nhuận, margin) | Nghiệp vụ tiền rõ ràng, có con số, PO rất thích | Giá quote, margin, tiền |
| D | **Job Spend Limit** | Câu chuyện "phát hiện edge case nhờ hiểu nghiệp vụ" mạnh nhất | Hạn mức, phê duyệt, thông báo, phân quyền |
| dự phòng | Selling Rate Times & Holidays | Tính giá theo khung giờ, ngày lễ | Tính giá theo thời gian, lịch giao |

Thứ tự kể khi được hỏi "What did you do at Joblogic?": **A + B gộp thành một câu chuyện** (đều thuộc ticket Customer Contract, Proj62), rồi C, rồi D. Chỉ kể 2 feature trong câu đầu, để interviewer chọn đào sâu.

**Câu mở (30 giây):**
> At Joblogic, a UK field-service management SaaS, I worked part-time in the Projects and Jobs modules. The work I'm most proud of is around project quotes and billing: I linked customer contracts to projects and quotes, with an audit trail, and extended the quote, invoice and application-for-payment documents, including the "previously claimed" logic for staged billing. I also built the cost breakdown that compares a project's quoted estimate with actual cost, and a spend-limit check for jobs. Happy to go deeper into any of them.

---

## A. Tài liệu Quote / Invoice / Application for Payment

### Bối cảnh nghiệp vụ
- Khách của Joblogic là **nhà thầu dịch vụ hiện trường ở UK** (bảo trì, lắp đặt…). Họ gửi cho **khách của họ** các tài liệu PDF: **Quote** (báo giá dự án), **Invoice**, và **Application for Payment** (đề nghị thanh toán theo tiến độ, kiểu phổ biến ở ngành xây dựng UK).
- Dự án dài thì **thu tiền theo đợt (cumulative / staged billing)**. Mỗi đợt, mỗi dòng phải cho thấy: tổng giá trị đã làm tới nay, **đã đề nghị trước đó (Previously Claimed)**, và **lần này đề nghị bao nhiêu**.
- Mỗi tenant tự thiết kế **template Word** riêng (logo, bố cục), chèn tag kiểu `@@TagName@@`. Hệ thống điền dữ liệu vào tag. Tenant không có template thì dùng **system template**.

Ví dụ đời thường: dự án lắp điều hoà trị giá £100,000. Đợt 1 làm xong 30% → đề nghị £30,000. Đợt 2 làm tới 70% → tổng tới nay £70,000, đã đề nghị £30,000, **lần này £40,000**. Không có Previously Claimed thì khách phải tự trừ, rất dễ trả trùng hoặc cãi nhau.

### Câu chuyện 60 giây
> Contractors on Joblogic send quotes, invoices and applications for payment to their own clients, and each tenant designs its own Word template with tags. The platform already had a document-generation service: the Core service builds a document model, the DocGen service fills the tags in the tenant's DOCX template, and Aspose converts it to PDF or Word. As part of the customer-contract work, I added new tags to the project quote, project invoice and application-for-payment documents, updated the system templates and the guideline tenants use to build their own, and implemented the "previously claimed" amount per line for cumulative billing. **So on a long project billed in stages, every line shows the value to date, what was already claimed, and what is due now — the client doesn't have to work it out.**

### Câu hỏi hay gặp

**Q1 (SA). Walk me through how a quote PDF is generated.**
> The web app sends a generate message to the DocGen service with the entity ID, an optional template ID and the output type. DocGen picks the template — the tenant's own one, or falls back to the system template. It asks Core for a checksum of the source data; **if the data and template haven't changed, it returns the file it already generated instead of rendering again.** Otherwise it gets a ready-made document model from Core, replaces the tags — text, images, signatures, repeating table rows — adds a DRAFT watermark for draft invoices, converts with Aspose to PDF or DOCX, saves it to temporary blob storage and returns a link.

Điểm cộng nói thêm nếu được hỏi "why split Core and DocGen": *"Core owns the business rules and the numbers, DocGen only renders. So the totals on the PDF are the same totals as on the screen — there's one place that calculates them."*

**Q2 (SA). Why Word templates with tags instead of HTML-to-PDF?**
Đây là quyết định có sẵn của platform; nói lý do mình hiểu, không nhận là mình chọn.
> That decision was made before I joined, but the reason makes sense: **tenants design their own documents in Word without a developer.** The trade-off is less layout control and the risk of a tenant breaking a template, which is why there's a system template as fallback and a guideline that lists every tag. For a product where the company controls the layout, HTML-to-PDF can be easier to version and test.

**Q3 (PO). What exactly is "previously claimed" and how is it calculated?**
> For each line, previously claimed is the sum of what was already claimed for that line on earlier applications or invoices of the same project. **This claim = value to date minus previously claimed.** For example, a £100k line at 30% then 70%: the second application shows £70k to date, £30k previously claimed, £40k due now.
> **[Hiệp xác nhận]**: tài liệu nào được tính vào "earlier" — chỉ bản đã phát hành, có loại bản nháp/huỷ không? Có credit note không? Làm tròn theo dòng hay theo tổng? Nếu nhớ thì thêm một câu: *"The tricky part was deciding which earlier documents count: [rule thật]."*

**Q4 (PO). The template changes after a quote was sent. Does the old document change?**
> The file the client received doesn't change, because it was already generated. But **if you regenerate, you get the current data and the current template** — the cache is keyed on a checksum of the data, the template and the logo, so any change produces a new file. For documents that must never change, like a signed contract, I'd store the generated PDF permanently together with the template version and a snapshot of the data, and never re-render it.
> **[Hiệp xác nhận]**: Joblogic có lưu vĩnh viễn PDF đã gửi khách (attachment/email log) không, hay chỉ blob tạm 7 ngày? Chưa chắc thì chỉ nói phần đầu + phần "I'd".

**Q5 (SA). How is the download link secured?**
> Generating the link requires login and a download permission on the action, and data is filtered by tenant. **The link itself is a short-lived signed blob URL (SAS), served through our own domain via a reverse proxy**, so we don't expose the storage account and avoid CORS. Printing is different: the server downloads the file and streams it inside the authenticated request.

**Q6 (SA). Generation is slow or the server is busy. What do you do?**
> Rendering is CPU-heavy, so it runs in its own service and doesn't block the web app, and the **checksum cache means the same document isn't rendered twice**. If it still took several seconds, I'd make it asynchronous: return 202 with a job ID, render in a background worker, and notify or let the client poll.

**Q7 (PO). A tenant says a tag shows nothing / the PDF looks broken.**
> First reproduce with their template and data versus the system template. If the system template is fine, it's usually the tenant's template — a mistyped tag or a tag inside a table where it can't repeat — and the guideline is what we point them to. If both are wrong, it's the data: I'd check the document model Core returns for that entity. **I separate "template problem" from "data problem" first**, because they have different owners.

**Q8 (SA). How did you test it?**
> **[Hiệp điền]**: unit test cho phần tính Previously Claimed? sinh thử tài liệu với system template trên môi trường UAT? ai review (team UK)? Mẫu: *"I unit-tested the previously-claimed calculation with MSTest — first claim, several claims, a line added later — then generated each document with the system template on UAT, and the UK team reviewed the PR."* Chỉ nói phần nào thật.

**Nối sang Ops Hub:**
> In the Ops Hub, quotes and contracts are documents customers sign, so I'd apply the same split: one place calculates the numbers, the renderer only renders, and once a document is signed it's stored and never regenerated.

---

## B. Gắn Customer Contract vào Project và Project Quote

### Bối cảnh nghiệp vụ
- **Customer Contract** là một app (module trả phí) của Joblogic: hợp đồng giữa nhà thầu và khách của họ. **[Hiệp điền: hợp đồng dùng để làm gì trong nghiệp vụ — giá thoả thuận? điều khoản? báo cáo theo hợp đồng?]**
- Yêu cầu: khi **tạo hoặc sửa** Project và Project Quote, chọn được Customer Contract của khách; field **chỉ hiện với tenant có đăng ký app Customer Contract**; mọi lần tạo/sửa phải có **audit** (ai đổi, đổi gì, lúc nào); số hợp đồng hiện được trên tài liệu (tags ở phần A).

### Câu chuyện 60 giây
> Contractors wanted to link a project, and its quote, to the customer contract it falls under. I added the contract selection to the create and edit flows of projects and project quotes. **The field only shows for tenants that subscribe to the Customer Contract app**, so other tenants see no change. **Every create or update sends an audit message that now carries the contract ID; the audit service stores versioned entries in MongoDB**, so support can answer "who linked this project to that contract, and when". I wrote unit tests for the audit handler, and the contract details flow into the quote, invoice and application documents through the new tags.

### Câu hỏi hay gặp

**Q1 (PO). Why does a contractor need this?**
> **[Hiệp điền]** lợi ích thật. Khung trả lời: *"So the project is billed and reported under the right contract — [ví dụ: the agreed rates/terms apply, and the contract reference appears on the quote and invoice the client receives]."*

**Q2 (SA). How does the audit trail work?**
> Create and update handlers publish an audit message through Service Bus to the Audit service, which stores entries per tenant in MongoDB. **Each entry has a version taken from the SQL row version, so entries can be ordered correctly even if messages arrive out of order**, and the first entry stores the full content. Audit is asynchronous, so saving a project isn't slowed down, and the message bus retries if the Audit service is down.

Follow-up: *"So audit can be lost or late?"* → *"It's eventually consistent, with retries. For an audit that must be exact, like money movements, I'd write it in the same database transaction or use an outbox."*

**Q3 (SA). Where do you enforce "only for subscribed tenants"?**
> The UI hides the field for tenants without the module, based on their license. **But hiding is only UX — the server must also ignore or reject the contract ID if the tenant isn't subscribed**, otherwise anyone can post it.
> **[Hiệp xác nhận]** server có check không. Nếu không chắc, nói: *"In my part it was mainly the UI and the data flow; in general the rule belongs on the server too."*

**Q4 (PO). What happens to existing projects, or if a tenant unsubscribes?**
> The field is optional, so existing projects simply have no contract and nothing breaks. If a tenant stops subscribing, **we hide the field but keep the data**, so if they subscribe again the links are still there and history stays correct.
> **[Hiệp xác nhận]** hành vi thật khi unsubscribe.

**Q5 (PO). The contract changes after the quote was sent. What then?**
> The audit trail shows exactly when the link changed. The quote the client already has doesn't change. Whether the new contract terms should apply to an already-sent quote is a business decision, so I'd ask the PO rather than decide it in code — usually a sent quote keeps its terms and you create a revision.

**Nối sang Ops Hub:**
> The same pattern fits a quote turning into an order and a contract: link records explicitly, keep an audit trail of who changed what, and gate features per company subscription on the server, not just in the UI.

---

## C. Project Cost Breakdown (dự toán từ quote vs thực tế)

### Bối cảnh nghiệp vụ
- Quản lý dự án muốn biết **giữa chừng**: dự án có đang vượt dự toán không, loại chi phí nào vượt, còn lời bao nhiêu.
- **Estimated** lấy từ các dòng trong **Project Quote Sections** (lúc báo giá đã dự tính). **Actual** lấy từ **job cost lines + Purchase Orders**.
- Chia theo **10 loại**: Material, Labour, Expense, Subcontractor, Travel, Callout, Mileage, Overtime, Schedule of Rates, Other. Có **Cost Variance**, **Estimated vs Actual Profit & Margin**, quy đổi **đa tiền tệ**.
- Hiệp sửa `GetProjectJobCostHandler` (thêm EstimatedCost, CostVariance), `ProjectController`, view model, UI tab Summary.

Ví dụ con số (thuộc để nói): giá bán £50,000, dự toán chi phí £40,000 → lợi nhuận dự kiến £10,000, **margin 20%**. Thực tế Labour dự toán £10,000 nhưng tốn £12,500 → **variance −£2,500 (vượt 25%)**; tổng chi phí thực £44,000 → lợi nhuận £6,000, **margin 12%**. Quản lý thấy ngay vấn đề nằm ở Labour.

### Câu chuyện 60 giây
> Project managers had no single place to see whether a project was on budget. I built the cost breakdown on the project summary: **estimated cost comes from the quote sections, actual cost from job cost lines and purchase orders, split into ten categories like labour, materials and subcontractors**, with the variance per category and estimated versus actual profit and margin, converted to the project's currency. For example, if labour was quoted at £10k and has cost £12.5k, the manager sees a £2.5k overrun on that line straight away, and the margin dropping from 20% to 12%, while there's still time to act.

### Câu hỏi hay gặp

**Q1 (PO). Markup vs margin?**
> **Markup is profit over cost; margin is profit over selling price.** Cost £80, price £100: markup 25%, margin 20%. Mixing them up is a classic pricing bug, so I always confirm which one the business means.

**Q2 (PO). How do you define variance — positive means good or bad?**
> We showed variance as estimated minus actual per category, so **a negative number means over budget**. **[Hiệp xác nhận dấu thật trong code]**. The important part is that the sign convention is agreed with the PO and labelled clearly on screen, because finance users read it both ways.

**Q3 (SA). Multi-currency: which exchange rate?**
> **[Hiệp xác nhận]**: tỷ giá lúc phát sinh chi phí hay tỷ giá hiện tại? Khung trả lời: *"Costs can be in different currencies, so we converted each one to the project currency [at the rate stored on the transaction / the current rate]. The principle: store the original amount, currency and rate on the transaction, so a report from last month gives the same number today."*

**Q4 (SA). A big project makes the page slow. What do you do?**
> **Aggregate in SQL — group by category in one query — rather than loading every cost line into memory**, and check the plan for missing indexes on project ID and cost type. If it's still heavy, read from the read-only replica, or keep a pre-aggregated summary updated when costs change. I'd measure first with the actual query plan before choosing.

**Q5 (PO). Why compare against the quote and not a separate budget?**
> Because the quote is what the contractor actually priced and agreed with the client, **so variance against the quote tells them if their pricing was right**, which also improves the next quote.

**Q6 (SA). Money in code?**
> `decimal`, never `double`, and round only at display or at defined business points, so totals of rounded lines don't drift.

**Nối sang Ops Hub:**
> In the Ops Hub the same thinking applies to quotes and orders: prices snapshotted when the quote is finalized, money in decimal with clear rounding rules, and a margin the business can trust.

---

## D. Job Spend Limit

### Bối cảnh nghiệp vụ
- Khách của nhà thầu thường cấp **hạn mức chi tiêu cho một Job** (ví dụ "sửa trong phạm vi £500, vượt thì phải hỏi tôi"). Một job có thể có nhiều **Visit** (lần kỹ thuật viên tới).
- Yêu cầu: hiện **banner OverLimit / InLimit** khi ước tính chi phí visit so với hạn mức; thông báo back-office; khách sửa được hạn mức trên **Customer Portal**; có **permission** riêng.
- Làm cùng một đồng nghiệp (Harrison Nguyen). Hiệp viết `GetVisitSpendEstimateBannerMsgHandler`, BO notification, phần Customer Portal, permission, nhiều bugfix.

### Câu chuyện 60 giây (bản đã có ở master D2.2, giữ nguyên)
> The requirement looked simple: warn when a visit's estimated spend goes over the job's spend limit. When I walked through real scenarios, two edge cases came up. **First, for the second and later visits, the comparison had to be against the remaining limit after earlier visits, not the full limit. Second, a visit could already be deployed to the engineer's mobile device when the office changed the limit, so the data on the device was stale; we added a "redeploy required" flag.** The back-office notification was fan-out to the right roles and idempotent on the event ID, so a retried event didn't notify people twice.

### Câu hỏi hay gặp

**Q1 (PO). Why should a contractor care?**
> If they go over the client's authorised limit without approval, **the client can refuse to pay the extra**. The banner warns the office before the engineer goes, and the notification makes sure someone acts.

**Q2 (PO). How did you find those edge cases?**
> By walking through a job with three visits on paper, with numbers: limit £500, first visit £300, second visit estimate £300. **Against the full limit it looks fine; against the remaining £200 it's over.** That walk-through is now how I read every requirement.

**Q3 (SA). Who gets the notification, and how do you avoid duplicates?**
> The event fans out to users in the Admin, Job Desk and Costing roles. **Message delivery is at-least-once, so the handler is idempotent on the event's idempotency ID** — a redelivered message doesn't notify people twice.

**Q4 (SA). The client edits the limit on the portal while the office edits it too.**
> **[Hiệp xác nhận]** có check concurrency không. Nếu không có, nói: *"Last write wins there today; I'd add optimistic concurrency with the row version so the second save gets a conflict instead of silently overwriting."*

**Q5 (PO). Who is allowed to change the limit?**
> A new permission under the job settings for staff, and a separate permission mapping for portal users, so **a contractor can decide which of their client's users may change it**.

**Nối sang Ops Hub:**
> Approval thresholds, notifications and permissions come up in any order flow — for example who can discount a quote beyond a limit, or cancel an order already in production.

---

## E. Dự phòng: Selling Rate Times & Holidays (2 câu)

> I built the weekly grid where contractors define time bands — day, start and end time — each with a selling rate, colour and type, pay band or holiday, edited by drag-and-drop with a read-only mode, plus the logic for which bands are chargeable. **The interesting cases are a shift crossing midnight, overlapping bands and holidays**, and I fixed several critical bugs, like pay bands not saving.

Follow-up "shift crosses midnight?" → *"Split it into two intervals at midnight and price each one by its own band."* **[Hiệp xác nhận code thật xử lý thế nào]**.

---

## F. Câu hỏi business chung về Joblogic

**"What does Joblogic do and who uses it?"**
> It's a field-service management SaaS in the UK. Contractors use it to run their business: quotes, jobs, scheduling engineers, a mobile app for engineers on site, invoicing, and a customer portal for their own clients. I worked in the Projects and Jobs modules.

**"How did you get requirements and work with the team?"**
> **[Hiệp điền]**: ai viết ticket (BA/PO bên UK?), ticket ở Azure DevOps, có buổi refinement không, hỏi lại bằng gì (Teams/comment)? Mẫu: *"Requirements came as tickets in Azure DevOps from the UK product team. Before coding, I listed the scenarios and open questions and confirmed them, then the UK team reviewed my pull requests and tested on UAT."*

**"What was the hardest part?"** → dùng D (edge case spend limit) hoặc A (Previously Claimed: chọn tài liệu nào được tính).

**"What would you do differently?"** → Hiệp không muốn chê code Joblogic, nên nói về bản thân:
> I'd write down the scenarios with numbers and get them confirmed even earlier — on spend limit, the "remaining limit" case came up during development rather than in refinement.

**"How does this experience help us?"**
> The Ops Hub is the same kind of product: business documents, money, approvals and different settings per company. I'm used to reading a requirement through real scenarios, keeping calculations in one place, and making sure what the customer sees on a PDF matches what's in the system.

---

## G. Thuộc lòng trước khi vào phòng (5 dòng)
1. Quote documents: **extended**, không phải "built"; pipeline Core → DocGen → tags → Aspose → PDF; cache theo checksum.
2. Previously Claimed: **lần này = tới nay − đã đề nghị**; ví dụ £70k − £30k = £40k.
3. Customer Contract: tạo/sửa project + quote, **ẩn theo gói (server cũng phải check)**, audit có version trong Mongo.
4. Cost Breakdown: estimated từ **quote sections**, actual từ **cost lines + PO**, 10 loại; margin = lời / giá bán.
5. Spend Limit: **visit 2+ so với phần còn lại**, **RedeployRequired**, thông báo idempotent.

## H. Việc Hiệp cần làm
- Điền các chỗ **[Hiệp điền] / [Hiệp xác nhận]** (khoảng 12 chỗ). Chỗ nào không nhớ thì xoá câu đó, không đoán.
- Tập nói to mục 1 (câu mở) và câu chuyện 60 giây của A và D.
