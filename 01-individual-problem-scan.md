# Bản nộp Day 02 — Hỗ trợ đặt câu hỏi bằng AI

Case: **AI Question Formulation Assistant (Hỗ trợ học viên đặt câu hỏi)**

Nhân vật: Một học viên AI / Người tự học đang gặp bế tắc khi tiếp cận kiến thức mới hoặc debug code. Thường xuyên bị bị kẹt vì không biết mình đang sai ở đâu để đặt câu hỏi cho đúng trọng tâm.

## Vì sao bài toán này đáng làm?

- Nỗi đau (pain point) rất thật và xảy ra hàng ngày với bất kỳ ai học AI/Code.
- Có actor cụ thể (Học viên và Mentor).
- Có workflow rõ ràng (Gặp lỗi -> Suy nghĩ -> Hỏi -> Trả lời qua lại).
- Có bottleneck nhận thức rõ ràng: "Không biết bắt đầu hỏi từ đâu".
- Có metric đo lường được (Giảm thời gian kẹt/suy nghĩ từ 10-15 phút xuống 2-3 phút).
- Có thể vẽ before/after workflow rất trực quan.

---

# 01 — Individual Problem Scan

## Scan rộng

Tôi scan 5 problems thực tế.

| # | Lăng kính | Problem quan sát được | Ai đang đau? | Dấu hiệu thật |
|---|---|---|---|---|
| 1 | Tốn thời gian, Lặp lại | Cập nhật CV (sửa project, skill) cho từng JD nhưng không đo được độ match, ngại apply. | Ứng viên AI Engineer | 45-60 phút/JD (khoảng 5 giờ cho 5 JD). Không biết CV của mình match tới đâu. |
| 2 | Lặp lại | Lướt nhiều nền tảng (LinkedIn, TopCV...) đọc JD thủ công để tìm việc phù hợp vì tiêu đề hay giống nhau. | Ứng viên AI Engineer | Tốn 30-45 phút/ngày (15-20 giờ/tháng). Không tìm được công việc phù hợp như ý (mức lương, vị trí, địa điểm). |
| 3 | AI có thể tốt hơn, Pain từ người khác | Không thể tự đánh giá chất lượng Project, luôn phụ thuộc mentor. | Người học AI, Mentor | 30-60 phút cho mỗi lần review. Dành nhiều tuần làm project không tạo lợi thế. |
| 4 | Tốn thời gian, AI có thể tốt hơn | Dùng AI để học nhưng phải tự tra cứu lại fact/hallucination từ Google/docs. | Người học và nghiên cứu AI | 5 phút hỏi AI mất tới 20-30 phút kiểm chứng. |
| 5 | Tốn thời gian | Không biết đặt câu hỏi chất lượng cho mentor/AI, không biết hỏi gì với kiến thức mới | Người học AI, Mentor | 10 phút suy nghĩ + hỏi lan man, câu hỏi ít giá trị. |

Đặc điểm của danh sách problem này:

- Đều xuất phát từ nỗi đau (pain point) thực tế trong quá trình học và tìm việc AI.
- Đều có thông số đo lường (metric) cụ thể về thời gian bị lãng phí (ví dụ: 10 phút suy nghĩ, 45 phút sửa CV).
- Các actor rất cụ thể (Ứng viên, Người học, Mentor).

## Top 3

| Rank | Problem | Vì sao chọn | Điều còn chưa chắc |
|---|---|---|---|
| 1 | Đặt câu hỏi cho mentor/AI | Pain point rất thực tế khi kẹt, giúp giảm tải vòng lặp hỏi lại nhiều lần. | Khó xác định context ban đầu nếu người dùng không biết mình đang sai ở đâu. |
| 2 | Đánh giá chất lượng Project | Rất cần thiết cho người mới, tiết kiệm thời gian cho cả mentor và học viên. | Tiêu chí đánh giá chất lượng project khó chuẩn hoá, dễ bị chủ quan. |
| 3 | Cập nhật CV (CV Tailoring) | Workflow tuyến tính rất rõ, impact đo bằng thời gian rõ ràng. Có thể cấu trúc data (JD, CV) dễ dàng. | Đánh giá độ "match" giữa CV và JD bằng AI có đủ tin cậy không. |

## Problem Card #1 — AI Question Formulation Assistant

