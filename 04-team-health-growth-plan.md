# GCAR Contract Generation Agent — Team Health & Growth Plan

> **Phase 4 — Track 1 Day 27 Lab** · 25 phút · Cá nhân → Team
> **Dự án:** GCAR Contract Generation Agent · **Mục tiêu:** ADR 0011 (chi nhánh + RBAC) trong 14 ngày đầu, ADR 0012 (thanh toán) trong ngày 15-30
> **Team AAA:** Đặng Văn Thái Anh (2A202602407), Đàm Quang Trung (2A202602525)

---

## 1. Cá nhân — Tự chấm Team Health (4 chiều, 1-5)

### 1.1. Đặng Văn Thái Anh

| Khía cạnh | Điểm | Lý do |
|---|---|---|
| Chất lượng AI | 4 | 640 test pass, eval pipeline chạy, RAG faithfulness 5.00/5 — điểm cao nhấtng deployment thật chưa verify |
| Tiến độ | 3 | MVP chạy được nhưng ADR 0011/0012 đã viết 1 tháng rồi chưa code |
| Tinh thần team | 4 | Chủ động review docs, chia việc rõ; áp lực là áp lực đều |
| Tốc độ ra sản phẩm | 2 | Mỗi deploy mất 3-5 ngày (chưa có auto-deploy); hotfix 1 bug mất 1 ngày |

### 1.2. Đàm Quang Trung

| Khía cạnh | Điểm | Lý do |
|---|---|---|
| Chất lượng AI | 3 | Eval pipeline tốt nhưng chưa thấy khách thật dùng → chưa biết có hallucination ở edge case không |
| Tiến độ | 2 | 7 FR-VEH/MVP còn dang dở (handover checklist 12 ảnh, lịch bàn giao); ADR 0011 chỉ mới có tài liệu |
| Tinh thần team | 4 | 2 người quen làm, ít conflict; áp lực khi Gcar hỏi "khi nào xong" |
| Tốc độ ra sản phẩm | 3 | Code review nhanh nhưng UI đổi chậm vì chỉ 1 người làm Frontend |

---

## 2. Team — So sánh & chọn vấn đề

### 2.1. Điểm hợp nhất (chênh lệch < 1 điểm)

| Khía cạnh | Thái Anh | Trung | TB | Chênh lệch |
|---|---|---|---|---|
| Chất lượng AI | 4 | 3 | **3.5** | 1 |
| Tiến độ | 3 | 2 | **2.5** | 1 |
| Tinh thần team | 4 | 4 | **4.0** | 0 |
| Tốc độ ra sản phẩm | 2 | 3 | **2.5** | 1 |

### 2.2. Phân tích chênh lệch

- **Tiến độ (TB 2.5, chênh 1):** Trung thấp hơn vì cảm nhận rõ hơn về 7 FR-VEH/MVP còn dang dở (anh Thái đã quen với MVP chạy được nên quên phần còn lại).
- **Chất lượng AI (TB 3.5, chênh 1):** Thái Anh cao hơn vì đã đọc kỹ báo cáo eval; Trung thận trọng hơn vì chưa thấy khách thật dùng.
- **Chênh lệch nhỏ (≤1) → hợp lý, không có xung đột quan điểm.**

### 2.3. Vấn đề ưu tiên — ảnh hưởng trực tiếp milestone tiếp theo

> **Nếu không xử lý sẽ ảnh hưởng milestone 3 tháng (ADR 0011 + 0012):**

| # | Vấn đề | Ảnh hưởng milestone | Điểm |
|---|---|---|---|
| 1 | **Tốc độ ra sản phẩm** (TB 2.5) | Mỗi deploy mất 3-5 ngày → không thể pilot chi nhánh đầu trong Q4/2026 | 2.5 ⭐ |
| 2 | **Tiến độ** (TB 2.5) | 7 FR-VEH/MVP + 2 ADR chưa code → khó chốt demo cuối tháng | 2.5 ⭐ |
| 3 | Chất lượng AI (3.5) | Rủi ro nhưng chưa cản milestone | 3.5 |
| 4 | Tinh thần team (4.0) | Ổn | 4.0 |

**→ Vấn đề ưu tiên: #1 (Tốc độ ra sản phẩm) + #2 (Tiến độ)** — chọn **#1 làm vấn đề chính** vì nếu deploy tự động hóa được, cả tiến độ cũng cải thiện theo.

---

## 3. Team — Competency cần nâng cấp

| Role cụ thể | Level hiện tại | Competency cần nâng | Action thực hành trong 30 ngày |
|---|---|---|---|
| **DevOps / QA (chia đôi Thái Anh 0.5 + Outsource 0.5)** | **L1** — AI Literate (chỉ biết chạy `make test`) | **CI/CD + Auto-deploy** lên L2 (AI Practitioner) | **Xây GitHub Action**: khi push lên `develop` → tự chạy test → tự deploy staging → gửi link preview vào Slack. Trong 30 ngày có pipeline chạy ổn định ≥ 80% lần push. |

