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