**Problem 1 câu:**  
Khi gặp khó khăn hay lỗi mới, học viên thường bị kẹt vì không biết mình đang hổng kiến thức gì để hỏi, không biết phải mô tả vấn đề ra sao, dẫn đến bế tắc hoặc hỏi những câu vô giá trị.

**Actor:**  
Học viên / Người học AI đang bị kẹt.

**Thời điểm / bối cảnh:**  
Khi gặp lỗi/bug khó hiểu, hoặc tiếp cận một khái niệm mới mà không biết mình không hiểu ở đâu.

**Current workflow:**

```text
1. Gặp lỗi/không hiểu bài
2. Loay hoay, suy nghĩ bế tắc vì không biết phải bắt đầu hỏi từ đâu (10 phút)
3. Cố rặn ra một câu hỏi chung chung (VD: "Code em lỗi rồi") hoặc bỏ cuộc
4. Mentor/AI hỏi ngược lại để làm rõ context
5. Trả lời bổ sung thông tin qua lại vài vòng (nếu vẫn không biết trả lời thì im lặng)
6. Mới xác định đúng vấn đề và giải quyết
```

**Bottleneck:**  
Bước 2 — "Không biết phải hỏi gì", đây là rào cản nhận thức (cognitive overload) lớn nhất khiến học viên không thể tiếp tục tiến độ hoặc tận dụng sự trợ giúp.

**Impact:**  
Học viên bế tắc, đình trệ tiến độ, mất tự tin. Nếu hỏi thì câu hỏi chất lượng thấp khiến mentor bối rối, tốn công "bói" xem học viên thực sự đang vướng ở đâu.

**Success metric:**  
Giảm thời gian bị kẹt (suy nghĩ câu hỏi) từ 10 phút xuống dưới 2 phút; sinh ra được 1 câu hỏi có đủ ngữ cảnh (lỗi, file, mục tiêu) để mentor có thể trả lời ngay ở lần đầu tiên.

**Non-AI alternative:**  
Cung cấp một form mẫu (template) điền tay: [Lỗi gì] - [Context] - [Đã thử gì]. Tuy nhiên người không biết mình sai ở đâu thì cũng không biết điền form này thế nào.

**AI hypothesis:**  
AI đóng vai trò "người khơi gợi" (Rubber Duck thông minh): tự động phân tích code/lỗi hiện hành, mớm lời "Có phải bạn đang vướng ở đoạn X không?", từ đó giúp học viên nhận diện đúng điều mình vướng và tự động cấu trúc thành câu hỏi chuẩn để gửi mentor.

**Quick gut:**  
Rule / Workflow.

### Draft current workflow

```text
CURRENT STATE — 15-20 phút

[1 Gặp lỗi: 1']
→ [2 Nghĩ cách hỏi: 10']
→ [3 Gửi câu hỏi chung chung: 1']
→ [4 Mentor hỏi lại context: 5']  <-- bottleneck
→ [5 Học viên bổ sung thông tin: 5']
```

### Draft future workflow

```text
FUTURE STATE — 3 phút

[1 Paste lỗi/context thô cho AI: 1']
→ [2 AI phân tích & hỏi gợi mở (nếu thiếu): 1']
→ [3 AI draft câu hỏi chuẩn: 1']
→ [4 Học viên chốt & gửi mentor: 1']  <-- human boundary

Fallback: AI không gom được ý → Học viên tự viết tay gửi mentor.
```

## Problem Cards #2 và #3 — tóm tắt

| Card | Actor | Bottleneck | Metric | Quick gut | Vì sao chưa chọn làm #1 |
|---|---|---|---|---|---|
| Đánh giá chất lượng Project | Người học AI | Thiếu barem chuẩn, đợi mentor review lâu (30-60 phút) | 60 phút → 5 phút | AI Output / Workflow | Khó định lượng metric "chất lượng project", tính chủ quan cao |
| Cập nhật CV (CV Tailoring) | Ứng viên AI Engineer | Đối chiếu CV và JD mất 45 phút/JD | 45-60 phút → 10 phút | Workflow | Cần tích hợp với nhiều form CV khác nhau, rủi ro format PDF khó xử lý |

---

# 02 — Group Problem Statement

## Group convergence
Dưới đây là các nhóm chính (clusters):

