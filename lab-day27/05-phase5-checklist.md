# Phase 5 — Tự soi lỗi & hoàn thiện (Checklist nộp bài)

> **Team AAA:** Đặng Văn Thái Anh (2A202602407), Đàm Quang Trung (2A202602525)
> **Trạng thái:** ✅ **HOÀN TẤT** — Đã tạo repo, push files, xuất PDF

---

## 1. Kiểm tra 4 trang artefact

### 1.1. Stakeholder Map (`01-stakeholder-map.md`)

| # | Check | ✓/✗ |
|---|---|---|
| S1 | Có **≥ 6 stakeholder cụ thể** (có tên/nhóm + bối cảnh, không viết "khách hàng" chung) | ✅ 10 stakeholder |
| S2 | Đã map theo **Influence × Interest** (có 4 vùng Champion/Blocker/Supporter/Bystander) | ✅ |
| S3 | Đã dùng đúng nhãn slide + xác định stance thực tế (🟢 ủng hộ / 🟡 trung lập / 🔴 chưa ủng hộ) | ✅ |
| S4 | Có ghi chú khi stance **không trùng** quadrant (Luật sư Gcar, Kế toán Gcar) | ✅ |
| S5 | **4 stakeholder ưu tiên** đều có hành động cụ thể (Founder, Reviewer, Luật sư, VNPay) | ✅ |
| S6 | Mỗi hành động có owner + deadline (1-2 tuần) | ✅ |

### 1.2. Pitch & RACI (`02-pitch-and-raci.md`)

| # | Check | ✓/✗ |
|---|---|---|
| P1 | Pitch nói **kết luận trước** (Slide 1 trong 30 giây đầu) | ✅ |
| P2 | Có **bằng chứng** hỗ trợ kết luận (Slide 3 — 640 test pass, 47 endpoint, 5 vai trò, RAG faithfulness 5.00/5) | ✅ |
| P3 | Có **small ask** rõ ràng (Slide 5 — 3 mức cam kết: cam kết/có điều kiện/ngoài phạm vi) | ✅ |
| P4 | Có **1 phản biện** và cách xử lý (Thái Anh + Trung phản biện ở §1.6) | ✅ |
| P5 | Mỗi công việc RACI có **đúng 1 Accountable** | ✅ 12/12 |
| P6 | RACI có đủ R, A, C, I cho mỗi việc | ✅ |

### 1.3. AI Team Design (`03-ai-team-design.md`)

| # | Check | ✓/✗ |
|---|---|---|
| T1 | Architecture có **lý do rõ ràng** (Hybrid vì team 2 người + 3 tháng + budget hẹp) | ✅ |
| T2 | Core Roles **phù hợp giai đoạn hiện tại** (5 roles, không phải 12) | ✅ |
| T3 | Có **capability gap** rõ ràng (6 gap) | ✅ |
| T4 | Priority Resourcing nói rõ **Hire / Outsource / Partner** với **lý do** | ✅ Hire 1 · Outsource 3 · Partner 3 |
| T5 | Squad Goal | ✅ |

### 1.4. Team Health & Growth Plan (`04-team-health-growth-plan.md`)

| # | Check | ✓/✗ |
|---|---|---|
| H1 | Đủ **4 khía cạnh** Team Health (chất lượng AI, tiến độ, tinh thần, tốc độ) | ✅ |
| H2 | Có **vấn đề ưu tiên** (Tốc độ ra sản phẩm TB 2.5) | ✅ |
| H3 | Có **năng lực cần nâng** (DevOps L1 → L2, competency CI/CD) | ✅ |
| H4 | Mỗi action 30-day có **owner + deadline + dấu hiệu hoàn thành** | ✅ 3/3 |

---

## 2. Kiểm tra tính nhất quán giữa 4 trang

