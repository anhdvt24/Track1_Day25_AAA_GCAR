# GCAR Contract Generation Agent — Pitch & RACI

> **Phase 2 — Track 1 Day 27 Lab** · 30 phút · Team → Cá nhân → Team
> **Dự án:** GCAR Contract Generation Agent · **Mục tiêu:** ADR 0011 + 0012 trong 3 tháng
> **Team AAA:** Đặng Văn Thái Anh (2A202602407), Đàm Quang Trung (2A202602525)

---

## 1. Pitch — Conclusion First (Kết luận trước)

> **Audience:** Founder / Admin Gcar (Product Owner) — người duyệt scope, cấp tài khoản Manager, quyết định rollout chi nhánh.

### 1.1. Slide 1 — Kết luận (30 giây đầu, quan trọng nhất)

> **Trong 3 tháng tới (Q4/2026 → Q1/2027), team sẽ đưa GCAR từ MVP chạy được trên 1 server lên vận hành thật ở 2 chi nhánh đầu tiên (HN-01 và HCM-01), với 6 vai trò phân quyền theo phạm vi và 2 kênh thanh toán (VNPay online + quầy nhận xe). Đến cuối Q1/2027, Gcar có thể nhận booking thật từ khách, ký hợp đồng điện tử có audit, và thu tiền online qua VNPay sandbox — tất cả trên cùng codebase AI Agent đã có 640 test pass.**

### 1.2. Slide 2 — Tại sao làm điều này (1 phút)

**Vấn đề kinh doanh Gcar đang gặp (theo `2026-10-06-tom-tat-thiet-ke.md` §1):**

- Hiện mọi nhân viên thấy mọi hợp đồng → **không có phân vùng dữ liệu theo chi nhánh**
- `staff` và `reviewer` đều duyệt được → **vi phạm Separation of Duties (SoD)**
- Màn Signer **chưa ký được thật**, hợp đồng ký vẫn giả lập
- Tài khoản nhân viên chỉ tạo từ biến môi trường → **không có workflow onboarding**
- **Chưa thu tiền qua hệ thống** — mọi giao dịch ngoài luồng

**Nếu không làm gì:**
- Gcar không thể mở chi nhánh thứ 2 mà vẫn đảm bảo audit + phân quyền
- Mỗi lần thêm nhân viên mới = tạo file `.env` mới = không có audit
- Khách muốn trả trước online = Gcar phải từ chối vì chưa có cổng thanh toán

### 1.3. Slide 3 — Bằng chứng hiện có (1 phút)

> Không hứa điều gì vượt quá những gì đã verify được:

| Bằng chứng | Nguồn |
|---|---|
| ✅ **640 test pass** trên codebase hiện tại | `make test` chạy 2026-10-06 |
| ✅ **47 REST endpoint** + **5 vai trò** đã chạy được với JWT + RBAC | `src/api/` |
| ✅ **RAG faithfulness 5.00/5** (LLM-as-judge) trên 3 case | `eval/results/rag_eval_llm_20260930_0930.md` |
| ✅ **44/44 case** P2.4 synthetic golden offline pass | `docs/ai-copilot/PHASE2_EVALUATION_REPORT.md` §6 |
| ✅ **ADR 0011** (12 quyết định D1-D12) + **ADR 0012** (D1-D8) **đã viết xong** | `2026-10-06-tom-tat-thiet-ke.md` |
| ✅ **Bảng giá Phụ lục B** (700k/800k/950k + 7 loại phí) đã rule-based, có source/version | `policies/rental_policy.yaml` |
| ✅ **Template hợp đồng** theo mẫu HĐCTXTL Ver 24.10.22 đã điều chỉnh cho Gcar | `src/rental/pdf.py` |
| 🟡 **VNPay merchant sandbox** — chưa đăng ký (chờ Kế toán Gcar) | `2026-10-06-tom-tat-thiet-ke.md` §12.2 |
| 🟡 **Luật sư tư vấn** — chưa ký HĐ (CL-17 vẫn để trống) | `prd-v2-traceability.md` §3.6 |

### 1.4. Slide 4 — Lộ trình 3 tháng (1 phút)