| Cluster | Candidate examples | Pattern chung |
|---|---|---|
| Cào & Tổng hợp thông tin | Tổng hợp Q&A Discord, Tổng hợp yêu cầu bài lab | Gom thông tin tản mạn từ các kênh chat/docs rồi cấu trúc lại thành tài liệu lưu trữ |
| Trợ lý khơi gợi (Prompting) | Hỗ trợ học viên đặt câu hỏi | Đặt câu hỏi gợi mở để giúp người dùng tự làm rõ vấn đề đang gặp phải |
| Review / Feedback | Review Pull Request | Đọc hiểu logic (code/nháp) và đưa ra nhận xét, đánh giá chất lượng |
| Phân tích & Dự đoán | Dự đoán nguyên liệu cho quán ăn | Phân tích số liệu lịch sử để đưa ra con số ước tính cho tương lai |

## Shortlist và score

| Candidate | Actor rõ | Workflow rõ | Pain có evidence | Impact đo được | Làm trong lab | So sánh R/W/A được | Nhóm hiểu domain | Tổng |
|---|---:|---:|---:|---:|---:|---:|---:|---:|
| Tổng hợp Q&A Discord | 5 | 5 | 5 | 5 | 5 | 5 | 5 | 35 |
| Hỗ trợ đặt câu hỏi | 5 | 4 | 5 | 4 | 4 | 4 | 5 | 31 |
| Tổng hợp yêu cầu bài lab | 5 | 5 | 4 | 4 | 4 | 4 | 4 | 30 |
| Dự đoán nguyên liệu | 5 | 4 | 4 | 4 | 2 | 3 | 3 | 25 |
| Review Pull Request | 4 | 3 | 4 | 3 | 2 | 4 | 4 | 24 |

Nhóm chọn: **Tổng hợp Q&A từ kênh Discord**.

Vì sao chọn:
- Có workflow lặp lại hằng ngày và điểm nghẽn rất rõ (đọc, lọc tin nhắn).
- Baseline thời gian đã được đo đạc cụ thể (45 phút/ngày).
- Tỉ lệ rủi ro thấp (chỉ tóm tắt Q&A, có human boundary).
- Có thể kết hợp rõ ràng giữa Rule (cào tin nhắn) và AI (trích xuất Q&A).
- Giải quyết được trực tiếp "pain" lặp lại câu hỏi của học viên và tốn tài nguyên Mentor.

Vì sao không chọn các bài khác:
- Dự đoán nguyên liệu: Mức độ phức tạp cao, dữ liệu (bảng sale lịch sử, thời tiết...) có thể khó giả lập trong thời gian lab, rủi ro dự đoán sai dẫn tới lỗ vốn (impact tài chính).
- Review Pull Request: Phụ thuộc vào business logic của code, khó kiểm soát chất lượng bằng AI chung chung, khó thống nhất success metric trong thời gian ngắn.

## Quick validation

Nhóm hỏi nhanh các lớp trưởng / mentor / học viên.

| Nguồn | Số người | Tín hiệu xác nhận | Tín hiệu phản bác | Nhóm sửa problem thế nào |
|---|---:|---|---|---|
| Phỏng vấn nhanh Mentor | 2 | Mentor xác nhận học viên hay hỏi lại câu cũ, tốn nhiều công search lại. | Có những câu hỏi không có đáp án rõ ràng mà phải debug 1-1. | AI chỉ lấy những cặp hỏi-đáp mà Mentor đã "thả reaction" (xác nhận) hoặc trả lời dứt điểm. |
| Phỏng vấn lớp trưởng | 2 | Công đoạn copy/paste qua Google Docs siêu nhàm chán và tốn thời gian. | Đôi khi tin nhắn không liên tiếp, bị ngắt quãng bởi người khác chèn vào. | Workflow cần AI có khả năng nhận diện context nguyên thread chứ không chỉ copy 2 tin nhắn liền nhau. |

Insight sau validation:

```text
Cần rule để đánh dấu câu hỏi đã được giải quyết (ví dụ mentor thả emoji ✅). AI không chỉ "copy", mà phải trích xuất tóm tắt toàn bộ thread chat lộn xộn thành 1 cặp Q&A ngắn gọn gọn gàng.
```

## Research giải pháp

