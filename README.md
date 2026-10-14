# Day 26 — AI Adoption | Klarna AI Customer Support Case Study

**Nhóm thực hiện:** `Anh Em Siêu Nhân` · **Track:** 01 · **Trạng thái:** Hoàn thành toàn diện (Dashboard v2 + Memo Quyết Định + Biên bản Phản Biện Chéo).

---

## 1. Thành viên và Đóng góp (Nhóm 5 người)

| Họ tên | MSSV | Phần phụ trách trong lab | Góp ý thực tế đã đưa cho nhóm bạn (Nhóm 02) |
|---|---|---|---|
| **Bùi Thị Ngọc Trân** | 2A202602529 | **Nhóm trưởng / Case Research Lead:** Tổng hợp nguồn chứng cứ S1–S4, khóa phạm vi bài toán, kiểm chứng tính xác thực của dữ liệu, điều phối chốt Memo quyết định và rà soát repo. | `Nhóm 02 — FinTech AI Ops: Góp ý thu hẹp phạm vi bài toán từ "toàn bộ CSKH" về 2-3 quy trình cốt lõi (đổi trả, tra cứu đơn) để tránh loãng nguồn lực và đo lường khả thi.` |
| **Đinh Thị Minh Tâm** | 2A202602433 | **Diagnosis Lead:** Thực hiện chẩn đoán 5 câu hỏi thực tế, vận dụng Gartner-Lite, ADKAR, lập luận 2 nguyên nhân gốc (RC1, RC2) và xác định giới hạn bằng chứng. | `Nhóm 02 — FinTech AI Ops: Nhắc nhóm bạn điểm nghẽn người dùng nằm ở Desire (sợ trách nhiệm sai sót) và Reinforcement, không thể giải quyết đơn thuần bằng mở lớp đào tạo (Knowledge).` |
| **Phạm Thành Đạt** | 2A202602721 | **Workflow Lead:** Thiết kế mô hình AS-IS / TO-BE, vận dụng Mollick (Centaurs & Cyborgs), thiết lập cơ chế kiểm chứng nguồn, phân luồng rủi ro và chuẩn hóa Handoff payload. | `Nhóm 02 — FinTech AI Ops: Mô hình TO-BE cần phân định ranh giới Mollick: con người giữ quyền quyết định cuối với ngoại lệ, bot chỉ tóm tắt và trích xuất versioned policy.` |
| **Ngô Lê Thủy Tiên** | 2A202602614 | **Metrics & Dashboard Lead:** Xây dựng cấu trúc Dashboard v1/v2, thiết lập công thức logic, xây dựng kế hoạch thu thập Baseline W0 và phân tầng Segments theo rủi ro. | `Nhóm 02 — FinTech AI Ops: Thay thế các vanity metric (lượt login, số câu hỏi) bằng outcome & workflow metrics (First Contact Resolution, Reopen rate, Handoff completeness) có baseline cụ thể.` |
| **Nguyễn Khánh Linh** | 2A202602409 | **Roadmap & QA Lead:** Thiết kế kế hoạch 30–60–90 ngày, xác lập tiêu chí Gate và Failure actions, ghi nhận biên bản phản biện chéo 2 chiều và hoàn thiện Memo quyết định. | `Nhóm 02 — FinTech AI Ops: Bổ sung Gate định lượng (QA pass ≥95%, 0 critical error) cho từng mốc 30-60-90 ngày thay vì chỉ liệt kê danh sách đầu việc hành chính.` |

### Quy trình phối hợp nhóm:
1. **TV1 + TV2**: Đối chiếu nguồn bằng chứng thực tế [S1–S4] và xác lập 2 nguyên nhân gốc; TV3 xác nhận mô hình TO-BE giải quyết triệt để nguyên nhân đã tìm ra.
2. **TV3 + TV4**: Thống nhất cấu trúc trường sự kiện (event logs) cho từng bước trong workflow; TV5 kiểm tra điều kiện vượt cổng (Gates) và người chịu trách nhiệm (Owners).
3. **Cả 5 thành viên**: Trực tiếp tham gia phiên phản biện chéo với Nhóm 02; TV5 tổng hợp biên bản, TV4 cập nhật Dashboard v2, TV1 kiểm tra tính nhất quán chéo giữa README – Memo – Excel.

---

## 2. Phạm vi Khóa (Locked Scope)

