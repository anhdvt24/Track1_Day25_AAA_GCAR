# GCAR Contract Generation Agent — AI Team Design

> **Phase 3 — Track 1 Day 27 Lab** · 25 phút · Team
> **Dự án:** GCAR Contract Generation Agent · **Mục tiêu:** ADR 0011 + 0012 trong 3 tháng
> **Team AAA:** Đặng Văn Thái Anh (2A202602407), Đàm Quang Trung (2A202602525)

---

## 1. AI Team Architecture — **Hybrid**

### 1.1. Tại sao chọn Hybrid (không phải Centralized hay Embedded)

| Architecture | Định nghĩa | Phù hợp khi | Tại sao KHÔNG chọn |
|---|---|---|---|
| **Centralized** | 1 team AI trung tâm phục vụ nhiều sản phẩm | Công ty lớn, nhiều domain | Gcar team 2 người + 1 dự án = quá mức cần thiết |
| **Embedded** | AI Agent là 1 thành viên, nằm trong team kinh doanh | Team có 1 AI engineer + nhiều domain expert | Hiện tại Trung + Thái Anh đều là dev, không có domain expert nội bộ → AI chưa thể "nằm trong" team nghiệp vụ |
| **Hybrid** ✅ | Core team tự làm phần cốt lõi + Outsource/Partner cho phần chuyên biệt | Team nhỏ, cần ship nhanh, budget hẹp | **Phù hợp nhất** với 2 người + 3 tháng + cần VNPay, bản đồ, legal review |

### 1.2. Cấu trúc Hybrid cụ thể của Gcar

```text
┌─────────────────────────────────────────────────────────────────┐
│                     GCAR AI TEAM (Hybrid)                       │
│                                                                 │
│  ┌─────────────────── CORE TEAM (nội bộ) ─────────────────────┐ │
│  │  • Đặng Văn Thái Anh (Backend/AI Engineer — L3)            │ │
│  │  • Đàm Quang Trung (Tech Lead/Frontend — L3/L2)            │ │
│  │  • + AI Agent (DeepSeek qua OpenRouter) — 1 node LLM duy  │ │
│  │    nhất trong workflow nghiệp vụ (extract + ReAct reason)  │ │
│  └────────────────────────────────────────────────────────────┘ │
│                           ↕ giao tiếp                            │
│  ┌────────────── OUTSOURCE (thuê ngoài ngắn hạn) ────────────┐  │
│  │  • Freelance Frontend (hỗ trợ UI production-grade)         │  │
│  │  • Part-time VNPay integrator (1-2 sprint)                 │  │
│  │  • Part-time DevOps (CI/CD + monitoring staging)           │  │
│  └────────────────────────────────────────────────────────────┘  │
│                           ↕ hợp đồng                             │
│  ┌──────────────── PARTNER ───────────────────────────────── │
│  │  • Founder/Admin Gcar — duyệt scope, cấp account           │ │
│  │  • Luật sư tư vấn Gcar — review hợp đồng 1-2 lần/tháng   │ │
│  │  • Ban giảng viên AI20K — feedback kiến trúc               │ │
│  │  • Mentor VinAI — review gate G1-G6                        │ │
│  └────────────────────────────────────────────────────────────┘  │
└─────────────────────────────────────────────────────────────────┘
```

---

## 2. Core Roles — Vai trò cốt lõi (5, KHÔNG phải 12)

> Theo luật Lab: "Không thiết kế team theo kiểu 'càng nhiều chức danh càng tốt'. Chỉ chọn role / capability thực sự cần."

### 2.1. 5 Core Roles hiện tại

| # | Core Role | Người cover | L1/L2/L3 hiện tại | L1/L2/L3 mục tiêu (30 ngày) | Quan trọng vì |
|---|---|---|---|---|---|
| 1 | **Tech Lead / Product Owner** | Trung | L3 | L3 (giữ) | Quyết định kiến trúc, dẫn dắt team, giao tiếp với Admin Gcar |
| 2 | **Backend/AI Engineer** | Thái Anh | L3 | L3 (giữ) | FastAPI, LangGraph, RAG, MySQL — đã 640 test pass |
| 3 | **Frontend Engineer** | Trung (+ freelance) | L2 | **L3** | Bản đồ Leaflet, 6-role UI, UI/UX demo |
| 4 | **DevOps / QA** | Chia đôi (Thái Anh 0.5 + Outsource 0.5) | L1 | **L2** | CI/CD auto-deploy, monitoring, test |
| 5 | **Legal/Policy Reviewer** | Luật sư Gcar (Partner) | L1 (chưa có HĐ) | **L2** (sau khi ký HĐ) | Review hợp đồng, CL-17, điều khoản pháp lý |

### 2.2. Vai trò KHÔNG cần ngay (để tránh "thêm cho có")

- ❌ **Data Engineer riêng** — Lượng data chưa đủ lớn (vài nghìn booking), SQLAlchemy + MySQL hiện tại đủ dùng
- ❌ **MLOps Engineer** — Chưa có model riêng cần train/fine-tune, đang dùng DeepSeek API
- ❌ **UX Designer** — UI demo chưa cần production-grade, dùng mockup Daisy đã có
- ❌ **Security Engineer chuyên biệt** — Đã có RBAC + audit hash-chain, chưa cần pentest đến khi pilot
- ❌ **PM riêng** — Team 2 người, Trung đang cover PM
- ❌ **Backend Engineer thứ 2** — Khi Gcar mở chi nhánh thứ 3, **mới** cần hire (xem §3)

---

## 3. Capability Gap & Priority Resourcing (Hire / Outsource / Partner)