Nhóm tìm các hướng đã có sẵn, không giả định phải tự build từ đầu.

| Nguồn / tool / case | Link | Họ giải quyết phần nào? | Điểm mạnh | Khoảng trống / rủi ro | Bài học cho nhóm |
|---|---|---|---|---|---|
| Discord Auto-Thread & Forum channels | https://support.discord.com/ | Chia các topic rành mạch, có tính năng search cơ bản. | Native tool của Discord, dễ dùng. | Người dùng vẫn lười search, lười tạo thread mà chỉ thích chat thẳng vào kênh chung. | Cách mạng thói quen người dùng rất khó, nên dùng bot chạy ngầm xử lý tin nhắn tự nhiên tốt hơn. |
| Slack AI Recap / Summarize | https://slack.com/help/articles/25076892548883-Guide-to-Slack-AI | Tổng hợp thread, tóm tắt kênh. | Nhanh, mượt. | Chỉ có trên Slack (trả phí), Discord chưa có native feature tương đương đủ mạnh. | Có thể dùng API/Bot Discord cào tin và dùng LLM tóm tắt tương tự Slack AI. |
| Mendable AI / Kapa.ai | https://www.kapa.ai/ | Bot tự động đọc tài liệu và trả lời kỹ thuật trên Discord. | Trả lời tự động siêu mạnh dựa trên Knowledge Base. | Cần setup Knowledge Base lớn và phức tạp. | Bắt đầu bằng việc tự động xây dựng Knowledge Base (tổng hợp Q&A lên Notion) trước, thay vì nhào vào làm Bot tự trả lời ngay. |

## Workflow before/after

### Current State — 4 bước, 45 phút/ngày

![Current State Workflow](asset/current-state.jpg)

### Future State — 4 bước, 10 phút/ngày

![Future State Workflow](asset/future-state.jpg)

**Fallback:** AI tóm tắt sai ngữ cảnh → Lớp trưởng tự chỉnh sửa nội dung trên Notion. Hoặc nếu chất lượng quá tệ, lớp trưởng tự copy bằng tay thread đó.

**Bottleneck mới:** Lớp trưởng review lại trên Notion. Bottleneck này chỉ mất 5 phút (so với 35 phút cũ) và đóng vai trò kiểm soát chất lượng cần thiết.

Before/after impact:

| Metric | Trước | Sau kỳ vọng | Ghi chú |
|---|---:|---:|---|
| Tổng thời gian | 45 phút/ngày | Dưới 10 phút/ngày | Target chính |
| Tỷ lệ câu hỏi trùng lặp | Cao (3-4 lần/tuần) | Giảm 80% | Vì có Notion Q&A đẹp, dễ tra cứu |
| Bước thủ công (bottleneck) | 35 phút (đọc/lọc) | 5 phút (review) | Tiết kiệm cực lớn |

## Problem Statement v0

| Field | Nội dung |
|---|---|
| **Actor** | Lớp trưởng hoặc thành viên ban hỗ trợ học thuật. |
| **Workflow** | Cuối mỗi ngày, lướt đọc các kênh chat, lọc thread hỏi đáp, copy và định dạng lưu vào Google Docs, rồi chia sẻ link. |
| **Bottleneck** | Bước 1 & 2 (Đọc và lọc hàng trăm tin nhắn trôi tự do) làm thủ công mất 35 phút. |
| **Impact** | Tốn 45 phút mỗi ngày của lớp trưởng. Học viên khó tra cứu, dẫn tới hay hỏi lặp lại câu cũ, làm tốn tài nguyên Mentor. |
| **Success Metric** | Giảm thời gian tổng hợp Q&A từ 45 phút xuống dưới 10 phút/ngày. Tài liệu cập nhật trước 23h00. Tỷ lệ câu hỏi trùng lặp giảm 80%. |
| **Boundary** | AI chỉ trích xuất từ tin nhắn thật, không tự sáng tác câu trả lời mới, không tự thay mặt Mentor để trả lời học viên, lớp trưởng luôn review. |

## Rule / Workflow / Agent

