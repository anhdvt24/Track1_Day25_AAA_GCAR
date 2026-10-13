# GCAR Day 27 Lab — Combined Markdown (để xuất PDF)

> File này ghép 4 artefact (Trang 1-4 PDF) để dễ xuất PDF ≤ 4 trang.
> **Team AAA:** Đặng Văn Thái Anh (2A202602407), Đàm Quang Trung (2A202602525)

---

## Trang 1 — Stakeholder Map & Strategy

### 1. Ma trận Influence × Interest (10 stakeholder cụ thể)

| Stakeholder | Influence | Interest | Stance | Vùng |
|---|---|---|---|---|
| Founder / Admin Gcar | Cao | Cao | 🟢 Ủng hộ | Champion |
| Manager khu vực (HN-01, HCM-01) | Cao | Cao | 🟢 Ủng hộ | Champion |
| Reviewer chi nhánh HN-01 | Cao | Cao | 🟢 Ủng hộ | Champion |
| Luật sư tư vấn Gcar | Cao | Cao | 🔴 Chưa ủng hộ | Champion tiềm năng |
| Kế toán Gcar | Cao | Cao | 🟡 Trung lập | Champion tiềm năng |
| Sở GTVT HN/HCM | Cao | Thấp | 🟡 Trung lập | Bystander |
| VNPay support | Cao | Thấp | 🟡 Trung lập | Bystander |
| Khách cá nhân 1-3 ngày / cuối tuần | Thấp | Cao | 🟢 Ủng hộ | Supporter |
| Khách doanh nghiệp dài hạn | Thấp | Cao | 🟡 Trung lập | Supporter |
| Worker / Signer chi nhánh, Ban giảng viên AI20K, Đối tác bảo hiểm | Thấp | Cao/Thấp | 🟢 / 🟡 | Supporter / Bystander |

> Lưu ý: Stance **không** luôn trùng nhãn quadrant — Luật sư + Kế toán Gcar là ví dụ rõ nhất.

### 2. 4 stakeholder ưu tiên & hành động

| Stakeholder | Hành động 1-2 tuần tới | Owner | Deadline |
|---|---|---|---|
| 🌟 **Founder / Admin Gcar** | Gửi ADR 0011 + 0012 + prototype bản đồ chi nhánh Leaflet + 6-book login UI; book 30' demo | Thái Anh | Thứ Sáu tuần này |
| 🌟 **Reviewer HN-01** | Viết walkthrough 6 trạng thái mới; book 2h shadow tại HN-01 | Thái Anh + Trung | Day 7 / Day 10 |
| ⚠️ **Luật sư Gcar** (chưa ký HĐ) | Chuẩn bị Legal review checklist 12 điểm; ping Admin Gcar xin intro luật sư | Trung + Thái Anh | Day 5 / Day 3 |
| ⚠️ **VNPay support** (chậm verify IPN) | Email đăng ký merchant sandbox (gửi qua Kế toán Gcar); deploy IPN endpoint `/api/v1/payments/vnpay/ipn` | Thái Anh + Trung | Day 4 / Day 7 |

---

## Trang 2 — Pitch & RACI

### 1. Pitch (Conclusion First — hướng đến Admin Gcar)

> **Kết luận (30 giây đầu):** Trong 3 tháng tới, team Gcar sẽ đưa dự án từ MVP chạy được (640 test pass) lên vận hành thật ở 2 chi nhánh đầu tiên (HN-01 + HCM-01), với 6 vai trò phân quyền theo phạm vi và 2 kênh thanh toán (VNPay online + quầy nhận xe).

**Bằng chứng hiện có:** 640 test pass · 47 endpoint · 5 vai trò (RBAC + audit hash-chain) · RAG faithfulness 5.00/5 · 44/44 P2.4 case pass · ADR 0011 + 0012 đã viết xong · Template hợp đồng theo HĐCTXTL đã điều chỉnh cho Gcar.