### 3.1. 6 Capability Gap trong 3 tháng tới

| # | Capability Gap | Hiện tại | Mục tiêu | **Hire / Outsource / Partner** | Vì sao chọn cách này |
|---|---|---|---|---|---|
| 1 | **Legal review hợp đồng** (CL-17, điều khoản Bên A, xử lý dữ liệu cá nhân) | L1 (chưa có luật sư) | L2 | **PARTNER** — Luật sư tư vấn Gcar | Không tuyển full-time: chỉ cần 1-2 buổi/tháng × 1-2h, không đủ workload cho 1 người full-time. Partner đúng chuyên môn + chi phí thấp hơn Hire. Đã ghi trong Stakeholder Map §4.2. |
| 2 | **VNPay sandbox + IPN integration** | L1 (chưa có merchant) | L2 | **OUTSOURCE** — Part-time dev VNPay (1 sprint) | Có template chuẩn từ VNPay, dev có kinh nghiệm làm trong 5-7 ngày. Không cần giữ full-time sau khi xong vì payment chỉ là 1 trong 6 workflow chính. |
| 3 | **UI production-grade** (responsive, accessibility WCAG 2.1 AA, mobile-first) | L2 (vanilla JS) | L3 | **OUTSOURCE** — Freelance Frontend 2 sprint | Trung đang L2, có thể học lên L3 trong 30 ngày nhưng chậm. Outsource 1 người chuyên Frontend 2 sprint (6 tuần) để Trung tập trung Tech Lead. Sau 2 sprint → chỉ Trung maintain. |
| 5 | **DevOps/QA chuyên biệt** (CI/CD, monitoring, on-call) | L1 (chia đôi với dev) | L2 | **OUTSOURCE** — Part-time DevOps (ongoing) | Team 2 người không đủ người để trực 24/7. Outsource part-time (~10h/tuần) để setup Grafana + Sentry + on-call rotation. |
| 6 | **Backend Engineer thứ 2** (khi Gcar mở chi nhánh thứ 3) | L0 (chưa có) | L1 | **HIRE** — Full-time Backend (Q2/2027) | Khi mở chi nhánh thứ 3 (dự kiến Q2/2027) → 1 người không đủ để cover code review + on-call + scope mới. Hire full-time là đúng lúc. Hiện tại KHÔNG hire vì: (i) budget hẹp, (ii) chưa có đủ việc cho 1 người full-time trong 3 tháng tới, (iii) Outsourcer/Partner có thể cover workload tăng đột biến. |
| 7 | **VNPay support / Kế toán Gcar** (mở merchant, đối soát payment) | L0 | L1 | **PARTNER** — Kế toán Gcar | Không thuộc team tech, nhưng là blocker. Partner để mở merchant + ký hợp đồng VNPay. Ghi trong Stakeholder Map (Kế toán Gcar stance 🟡 chờ merchant). |

### 3.2. Tổng kết Priority Resourcing

| Cách | Số lượng | Vai trò | Chi phí tương đối |
|---|---|---|---|
| **Hire** (full-time) | 1 | Backend #2 (khi mở chi nhánh 3, Q2/2027) | $$$ |
| **Outsource** (part-time / freelance) | 3 | VNPay integrator · Freelance Frontend · DevOps part-time | $$ |
| **Partner** (hợp tác dài hạn) | 3 | Luật sư Gcar · Kế toán Gcar · Mentor AI20K | $ |

> **Tại sao KHÔNG chọn "toàn Hire":** Team 2 người + budget AI20K cohort không đủ cho 5-6 nhân viên full-time trong 3 tháng. Outsource + Partner giúp tận dụng chuyên gia không cần full-time.

---

## 4. Gate 3 Checklist

| Tiêu chí | Đạt? |
|---|---|
| Architecture chọn có **lý do rõ ràng** (không chọn đại) | ✅ Hybrid vì team 2 người + 3 tháng + budget hẹp + cần chuyên biệt |
| **Không** thiết kế team theo kiểu "càng nhiều vai trò càng tốt" | ✅ Chỉ 5 core roles; 6 vai trò đã loại bỏ có lý do (PM, MLOps, Data, Security, UX, BE #2 hiện tại) |
| Mỗi capability gap có **Hire / Outsource / Partner** rõ ràng | ✅ 6/6 gap có quyết định |
| Có **lý do vì sao** chọn Hire / Outsource / Partner | ✅ Ghi rõ lý do cho cả 6 |
| **Cân nhắc cả 3** (không chỉ Hire) | ✅ Hire 1 · Outsource 3 · Partner 3 |
| Có **đủ năng lực cốt lõi** để đạt milestone 3 tháng | ✅ Core 5 roles có L2+ trở lên sau 30 ngày |

---

## 5. Rủi ro & Mitigation

| Rủi ro | Mitigation |
|---|---|
| **Outsource Frontend không hiểu domain Gcar** | Viết 1 tài liệu "Domain Glossary for Outsourcer" (10 khái niệm chính: chi nhánh, vai trò, ký 2 bên, v.v.) — Trung chịu trách nhiệm, deadline **Day 5** |
| **VNPay sandbox không verify được IPN** | Backup plan: dùng webhook.site + tự viết test IPN handler; nếu vẫn fail → chuyển sang Partner Kế toán Gcar xử lý trực tiếp |
| **Luật sư Gcar không ký HĐ** | Backup: dùng Chuyên gia pháp lý độc lập (đã ghi trong Stakeholder Map B6); chi phí cao hơn 30-50% nhưng ship được |
| **Freelance Frontend nghỉ giữa chừng** | Backup: Trung đang học lên L3, có thể cover nếu cần 1 sprint thêm |