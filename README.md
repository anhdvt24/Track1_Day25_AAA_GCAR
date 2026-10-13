# GCAR Contract Generation Agent — README

> **Track 1 Day 27 Lab · 120 phút · Team AAA (2 người)**
> **Bài nộp:** Stakeholder Map → Pitch & RACI → AI Team Design → Team Health & Growth Plan → Repo GitHub + 1 PDF ≤ 4 trang
> **Tên nhóm:** **AAA**
> **Trạng thái tổng:** ✅ **HOÀN TẤT** (đã push repo, xuất PDF, sẵn sàng nộp)

---

## Team

| # | Họ tên | MSSV | Vai trò |
|---|---|---|---|
| 1 | Đặng Văn Thái Anh | 2A202602407 | Trưởng nhóm / tạo repo / Backend & AI Engineer |
| 2 | Đàm Quang Trung | 2A202602525 | Tech Lead / Front-end & DevOps |

> **Team AAA** gồm 2 thành viên thay vì 3-5 theo yêu cầu đề bài — đã được phép ngoại lệ (xác nhận với giảng viên trước khi bắt đầu Lab).

---

## 📊 Trạng thái Task (Task Status)

### Phase Lab Day 27 (120 phút)

| # | Phase | Thời gian | Output | Trạng thái |
|---|---|---|---|---|
| 0 | Chốt phạm vi | 5 phút | Setup repo + README | ✅ Hoàn tất |
| 1 | Stakeholder Map | 20 phút | `01-stakeholder-map.md` (10 stakeholder + 4 chiến lược) | ✅ Hoàn tất |
| 2 | Pitch & RACI | 30 phút | `02-pitch-and-raci.md` (Pitch + RACI 12 việc) | ✅ Hoàn tất |
| 3 | AI Team Design | 25 phút | `03-ai-team-design.md` (Hybrid + 6 capability gap) | ✅ Hoàn tất |
| 4 | Team Health & Growth Plan | 25 phút | `04-team-health-growth-plan.md` (4 chiều + 3 actions) | ✅ Hoàn tất |
| 5 | Tự kiểm & Nộp | 15 phút | `05-phase5-checklist.md` + `combined_markdown.pdf` + push repo | ✅ Hoàn tất |

### Gate Checklist (đề bài yêu cầu)

| Gate | Tiêu chí | Trạng thái |
|---|---|---|
| **Gate 1** | Stakeholder Map có ≥ 6 stakeholder cụ thể, có Influence×Interest + stance thực tế | ✅ 10 stakeholder |
| **Gate 2** | Pitch "kết luận trước" + bằng chứng + small ask + 1 phản biện; RACI 12 việc có đúng 1 A | ✅ |
| **Gate 3** | AI Team Design có lý do rõ ràng cho architecture; 6 capability gap với Hire/Outsource/Partner | ✅ Hybrid |
| **Gate 4** | Team Health đủ 4 khía cạnh; Growth Plan ≤ 3 actions có owner + deadline + dấu hiệu hoàn thành | ✅ 3/3 |
| **Gate 5** | Repo public + 1 PDF ≤ 4 trang + README đúng format | ✅ Đã push |

### Action 30 ngày tới (sau Lab)

| # | Hành động | Owner | Deadline | Trạng thái |
|---|---|---|---|---|
| **1** | Setup GitHub Action auto-deploy staging + enable Sentry | Thái Anh | Day 14 | ⬜ Chưa bắt đầu |
| **2** | Hoàn tất 50% LMS-023 (chi nhánh + RBAC) | Trung | Day 14 | ⬜ Chưa bắt đầu |
| **3** | Thêm RAG eval vào CI (faithfulness < 4.5/5 → fail) | Thái Anh | Day 21 | ⬜ Chưa bắt đầu |

### Hành động tuần 1–2 (Stakeholder ưu tiên)

| # | Hành động | Owner | Deadline | Trạng thái |
|---|---|---|---|---|
| S1 | Ping Admin Gcar xin intro luật sư | Thái Anh | Day 3 | ⬜ |
| S2 | Email đăng ký merchant VNPay sandbox | Thái Anh | Day 4 | ⬜ |
| S3 | Legal review checklist (12 điểm) | Trung | Day 5 | ⬜ |
| S4 | Walkthrough 1 trang A4 cho Reviewer | Thái Anh | Day 7 | ⬜ |
| S5 | Deploy IPN endpoint VNPay lên Vercel production | Trung | Day 7 | ⬜ |
| S6 | Shadow 2h tại HN-01 với Reviewer | Trung | Day 10 | ⬜ |