**Small ask (3 mức cam kết):**
- ✅ **Cam kết:** Migration schema chi nhánh + RBAC scope + 6-role UI + bản đồ + ký 2 bên + bảng giá versioned + audit hash-chain
- 🟡 **Có điều kiện:** VNPay sandbox (cần Kế toán Gcar mở merchant 5-7 ngày); CL-17 (cần Luật sư Gcar 2-4 tuần)
- ❌ **Ngoài phạm vi 3 tháng:** Production VNPay thật, hoàn cọc tự động, Computer Vision, Voice Assistant

**Phản biện + cách xử lý:**
- "Lời hứa có quá rộng không?" → Nói rõ "50% LMS-023 trong 14 ngày"; có điều kiện backup rõ ràng
- "VNPay + Luật sư 🟡 — nói rõ cam kết có điều kiện" → Đã có ở Small ask mức 🟡

### 2. RACI Matrix (12 công việc — mỗi việc đúng 1 Accountable)

| # | Công việc | R | A | C | I |
|---|---|---|---|---|---|
| 1 | Migration schema `regions`/`branches`/`vehicles` | Thái Anh | **Trung** | Admin Gcar, Luật sư | Manager, Reviewer |
| 2 | RBAC `branch_scope(user)` | Thái Anh | **Trung** | Luật sư | Customer, Manager |
| 3 | 6-role login UI | Trung | **Trung** | Admin Gcar | All 6 roles |
| 4 | Bản đồ Leaflet + OSM tìm cơ sở gần | Thái Anh | **Trung** | Customer, Admin | Manager, Reviewer |
| 5 | Ký 2 bên hợp đồng (Customer → Signer → PDF) | Thái Anh | **Trung** | Luật sư, Admin | Customer, Worker |
| 6 | Bảng giá versioned (`policy_versions`) | Trung | **Thái Anh** | Admin, Kế toán | Customer |
| 7 | Audit hash-chain theo phạm vi chi nhánh | Thái Anh | **Thái Anh** | Luật sư | Admin, Manager |
| 8 | Đăng ký VNPay merchant sandbox | Thái Anh | **Thái Anh** | Kế toán, VNPay | Admin |
| 9 | Tích hợp IPN endpoint VNPay | Trung | **Thái Anh** | VNPay, Kế toán | Customer, Reviewer |
| 10 | Quầy nhận xe UI cho Signer | Trung | **Trung** | Admin | Worker, Manager |
| 11 | Lịch bàn giao + checklist 12 ảnh (FR-VEH-01..05) | Thái Anh | **Trung** | Worker, Customer | Manager, Reviewer |
| 12 | Migration MySQL staging → production | Thái Anh | **Thái Anh** | Admin | All 6 roles |

**Tổng kết:** Thái Anh R=7, A=5 · Trung R=5, A=7. Cân bằng. Không có 2 A cho cùng việc.

---

## Trang 3 — AI Team Design

### 1. Architecture: **Hybrid** (lý do: team 2 người + 3 tháng + budget hẹp + cần chuyên biệt)

```text
CORE (2 người + AI Agent)
├── Tech Lead / Product Owner (Trung — L3)
├── Backend / AI Engineer (Thái Anh — L3)
├── Frontend Engineer (Trung L2 + freelance — sẽ lên L3)
├── DevOps / QA (chia đôi 0.5 — sẽ lên L2 nhờ Outsource)
└── Legal/Policy Reviewer (Luật sư Gcar — Partner, chưa ký HĐ)

OUTSOURCE (3)
├── Freelance Frontend 2 sprint (UI production-grade)
├── Part-time VNPay integrator 1 sprint
└── Part-time DevOps ongoing (~10h/tuần)

PARTNER (3)
├── Luật sư tư vấn Gcar (1-2 buổi/tháng)
├── Kế toán Gcar (mở merchant sandbox)
└── Mentor AI20K (review gate)
```