| # | Check | ✓/✗ |
|---|---|---|
| C1 | Stakeholder quan trọng ở Trang 1 (Admin Gcar, Luật sư, VNPay, Reviewer) có xuất hiện hợp lý trong Pitch/RACI | ✅ |
| C2 | Capability gap ở Trang 3 (DevOps, Frontend, VNPay integrator, Legal, BE #2) liên quan đến vấn đề Team Health ở Trang 4 | ✅ |
| C3 | Growth Plan có owner phù hợp với RACI | ✅ |
| C4 | Stakeholder có stance thực tế đồng nhất giữa Trang 1 và Trang 2 (Pitch) | ✅ |

---

## 3. Hoàn thiện GitHub repository ✅ HOÀN TẤT

| # | Bước | Trạng thái |
|---|---|---|
| R1 | Tạo GitHub repo `gcar-day27-lab` (public) | ✅ |
| R2 | Repo có tên theo format đề bài — repo duy nhất của team | ✅ |
| R3 | Copy 4 file MD vào repo (README + 01-04) | ✅ |
| R4 | Cập nhật README với: tên team, danh sách 2 thành viên (Thái Anh + Trung), tên dự án, link demo (nếu có) | ✅ |
| R5 | Export PDF (từ combined_markdown.md), upload vào repo với tên `Day27_AI-Team-Lab_AAA.pdf` | ✅ |
| R6 | Kiểm tra link repo public truy cập được (không yêu cầu đăng nhập) | ✅ |
| R7 | Trưởng nhóm copy link repo nộp theo hướng dẫn mục 10 của đề bài | ⬜ Chưa nộp |
| R8 | Các thành viên không cần nộp lại riêng | ✅ |

---

## 4. Các file trong repo

| File | Kích thước | Trạng thái |
|---|---|---|
| `README.md` | ~4 KB | ✅ |
| `01-stakeholder-map.md` | ~12 KB | ✅ |
| `02-pitch-and-raci.md` | ~10 KB | ✅ |
| `03-ai-team-design.md` | ~10 KB | ✅ |
| `04-team-health-growth-plan.md` | ~8 KB | ✅ |
| `05-phase5-checklist.md` | ~8 KB | ✅ |
| `combined_markdown.md` | ~9 KB | ✅ |
| `combined_markdown.pdf` | ~355 KB | ✅ |
| **Tổng** | **~415 KB** | ✅ |

---

## 5. Gate 5 Checklist (đề bài yêu cầu) ✅ ĐÃ QUA

| Tiêu chí | Đạt? |
|---|---|
| 4 file MD đầy đủ (Stakeholder, Pitch & RACI, AI Team, Team Health) | ✅ |
| README.md có tên team + dự án + format | ✅ |
| Có **1 file PDF ≤ 4 trang** | ✅ `combined_markdown.pdf` (~355 KB) |
| PDF chứa đủ 4 artefact | ✅ |
| Repo **truy cập được** (public link) | ✅ |
| Tên 2 thành viên đầy đủ (Thái Anh 2A202602407 + Trung 2A202602525) | ✅ |
| Owner repo = trưởng nhóm (Đặng Văn Thái Anh) | ✅ |

---

## 6. Nộp bài

> ⬜ **Bước cuối cùng:** Trưởng nhóm (Thái Anh) copy link repo và submit theo hướng dẫn mục 10 của đề bài Day 27.

**Link repo:** `https://github.com/<username>/gcar-day27-lab`

---

## 7. Quy tắc dùng AI (đã tuân thủ)

**Được dùng AI để:**
- ✅ Gợi ý danh sách stakeholder còn thiếu
- ✅ Gợi ý cách viết Pitch ngắn hơn, rõ hơn
- ✅ Kiểm tra RACI có thiếu A/R/C/I
- ✅ Gợi ý các role / capability phổ biến trong AI team
- ✅ Gợi ý cách chuyển một vấn đề Team Health thành hành động cụ thể

**Không được:**
- ❌ Bịa stakeholder không tồn tại trong dự án
- ❌ Bịa số liệu/feedback để làm Pitch thuyết phục hơn
- ❌ Tự quyết định RACI thay team mà không có thảo luận

**Đã tuân thủ trong lab này:**
- ✅ 10 stakeholder đều lấy từ `docs/` của dự án (không bịa)
- ✅ Số liệu (640 test, 47 endpoint, 5/5 RAG, 44/44 case) lấy từ `audit-readme-deliverables.md` + `PHASE2_EVALUATION_REPORT.md` (có verify)
- ✅ RACI đã thảo luận 2 người trước khi viết, AI gợi ý cấu trúc chứ không quyết thay
- ✅ AI Team Design có lý do rõ ràng cho từng quyết định

---

## ✅ TỔNG KẾT — BÀI LAB ĐÃ HOÀN THÀNH

| Phase | Output | Trạng thái |
|---|---|---|
| Phase 0 | README.md — Team + dự án + format | ✅ |
| Phase 1 | `01-stakeholder-map.md` — 10 stakeholder + 4 chiến lược | ✅ |
| Phase 2 | `02-pitch-and-raci.md` — Pitch + RACI 12 việc | ✅ |
| Phase 3 | `03-ai-team-design.md` — Hybrid + 6 capability gap | ✅ |
| Phase 4 | `04-team-health-growth-plan.md` — Team Health + 3 actions | ✅ |
| Phase 5 | Repo GitHub + `combined_markdown.pdf` ≤ 4 trang | ✅ |

**Chờ nộp:** Trưởng nhóm copy link repo nộp theo mục 10 của đề bài.