| Mức | Phương án | Khi nào đủ | Rủi ro | Chọn? |
|---|---|---|---|---|
| **Rule** | Dùng Discord Bot tự lưu tin nhắn mỗi khi user gọi lệnh (vd: !save). | Đủ nếu user có ý thức gọi lệnh. | Học viên và Mentor thường quên gọi lệnh, dẫn tới sót dữ liệu. | Dùng một phần để cào data tự động (API), không dùng làm giải pháp cốt lõi. |
| **Workflow** | Cào tự động theo giờ → AI đọc log và trích xuất cặp Q&A → Đẩy lên Notion → Lớp trưởng review. | Hợp lý, AI thay thế đúng đoạn mệt nhất là đọc/lọc/tóm tắt ngữ cảnh tự nhiên. | AI có thể bắt sai ngữ cảnh nếu hội thoại ngắt quãng nhiều. | **Chọn** |
| **Agent** | Agent tự lượn trong Discord, thấy ai hỏi trùng sẽ tự trả lời, tự bổ sung vào docs. | Khi cần trả lời tức thì để giảm tải mentor ngay lập tức. | Trả lời sai kiến thức chuyên môn, làm học viên hiểu nhầm. Khó quản lý. | Chưa chọn (quá rủi ro cho bước đầu). |

Mức chọn:

```text
Workflow
```

Vì sao:
- Việc cào dữ liệu lên lịch hoàn toàn dùng Rule (API Discord + Cronjob).
- AI chỉ tham gia vào đúng 1 khâu cần NLP: Đọc hiểu thread lộn xộn và tóm tắt thành Question - Answer gọn gàng.
- Có bước Human Boundary (lớp trưởng duyệt trên Notion) nên kiểm soát được rủi ro hallucination.

## Problem Statement v1

| Field | Nội dung |
|---|---|
| **Actor** | Lớp trưởng hoặc thành viên ban hỗ trợ học thuật. |
| **Workflow** | Cào tin nhắn cuối ngày → Trích xuất/Tóm tắt thread → Đẩy lên Notion → Review & Phân phối. |
| **Bottleneck** | Đọc, lọc ngữ cảnh hàng trăm tin nhắn lộn xộn để rút ra cặp Q&A chuẩn (35 phút). |
| **Impact** | Mất 45 phút/ngày của Lớp trưởng. Học viên bị trôi tin nhắn nên hỏi lại, phiền Mentor (3-4 lần/tuần). |
| **Success Metric** | Thời gian tổng hợp giảm xuống dưới 10 phút/ngày. Cập nhật đều đặn mỗi tối. Tỷ lệ câu hỏi trùng lặp giảm 80%. |
| **Boundary** | Lớp trưởng duyệt cuối. AI chỉ tóm tắt câu đã trả lời, không tự chế kiến thức mới. |
| **AI intervention point** | Khâu nhận diện và tóm tắt (Question - Answer Extraction) từ đống raw chat logs thành nội dung có cấu trúc. |
| **Mức chọn** | Workflow: Rule (cào tin) → AI (trích xuất Q&A) → Rule (đẩy Notion) → Human (review). |
| **Rủi ro & người thật kiểm tra** | Rủi ro: AI tóm tắt sai ý nghĩa kỹ thuật của Mentor. Người thật kiểm tra: Lớp trưởng đọc nháp trên Notion trước khi publish cho lớp. |

## Final decision

Decision:

```text
Go
```

Pilot nhỏ nhất:
- Xuất thủ công file chat log của 1 kênh Discord trong 1 tuần (dạng text/json).
- Tạo prompt để AI đọc file log đó và xuất ra Markdown danh sách Q&A.
- Lớp trưởng đánh giá xem AI lọc được bao nhiêu % số lượng câu hỏi thực tế và tóm tắt có chuẩn xác không.

Exit / rollback:
- Nếu AI không thể hiểu được context vì tin nhắn chèn ngang quá lộn xộn (độ chính xác < 50%), quay về giải pháp Non-AI: Bắt buộc dùng Forum Channel/Thread trên Discord.

Decision rationale:
- Baseline rõ (45 phút/ngày). Workflow rõ ràng từng bước.
- Rủi ro AI chế chữ được kiểm soát hoàn toàn nhờ Lớp trưởng review bản nháp.
- Phân tách nhiệm vụ tốt: Máy làm việc lặp lại (cào tin, đẩy Notion), AI làm việc hiểu ngữ cảnh (tóm tắt), Người làm việc chất lượng (kiểm duyệt).

---



