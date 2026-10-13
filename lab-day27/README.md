# GCAR Contract Generation Agent — README

> **Track 1 Day 27 Lab · 120 phút · Team AAA (2 người)**
> **Bài nộp:** Stakeholder Map → Pitch & RACI → AI Team Design → Team Health & Growth Plan → Repo GitHub + 1 PDF ≤ 4 trang
> **Tên nhóm:** **AAA**

---

## Team

| # | Họ tên | MSSV | Vai trò |
|---|---|---|---|
| 1 | Đặng Văn Thái Anh | 2A202602407 | Trưởng nhóm / tạo repo / Backend & AI Engineer |
| 2 | Đàm Quang Trung | 2A202602525 | Tech Lead / Front-end & DevOps |

> **Team AAA** gồm 2 thành viên thay vì 3-5 theo yêu cầu đề bài — đã được phép ngoại lệ (xác nhận với giảng viên trước khi bắt đầu Lab).

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
├── README.md                             ← (file này) Team + dự án + format
├── 01-stakeholder-map.md                 ← Phase 1
├── 02-pitch-and-raci.md                  ← Phase 2
├── 03-ai-team-design.md                  ← Phase 3
├── 04-team-health-growth-plan.md         ← Phase 4
└── deliverables/
    └── gcar-day27-summary.pdf            ← PDF tóm tắt ≤ 4 trang
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
| 2 — Pitch & RACI | 30 phút | 🔜 |
| 3 — AI Team Design | 25 phút | ⏳ |
| 4 — Team Health & Growth Plan | 25 phút | ⏳ |
| 5 — Tự kiểm & Nộp | 15 phút | ⏳ |