---

## Dự án

**GCAR Contract Generation Agent** — AI Agent cho thuê xe điện (Booking, Contract Generation & Handover).

- **Stack:** FastAPI + LangGraph + DeepSeek + MySQL 8 + ChromaDB RAG + Leaflet + JWT/RBAC
- **Trạng thái MVP:** 640 test pass, 47 endpoint, 5 vai trò (sắp mở rộng lên 6 theo ADR 0011)
- **PRD:** [`docs/01-PROJECT-BRIEF.md`](../docs/01-PROJECT-BRIEF.md), [`docs/02-PRD.md`](../docs/02-PRD.md)
- **Tổng quan kiến trúc:** [`docs/architecture_diagram.md`](../docs/architecture_diagram.md)
- **Tài liệu chi tiết:** thư mục [`docs/`](../docs/) trong repo gốc

---

## Mục tiêu 1–3 tháng

Triển khai 2 ADR đang ở trạng thái **Proposed** (đã viết 2026-10-06, chưa code):

1. **ADR 0011 — Chi nhánh & RBAC 6 vai trò** ([`docs/2026-10-06-tom-tat-thiet-ke.md`](../docs/2026-10-06-tom-tat-thiet-ke.md) §2):
   - 6 vai trò: Admin / Manager / Reviewer / Worker / Signer / Customer
   - Database phân vùng theo `branch_id` (HN-01, HN-02, HCM-01…)
   - Bản đồ tìm cơ sở gần (Leaflet + OpenStreetMap)
   - Ký hai bên + audit log theo phạm vi

2. **ADR 0012 — Thanh toán** ([`docs/2026-10-06-tom-tat-thiet-ke.md`](../docs/2026-10-06-tom-tat-thiet-ke.md) §7):
   - **Online:** VNPay sandbox (HMAC-SHA512, IPN)
   - **Khi nhận xe:** Quầy nhận xe — Signer thu tiền + ký tại chỗ
   - **Không đến:** quá giờ nhận xe + 2h → tự huỷ

**Mục tiêu đo lường:**
- Sprint LMS-023 (chi nhánh + RBAC) + LMS-024 (thanh toán) hoàn tất 50% scope trong 14 ngày
- Demo được end-to-end với 1 chi nhánh HN-01 thật (có Reviewer/Worker/Signer hoạt động)
- Test pass ≥ 700 (thêm 60 test cho RBAC scope + payment flow)

---

## Cấu trúc repo lab

```
gcar-day27-lab/                          ← repo này (Team AAA)
├── README.md                             ← (file này) Team + dự án + Task Status
├── 00-timeline.md                        ← Timeline tổng hợp tất cả mốc thời gian
├── 01-stakeholder-map.md                 ← Phase 1
├── 02-pitch-and-raci.md                  ← Phase 2
├── 03-ai-team-design.md                  ← Phase 3
├── 04-team-health-growth-plan.md         ← Phase 4
├── 05-phase5-checklist.md                ← Phase 5
├── combined_markdown.md                  ← Ghép 4 file để xuất PDF
└── combined_markdown.pdf                 ← PDF ≤ 4 trang đã nộp
```

---

## Format làm bài

- **Công cụ soạn:** Markdown thuần (VSCode / Obsidian / Typora), xuất PDF bằng VSCode extension "Markdown PDF" hoặc tương đương
- **Collaborative:** Chia file cá nhân trước (`draft-thai-anh.md`, `draft-trung.md`) → gộp vào file team
- **Output cuối:** Repo GitHub public + 1 PDF ≤ 4 trang (paste link nộp theo mục 10 của đề bài)

---

## Người tổng hợp & nộp bài

- **Trưởng nhóm / tạo repo:** Đặng Văn Thái Anh (2A202602407)
- **Nộp bài:** Sau khi Phase 5 hoàn tất, copy link repo và submit theo hướng dẫn mục 10 của đề bài Day 27.

---

## Timeline (120 phút)

| Phase | Thời gian | Trạng thái |
|---|---|---|
| 0 — Chốt phạm vi | 5 phút | ✅ |
| 1 — Stakeholder Map | 20 phút | ✅ |
| 2 — Pitch & RACI | 30 phút | ✅ |
| 3 — AI Team Design | 25 phút | ✅ |
| 4 — Team Health & Growth Plan | 25 phút | ✅ |
| 5 — Tự kiểm & Nộp | 15 phút | ✅ |

> ✅ **Bài Lab đã hoàn tất.** Trưởng nhóm copy link repo nộp theo mục 10 đề bài.