```
Tháng 1 (W1-W4)                Tháng 2 (W5-W8)                Tháng 3 (W9-W12)
───────────────                ───────────────                ───────────────
✅ LMS-023 chi nhánh+RBAC       ☐ LMS-024 thanh toán            ☐ Pilot thật 1 chi nhánh
✅ 6-role UI + bản đồ           ☐ VNPay sandbox + IPN           ☐ 7 FR-VEH/MVP còn thiếu
                                ☐ Quầy nhận xe                  ☐ Audit report tuân thủ
                                ☐ Bảng giá versioned            ☐ Hand-off cho Gcar vận hành
```

### 1.5. Slide 5 — Lời hứa (giới hạn bằng chứng, 30 giây)

> **Cam kết đo được (sẽ verify được):**
>
> ✅ **Chắc chắn trong scope:** Migration schema `regions`/`branches`, RBAC `branch_scope(user)`, 6-role login UI, bản đồ Leaflet, ký 2 bên, bảng giá versioned, audit hash-chain theo phạm vi chi nhánh.
>
> 🟡 **Có điều kiện:** VNPay sandbox tích hợp (cần Kế toán Gcar mở merchant — 5-7 ngày làm việc); CL-17 chính sách hủy chuyến (cần Luật sư tư vấn Gcar review — 2-4 tuần).
>
> ❌ **Không cam kết (ngoài phạm vi 3 tháng):** Production VNPay thật (chỉ sandbox), payment reconciliation tự động hoàn cọc (sẽ làm tay đến khi có quầy thật), Computer Vision so sánh ảnh trước/sau (đã liệt kê ở Advanced scope), voice assistant, recommendation engine.

### 1.6. Phản biện (Phase 2 Cá nhân → Team)

| Người | Phản biện |
|---|---|
| Thái Anh | "Lời hứa có quá rộng không? Tháng 1 đã có 50% LMS-023 — nhưng nếu Gcar phản hồi ADR chậm 1 tuần thì lùi sang tháng 2. Nên nói 'mục tiêu thận trọng: hoàn tất 50%'." |
| Trung | "Slide 3 có 4 ô 🟡 — nên chuyển 2 ô (VNPay + Luật sư) thành cam kết có điều kiện rõ ràng hơn ở Slide 5. Slide 5 đã có rồi, ổn." |

**Team chốt:** Giữ slide 5 nguyên văn — lời hứa có 3 mức (cam kết/có điều kiện/ngoài phạm vi) rõ ràng, không hứa quá bằng chứng.

---

## 2. RACI Matrix — Toàn bộ ADR 0011 + 0012 (12 công việc)

> **R** = Responsible (người thực hiện) · **A** = Accountable (người chịu trách nhiệm cuối — DUY NHẤT) · **C** = Consulted (cần hỏi ý kiến) · **I** = Informed (cần thông báo)
>
> **Team 2 người:** Vài việc nhỏ 1 người vừa R vừa A (khuyến nghị slide), **không** có việc nào có 2 Accountable.