### 2. Capability Gap & Priority Resourcing (6 gap)

| # | Gap | Hire / Outsource / Partner | Lý do |
|---|---|---|---|
| 1 | Legal review hợp đồng (CL-17, Bên A) | **Partner** — Luật sư Gcar | Chỉ cần 1-2 buổi/tháng, không full-time |
| 2 | VNPay sandbox + IPN | **Outsource** — Part-time 1 sprint | Có template chuẩn, làm 5-7 ngày xong |
| 3 | UI production-grade | **Outsource** — Freelance 2 sprint | Trung đang học lên L3, Outsource tăng tốc |
| 4 | DevOps/QA chuyên biệt | **Outsource** — Part-time ongoing | 2 người không trực 24/7 |
| 5 | Backend Engineer #2 (khi mở chi nhánh 3) | **Hire** (Q2/2027) | Hiện tại KHÔNG hire — budget hẹp, chưa đủ việc |
| 6 | VNPay support / Kế toán Gcar | **Partner** — Kế toán Gcar | Blocker mở merchant, không thuộc tech |

**Squad Goal:** "Team Gcar sở hữu **ADR 0011 + 0012** và chịu trách nhiệm đưa **GCAR Contract Agent** từ **MVP chạy được (640 test pass)** đến **pilot thật tại chi nhánh HN-01 trong Q1/2027**."

---

## Trang 4 — Team Health & Growth Plan (30 ngày)

### 1. Team Health (4 chiều, điểm TB)

| Khía cạnh | Thái Anh | Trung | TB |
|---|---|---|---|
| Chất lượng AI | 4 | 3 | 3.5 |
| Tiến độ | 3 | 2 | 2.5 |
| Tinh thần team | 4 | 4 | 4.0 |
| **Tốc độ ra sản phẩm** | 2 | 3 | **2.5** ⭐ |

**Vấn đề ưu tiên:** Tốc độ ra sản phẩm (mỗi deploy mất 3-5 ngày, chưa có auto-deploy) — ảnh hưởng trực tiếp milestone pilot Q1/2027.

### 2. Competency cần nâng

| Role | Level hiện tại | → Mục tiêu | Action 30 ngày |
|---|---|---|---|
| DevOps / QA | L1 (chỉ biết `make test`) | **L2** (CI/CD + monitoring) | Xây GitHub Action: push `develop` → test → auto-deploy staging → comment preview |

### 3. Growth Plan 30 ngày (3 hành động)

| # | Hành động | Owner | Deadline | Dấu hiệu hoàn thành |
|---|---|---|---|---|
| 1 | **Setup GitHub Action auto-deploy staging** + Sentry cho runtime errors | Thái Anh | Day 14 | (a) File `.github/workflows/deploy-staging.yml` chạy được; (b) PR mới có comment link preview ≤5'; (c) Sentry ≥1 alert test pass |
| 2 | **Hoàn tất 50% LMS-023** (chi nhánh + RBAC + 6-role login UI cơ bản, KHÔNG gồm bản đồ) | Trung | Day 14 | (a) Branch `feature/branch-rbac` merged; (b) Migration script chạy trên MySQL staging; (c) Test mới ≥30 case → tổng ≥690 pass; (d) 6-role login UI demo với 3 tài khoản giả lập |
| 3 | **Thêm RAG eval vào CI** — chạy 30 case vàng; fail nếu faithfulness <4.5 hoặc Hit@1 <80% | Thái Anh | Day 21 | (a) Job `eval-rag` trong GitHub Actions; (b) PR thay đổi prompt/RAG có check eval fail; (c) `eval-results-ci.md` sinh tự động mỗi PR |

**Check-in:** W1 Day 7 · W2 Day 14 (nếu miss → họp 30', quyết cắt scope LMS-023.5) · W3 Day 21 · W4 Day 30 tổng kết.