- **1 sản phẩm AI cụ thể:** Trợ lý AI Chăm sóc Khách hàng Klarna (Klarna AI Customer Service Assistant).
- **1 nhóm người dùng chính:** Nhân viên CS tuyến 1 & tuyến 2 tiếp nhận ca chuyển tiếp từ AI (Tier-1 / Tier-2 Human CS Agents).
- **3 quy trình liên quan:**
  1. *(W1) Phân loại ý định và Đánh giá rủi ro yêu cầu* (Intent Classification & Risk Triaging).
  2. *(W2) AI xử lý ca đủ điều kiện có trích dẫn chính sách* (AI Resolution for Eligible Low-risk Inquiries with Versioned Policy Citation).
  3. *(W3) Bàn giao người–AI có cấu trúc, Kiểm toán QA và Vòng lặp phản hồi* (Contextual Handoff, QA Sampling & Continuous Feedback Loop).
- **1 vấn đề quan sát & đo lường được:** Doanh nghiệp quá tập trung vào mục tiêu cắt giảm chi phí ngắn hạn dẫn đến việc AI cố trả lời cả những ca phức tạp/nhạy cảm, câu trả lời thiếu trích dẫn phiên bản chính sách, bàn giao sang nhân viên thiếu bối cảnh khiến khách hàng phải lặp lại từ đầu, làm tăng tỷ lệ mở lại ca (Reopen rate đạt 12% ở quy trình cũ) và buộc CEO Klarna phải công khai thừa nhận sự suy giảm chất lượng [S2].

---

## 3. Chẩn đoán Điểm nghẽn và Hai Nguyên nhân Gốc (Root Causes)

Nhóm tiến hành chẩn đoán qua 5 câu hỏi thực tế và liên kết 3 khung phân tích chuẩn:

### 3.1. Năm câu hỏi chẩn đoán thực tế
1. **Workflow (Quy trình):** AI có nằm trong công việc thật không?  
   → *Có xuất hiện nhưng nằm ngoài sự kiểm soát chặt chẽ; AI cố trả lời thay vì phối hợp với nhân viên CS.*
2. **Con người (Con người):** Người dùng thiếu động lực, kiến thức hay khả năng?  
   → *Nhân viên CS không thiếu kiến thức sử dụng nhưng thiếu động lực (Desire) vì sợ gánh trách nhiệm khi AI tư vấn sai và ức chế vì nhận ca chuyển tiếp không có tóm tắt.*
3. **Sẵn sàng (Tổ chức):** Dữ liệu, quyền truy cập và governance đã đủ chưa?  
   → *Chính sách FAQ chưa có versioning timestamp; chưa phân quyền dữ liệu theo độ nhạy cảm của giao dịch tài chính.*
4. **Tin cậy (Kiểm soát):** AI sai thì phát hiện, kiểm tra và xử lý thế nào?  
   → *Hệ thống cũ không có trích dẫn nguồn cụ thể, thiếu cơ chế QA mẫu định kỳ và không có Kill-switch ngắt luồng tự động khi xảy ra sự cố.*
5. **Đo lường (Chỉ số):** Đang đo activity hay giá trị thực?  
   → *Hệ thống cũ chỉ đo activity (số lượt chat 2,3 triệu, % chat bot nhận 80%), hoàn toàn bỏ quên chất lượng giải quyết dứt điểm và thời gian chờ đuôi dài (P90).*

### 3.2. Hai nguyên nhân gốc (Root Causes)
- **RC1 (Quy trình & Ranh giới phân chia việc — Thuộc Mollick Framework):** Ranh giới phân luồng giữa AI và nhân viên CS chưa tối ưu; thiếu phân tầng rủi ro (Risk-tiering). Bot được giao xử lý cả các ca tranh chấp giao dịch tài chính, khi bot không chắc chắn lại thiếu cơ chế bàn giao ngữ cảnh (Handoff payload) chuẩn hóa.
  - *Căn cứ bằng chứng:* 35% ca chuyển tiếp ở AS-IS thiếu tóm tắt; CEO Klarna thừa nhận thiếu hụt hỗ trợ con người [S2]; SEC filing ghi nhận sự cần thiết của human support [S3].
- **RC2 (Mức độ sẵn sàng & Đo lường — Thuộc Gartner-Lite & Measurement):** Tổ chức đo lường vanity metrics thay vì outcome metrics; kho tri thức (KB) thiếu quản trị phiên bản (versioned policies) và content owner, dẫn đến việc bot đưa thông tin chính sách cũ gây rủi ro sai sót tài chính (Critical Errors).
  - *Căn cứ bằng chứng:* Báo cáo PR chỉ nêu số lượng chat gộp [S1]; log khảo sát tiền trạm W0 ghi nhận 2 sự cố sai sót chính sách hoàn tiền.

---
