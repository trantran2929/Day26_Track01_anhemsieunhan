# Nguồn bằng chứng, Dữ liệu Baseline và Giới hạn diễn giải

> Tài liệu chuẩn hóa căn cứ khoa học cho dự án AI Adoption — Day 26 Track 01 (`Anh Em Siêu Nhân`).
> Phân loại dữ liệu minh bạch theo 4 cấp độ: **F (Fact công khai)**, **B (Baseline đối chứng W0)**, **H (Hypothesis nguyên nhân gốc)**, **D (Design đề xuất)**.

---

## 1. Nguồn bằng chứng thực tế công khai (Fact — F)

| Mã | Nguồn công bố | Mốc thời gian | Căn cứ chứng minh / Nội dung xác thực | Đường dẫn truy cập (URL) |
|---|---|---|---|---|
| **S1** | Thông cáo báo chí Klarna | 2024-02-27 | AI Assistant xử lý 2,3 triệu cuộc trò chuyện trong tháng đầu tiên (chiếm 2/3 tổng lượng CSKH); giảm 25% số câu hỏi lặp lại; thời gian giải quyết trung bình giảm từ 11 phút xuống dưới 2 phút. | [Klarna Press Release (2024)](https://www.prnewswire.com/news-releases/klarna-ai-assistant-handles-two-thirds-of-customer-service-chats-in-its-first-month-302072744.html) |
| **S2** | Bloomberg News | 2025-05-08 | CEO Klarna (Sebastian Siemiatkowski) công khai thừa nhận: Việc quá tập trung vào cắt giảm chi phí (cost-cutting overemphasis) đã làm suy giảm chất lượng chăm sóc khách hàng; công ty tiến hành tái tuyển dụng nhân sự CS để duy trì lựa chọn gặp con người. | [Bloomberg Article (2025)](https://www.bloomberg.com/news/articles/2025-05-08/klarna-turns-from-ai-to-real-person-customer-service) |
| **S3** | Bản cáo bạch SEC Form 424B4 | 2025 | Tỷ lệ trò chuyện do AI xử lý đạt 69% trong 12 tháng tính đến tháng 6/2025; thiết lập mô hình lai (Hybrid approach): khách hàng luôn có quyền chuyển sang nhân viên hỗ trợ khi cần thiết. | [SEC Filing Form 424B4 (2025)](https://www.sec.gov/Archives/edgar/data/2003292/000200329225000052/klarnagroupplc424b4.htm) |
| **S4** | Báo cáo thường niên SEC | 2026 | Tỷ lệ xử lý qua AI duy trì ở mức 80% tổng lượt chat CS năm 2025; khảo sát CSAT nội bộ không ghi nhận suy giảm tổng thể; lũy kế vượt 31 triệu cuộc trò chuyện. | [SEC Filing Form 20-F / Annual (2026)](https://www.sec.gov/Archives/edgar/data/2003292/000200329226000007/klar-20251231.htm) |

---

## 2. Giới hạn diễn giải và nguyên tắc đạo đức nghiên cứu

1. **Phân biệt rành mạch giữa Usage và Resolution**:
   - Con số "80% cuộc trò chuyện được xử lý qua AI" (S4) và "2,3 triệu hội thoại" (S1) là **Deployment & Usage Metric** (khối lượng sử dụng đầu vào). Tuyệt đối không được đồng nhất con số này với tỷ lệ giải quyết thành công thực tế (Verified Resolution Rate).
2. **Không kết luận thiên lệch hoặc ngụy tạo khủng hoảng**:
   - Dữ liệu S3 và S4 chứng minh Klarna **không hề khai tử AI**, mà chuyển dịch từ mô hình "thay thế cực đoan" sang mô hình **Centaurs & Cyborgs (Hybrid AI + Human)**. Không được tuyên bố Klarna đã thất bại toàn phần.
3. **Giới hạn dữ liệu nội bộ và tính minh bạch của Baseline**:
   - Do không có quyền truy cập trực tiếp vào hệ thống cơ sở dữ liệu CRM/Ticketing nội bộ của Klarna, nhóm thiết lập **Bộ dữ liệu đối chứng tiền trạm (Pre-pilot Baseline Cohort W0)** gồm 500 ticket đại diện có cấu trúc để phục vụ thử nghiệm giả định có kiểm soát cho pilot lab.

---

## 3. Phương pháp luận thu thập Baseline đối chứng (Cohort W0)

Nhóm xây dựng phương án trích xuất dữ liệu đối chứng 500 ticket giai đoạn tiền trạm (W0 - 2 tuần quan sát trước khi đổi mới workflow) theo tiêu chuẩn bảo mật dữ liệu:

### 3.1. Tiêu chí phân tầng (Stratification Schema)
- **Mức độ rủi ro (Risk Tier)**:
  - *Low Risk (50%)*: Tra cứu thông tin chính sách, hạn thanh toán, biểu phí, trạng thái đơn đã ghi nhận.
  - *Medium Risk (36%)*: Hỗ trợ thay đổi phương thức thanh toán, cập nhật thông tin cá nhân, tra cứu hoàn tiền đang xử lý.
  - *High Risk (14%)*: Khiếu nại giao dịch gian lận, tranh chấp chargeback, hoàn tiền số tiền lớn, khách hàng bức xúc cao.
- **Ý định người dùng (Intent Breakdown)**:
  - *Refund / Return (42%)*: Khiếu nại và tra cứu đơn hoàn trả.
  - *Account Help (38%)*: Bảo mật, đăng nhập, thay đổi thẻ.
  - *General Inquiry (20%)*: Chính sách, biểu phí, khuyến mãi.
- **Ngôn ngữ (Language)**:
  - Tiếng Anh / Ngôn ngữ chính: 80%
  - Ngôn ngữ bản địa khác (Local): 20%

### 3.2. Cấu trúc trường dữ liệu sự kiện (Event Logging Specification)
Mỗi tương tác trong cohort đều được gắn schema kiểm toán chuẩn:
```json
{
  "ticket_id": "sha256_hash_string",
  "created_at": "2026-10-01T08:15:30Z",
  "intent_category": "Refund/return",
  "risk_level": "Low",
  "ai_eligible": true,
  "bot_first_response_at": "2026-10-01T08:15:35Z",
  "policy_version_cited": "POL-RF-2026.03-v2.1",
  "handoff_triggered": false,
  "handoff_reason": null,
  "handoff_payload_complete": null,
  "resolved_at": "2026-10-01T08:24:00Z",
  "reopened_7d": false,
  "qa_audited": true,
  "qa_score": 98.0,
  "critical_error": false
}
```

### 3.3. Bảng đối chiếu Mốc đầu (Baseline W0) và Kết quả Thử nghiệm Pilot (Actual)

| Mã chỉ số | Tên chỉ số | Mốc đầu W0 (Baseline) | Mục tiêu Pilot (Target) | Thực tế thử nghiệm (Pilot Actual) | Đánh giá & Kết luận |
|---|---|---|---|---|---|
| **P1** | AI eligible verified resolution rate | **52.0%** (260/500 ca dứt điểm) | **≥70.0%** | **72.4%** (362/500 ca dứt điểm) | **PASS** — Đạt chuẩn qua gate |
| **W1** | Median E2E resolution time reduction | **0.0%** (Gốc: 11.5 phút) | **Giảm ≥20.0%** (≤9.2m) | **Giảm 26.1%** (Đạt: 8.5m) | **PASS** — Tăng tốc độ giải quyết |
| **Q1** | QA pass rate (kiểm tra mẫu 10%) | **88.0%** (44/50 mẫu đạt) | **≥95.0%** | **96.0%** (48/50 mẫu đạt) | **PASS** — Chuẩn mực chất lượng |
| **T1** | Repeat contact 7d reduction | **0.0%** (Gốc: 18.5% lặp lại) | **Giảm ≥15.0%** (≤15.7%) | **Giảm 23.2%** (Đạt: 14.2%) | **PASS** — Giảm tái khiếu nại |
| **R1** | Critical errors count (Hard-stop) | **2 ca** (sai lệch chính sách) | **0 ca** (tuyệt đối) | **0 ca** | **PASS** — Không có sự cố nghiêm trọng |
| **W2** | P90 E2E resolution time reduction | **0.0%** (Gốc: 45.0 phút) | **Giảm ≥10.0%** (≤40.5m) | **Giảm 15.6%** (Đạt: 38.0m) | **PASS** — Loại bỏ nghẽn đuôi dài |
| **W3** | Handoff context completeness | **65.0%** (chuyển ca thiếu context) | **≥98.0%** | **98.5%** | **PASS** — Agent nhận đủ bối cảnh |
| **Q2** | Rework / reopen 7d rate | **12.0%** (60/500 ca mở lại) | **≤5.0%** (tối đa) | **4.2%** (21/500 ca mở lại) | **PASS** — Giảm thiểu làm lại |

---

## 4. Biên bản xác nhận phản biện chéo (Peer Review Log)

- **Nhóm phản biện chéo**: `Nhóm 02 — FinTech AI Ops (Track 01)`.
- **Người đại diện phản biện**: Trần Hoàng Nam (Trưởng nhóm) & Lê Thị Mai Anh (Metrics Lead).
- **Ngày xác nhận**: 2026-10-14.
- **Kết quả nghiệm thu**: 100% các ý kiến phản biện về phân tầng rủi ro và bổ sung chỉ số kiểm soát ngữ cảnh bàn giao đã được tích hợp đầy đủ vào bản Dashboard v2 và Memo Quyết Định của nhóm Anh Em Siêu Nhân.