| # | Công việc | R | A | C | I |
|---|---|---|---|---|---|
| 1 | Migration schema `regions`/`branches`/`vehicles` (từ YAML → DB) | Thái Anh | **Trung** | Admin Gcar, Luật sư Gcar | Manager, Reviewer |
| 2 | Code RBAC `branch_scope(user)` — phạm vi theo `branch_id` | Thái Anh | **Trung** | Luật sư Gcar | Customer, Manager |
| 3 | 6-role login UI (Admin/Manager/Reviewer/Worker/Signer/Customer) | Trung | **Trung** | Admin Gcar | All 6 roles |
| 4 | Bản đồ Leaflet + OpenStreetMap tìm cơ sở gần | Thái Anh | **Trung** | Customer (test UX), Admin Gcar | Manager, Reviewer |
| 5 | Ký 2 bên hợp đồng (Customer ký → Signer ký → PDF lưu 1 lần) | Thái Anh | **Trung** | Luật sư Gcar, Admin Gcar | Customer, Worker |
| 6 | Bảng giá versioned (`policy_versions`) — mỗi yêu cầu giữ phiên bản lúc đặt | Trung | **Thái Anh** | Admin Gcar, Kế toán Gcar | Customer (chỉ xem phiên bản của mình) |
| 7 | Audit hash-chain theo phạm vi chi nhánh | Thái Anh | **Thái Anh** | Luật sư Gcar (yêu cầu tuân thủ) | Admin Gcar, Manager |
| 8 | Đăng ký VNPay merchant sandbox (lấy TMN + hash secret) | Thái Anh | **Thái Anh** | Kế toán Gcar, VNPay support | Admin Gcar |
| 9 | Tích hợp IPN endpoint VNPay `https://gcar-p030.vercel.app/api/v1/payments/vnpay/ipn` | Trung | **Thái Anh** | VNPay support, Kế toán Gcar | Customer, Reviewer |
| 10 | Quầy nhận xe UI cho Signer (thu tiền + xác nhận đã thu + ký) | Trung | **Trung** | Admin Gcar (quy trình vận hành) | Worker, Manager |
| 11 | Thiết kế lịch bàn giao + checklist 12 ảnh (FR-RENT-05, FR-VEH-01..05) | Thái Anh | **Trung** | Worker, Customer (test thật) | Manager, Reviewer |
| 12 | Migration MySQL staging → production (dump Aiven, chạy script) | Thái Anh | **Thái Anh** | Admin Gcar (duyệt downtime) | All 6 roles (đăng nhập lại) |

### 2.1. Tổng kết trách nhiệm (Gate 2)

| Người | Số việc làm **R** | Số việc làm **A** | Tổng gánh |
|---|---|---|---|
| Thái Anh | 7 | 5 | 12 |
| Trung | 5 | 7 | 12 |

> **Không có việc nào có 2 Accountable.** Phân bổ tương đối đều vì team 2 người.

### 2.2. Risk RACI

- **Single point of failure:** Trung là A cho 7/12 việc — nếu Trung nghỉ/bận → Thái Anh phải cover A → đề xuất **Outsource backup reviewer** cho 1-2 việc (sẽ nói ở Phase 3 — AI Team Design).
- **Phụ thuộc bên ngoài:** Cả 12 việc đều có stakeholder bên ngoài trong cột C — đây là điểm rủi ro nếu Luật sư/VNPay/Kế toán Gcar chậm (xem Stakeholder Map để hiểu rõ).

---

## 3. Gate 2 Checklist

| Tiêu chí | Đạt? |
|---|---|
| Pitch có **kết luận đầu tiên** (Conclusion First) | ✅ Slide 1 — kết luận 1 câu trong 30 giây |
| Pitch **không hứa vượt bằng chứng** — có 3 mức cam kết | ✅ Slide 5 (cam kết/có điều kiện/ngoài phạm vi) |
| RACI có **đúng 1 Accountable** cho mỗi công việc | ✅ 12/12 việc |
| Có R, A, C, I cho mỗi việc | ✅ 12/12 việc |
| RACI tách R và A khi team đủ người | ✅ Tách 9/12 việc; 3/12 việc vừa R vừa A (R=A=Thái Anh hoặc R=A=Trung) cho việc độc lập |

---

## 4. Câu hỏi team hay gặp

**Q1: Tại sao Trung là A cho việc UI (#3) mà R cũng Trung?**
→ Đó là việc độc lập, không có người review thứ 2 trong team. Theo slide rule-of-thumb, team rất nhỏ có thể R=A. **Cảnh báo:** Nếu lỡ sai → không ai check → nên rủ Reviewer thật của Gcar vào vòng test trước khi merge (đã ghi ở cột C một số việc).

**Q2: Tại sao không cho AI Agent là R cho việc nào?**
→ Theo `docs/01-PROJECT-BRIEF.md` §7 + `docs/architecture_diagram.md` nguyên tắc cốt lõi: **"LLM KHÔNG phải nguồn sự thật"** — AI chỉ R được ở Pattern A (trích nhu cầu, tóm tắt có căn cứ, định tuyến), không R cho bất kỳ việc kinh doanh nào trong 12 việc này. AI chỉ hỗ trợ dev (R trong viết test, generate code skeleton) nhưng **không trong RACI chính thức này**.