> **Tại sao chọn DevOps/QA thay vì Backend/Frontend?**
> - Backend (Thái Anh) đã L3 — không phải gap.
> - Frontend (Trung) đã ở L2 — gap nhưng fix bằng Outsource (đã ghi ở 03-ai-team-design.md §3.1 #3).
> - DevOps đang L1 và là **bottleneck cho cả team** — nếu fix được thì mọi người đều ship nhanh hơn.

---

## 4. Team — Growth Plan 30 ngày (tối đa 3 hành động, có owner + deadline + dấu hiệu hoàn thành)

| # | Vấn đề | Hành động 30 ngày | Owner | Deadline | Dấu hiệu hoàn thành |
|---|---|---|---|---|---|
| **1** | Tốc độ ra sản phẩm (TB 2.5) — mỗi deploy mất 3-5 ngày | **Setup GitHub Action auto-deploy staging**: push `develop` → chạy `pytest` + `ruff` + `mypy` → nếu pass → auto-deploy lên Vercel preview → comment link vào PR. Đồng thời enable Sentry để catch lỗi runtime. | **Thái Anh** | **Day 14** | (a) File `.github/workflows/deploy-staging.yml` tồn tại và chạy được; (b) PR mới mở có comment tự động chứa link preview trong ≤5 phút; (c) Sentry dashboard có ≥1 alert test được trigger. |
| **2** | Tiến độ (TB 2.5) — 7 FR-VEH/MVP + 2 ADR chưa code | **Hoàn tất 50% LMS-023** (chi nhánh + RBAC): migration schema `regions`/`branches`, code RBAC `branch_scope(user)`, 6-role login UI cơ bản. **KHÔNG** bao gồm bản đồ Leaflet (sang LMS-023.5 tuần 3). | **Trung** | **Day 14** | (a) Có branch `feature/branch-rbac` đã merge vào `develop`; (b) Migration script chạy thành không lỗi trên MySQL staging; (c) Test mới ≥30 case cho RBAC scope → tổng test ≥690 pass; (d) 6-role login UI demo được với 3 tài khoản giả lập (Admin/Reviewer/Customer). |
| **3** | DevOps competency (L1 → L2) + chất lượng AI (TB 3.5) — chưa có eval tự động trong CI | **Thêm bước RAG eval vào CI**: chạy `eval/run_needs_eval.py` + `eval/knowledge_eval_core.py` trên 30 case vàng trong GitHub Action. Nếu faithfulness < 4.5/5 HOẶC Hit@1 < 80% → fail CI. | **Thái Anh** | **Day 21** | (a) Job `eval-rag` xuất hiện trong GitHub Actions; (b) PR thay đổi prompt/RAG có check eval fail rõ ràng; (c) Báo cáo `eval-results-ci.md` được sinh tự động vào mỗi PR. |

> **Tại sao chỉ 3 hành động?** Slide yêu cầu "tối đa 3 hành động" — mỗi hành động phải có thể kiểm tra được. 3 hành động đủ cover vấn đề #1 (tốc độ) + #2 (tiếnộn) + bonus nâng competency DevOps.

---

## 5. Gate 4 Checklist

| Tiêu chí | Đạt? |
|---|---|
| Chấm đủ **4 khía cạnh** (chất lượng AI, tiến độ, tinh thần, tốc độ) | ✅ Cả 4 |
| Chọn **vấn đề ưu tiên** có ảnh hưởng milestone | ✅ #1 Tốc độ ra sản phẩm |
| Có **1 role + level + competency + action** rõ ràng | ✅ DevOps L1 → L2, competency CI/CD, action setup GitHub Action |
| Growth Plan **≤ 3 hành động** | ✅ 3/3 |
| Mỗi hành động có **owner** | ✅ Thái Anh #1 #3 · Trung #2 |
| Mỗi hành động có **deadline cụ thể** | ✅ Day 14 / Day 14 / Day 21 |
| Mỗi hành động có **dấu hiệu hoàn thành** đo được | ✅ Mỗi action có 2-4 tiêu chí đo |

---

## 6. Theo dõi 30 ngày

| Tuần | Check-in | Owner |
|---|---|---|
| W1 (Day 7) | GitHub Action CI pass · migration branch mở | Thái Anh / Trung |
| W2 (Day 14) | LMS-023 50% merged · staging deploy chạy tự động | Cả 2 |
| W3 (Day 21) | RAG eval chạy trong CI · eval-results-ci.md có data | Thái Anh |
| W4 (Day 30) | Tổng kết: deploy time < 30 phút, test pass ≥ 690, RAG faithfulness ≥ 4.5/5 | Cả 2 |

**Nếu Day 14 chưa đạt #1 + #2:** team họp 30 phút, quyết định: (a) cắt scope LMS-023.5 (bản đồ) sang Q1/2027; (b) tăng Outsource DevOps lên 0.7; (c) extend deadline 7 ngày có điều kiện.