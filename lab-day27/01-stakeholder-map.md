# GCAR Contract Generation Agent — Stakeholder Map & Strategy

> **Phase 1 — Track 1 Day 27 Lab** · 20 phút · Cá nhân → Team
> **Dự án:** GCAR Contract Generation Agent (AI cho thuê xe điện — Booking, Contract & Handover)
> **Mục tiêu 1-3 tháng:** Triển khai ADR 0011 (chi nhánh + 6 vai trò) + ADR 0012 (thanh toán VNPay / quầy)
> **Team AAA:** Đặng Văn Thái Anh (2A202602407), Đàm Quang Trung (2A202602525)

---

## 1. Phương pháp làm

Mỗi thành viên liệt kê **6 stakeholder cụ thể** (có tên/nhóm + bối cảnh), **KHÔNG** viết chung chung như "khách hàng". Sau đó team gộp danh sách, loại trùng, đặt từng stakeholder lên ma trận **Influence × Interest**, rồi đánh dấu **stance (mức độ ủng hộ)** thực tế:

- 🟢 Ủnghộ
- 🟡 Trung lập
- 🔴 Chưa ủng hộ / phản đối

> Nhãn **Champion / Blocker / Supporter / Bystander** trong slide chỉ giúp gọi tên vùng; **stance thực tế mới là tín hiệu để hành động**.

---

## 2. Cá nhân — Liệt kê stakeholder

### 2.1. Đặng Văn Thái Anh (Back-end / AI Engineer)

| # | Stakeholder cụ thể | Vì sao đưa vào |
|---|---|---|
| A1 | **Founder / Admin Gcar** (Product Owner) | Người duyệt scope ADR 0011/0012, cấp tài khoản Manager, quyết định rollout chi nhánh |
| A2 | **Manager khu vực Miền Bắc** (HN-01, HN-02 sau này) | Cấp tài khoản Reviewer/Worker/Signer, chịu trách nhiệm KPI vận hành khu vực |
| A3 | **Reviewer chi nhánh HN-01** | Người duyệt hồ sơ khách + hợp đồng hàng ngày; là bottleneck chính của pipeline |
| A4 | **Luật sư tư vấn Gcar** (ngoài, hiện chưa có) | Review hợp đồng mẫu (CL-17 hủy chuyến, đối chiếu HĐCTXTL→Gcar, điều khoản Bên A) |
| A5 | **Đội ngũ kế toán Gcar** | Quyết định merchant sandbox VNPay, đối soát payment, quản lý hoàn cọc khi khách hủy |
| A6 | **Khách doanh nghiệp thuê dài hạn** (≥ 7 ngày) | Tạo booking lớn, yêu cầu hóa đơn VAT, payment online bắt buộc |
| A7 | **Ban giảng viên AI20K** (mentor + giảng viên) | Đánh giá 6 gate, review deliverables, có thể mời pilot nếu dự án tốt |
| A8 | **Sở GTVT Hà Nội + TP.HCM** (bên giám sát luật) | Quy định hạng GPLX, giá trần taxi, biển cấm đỗ — chi phối điều khoản hợp đồng |

### 2.2. Đàm Quang Trung (Tech Lead / Front-end)

| # | Stakeholder cụ thể | Vì sao đưa vào |
|---|---|---|
| B1 | **Khách cá nhân thuê 1-3 ngày** (mục tiêu chính của MVP) | Dùng UI chọn xe + đặt cọc online; UX phải đơn giản để họ không bỏ giữa chừng |
| B2 | **Worker tại chi nhánh** (đối chiếu CCCD + GPLX gốc, checklist 12 ảnh) | Người dùng nặng UI checklist; ảnh trước/sau handover là evidence pháp lý |
| B3 | **Signer tại chi nhánh** (ký hợp đồng thay Gcar, thu tiền tại quầy) | Dùng UI "Quầy nhận xe"; nếu UI khó → khách SIGH (quá giờ + 2h tự huỷ) |
| B4 | **VNPay (technical support)** | Cần sandbox merchant, IPN endpoint, hash secret; cản trở nếu chậm verify IPN |
| B5 | **Đối tác bảo hiểm VF (gói Basic 50k/ngày + Advanced 100k/ngày)** | Cấu hình gói bảo hiểm, mức khấu trừ tối đa khách gửi; cản trở nếu mức khấu trừ thay đổi đột ngột |
| B6 | **Chuyên gia pháp lý độc lập** (thuê ngoài 1 lần/tháng) | Review chính sách hủy chuyến (CL-17), hợp đồng HĐCTXTL→Gcar |
| B7 | **Mentor VinAI** (hướng dẫn trực tiếp) | Chấm gate, feedback UI/UX, recommend kiến trúc khi G5 tổng duyệt |
| B8 | **Khách cá nhân thuê cuối tuần / lễ** (giá 800k-950k/ngày) | Nhóm ngày cao điểm; nếu UI báo sai giá hoặc không hiển thị nguồn → khiếu nại |

---

## 3. Team — Stakeholder Map gộp (loại trùng)

Gộp A1 + A1' (Founder/Admin Gcar) và A2 + B0 (Manager khu vực) → giữ nguyên; gộp A7 + B7 (Mentor/giảng viên) → giữ 1; còn lại **10 stakeholder cụ thể** đặt lên ma trận:

```text
                    Interest thấp                          Interest cao
                ┌─────────────────────────┬─────────────────────────────┐
                │                         │                             │
   Influence    │   BYSTANDER             │   CHAMPION                  │
   cao          │   (theo dõi)            │   (làm việc chặt chẽ)       │
                │                         │                             │
                │  • Sở GTVT HN/HCM 🟡     │  • Founder/Admin Gcar 🟢     │
                │  • VNPay support 🟡      │  • Manager khu vực 🟢       │
                │  • Luật sư tư vấn Gcar 🔴│  • Reviewer chi nhánh 🟢    │
                │    (chờ Gcar review)    │  • Kế toán Gcar 🟡 (chờ     │
                │                         │    merchant sandbox)        │
                │                         │  • Chuyên gia pháp lý 🔴    │
                │                         │    (chưa ký HĐ)             │
                ├─────────────────────────┼─────────────────────────────┤
                │                         │                             │
   Influence    │   BYSTANDER             │   SUPPORTER                 │
   thấp         │                         │   (nuôi dưỡng)              │
                │                         │                             │
                │  • Đối tác bảo hiểm 🟡   │  • Khách cá nhân 1-3 ngày 🟢│
                │                         │  • Khách cá nhân cuối tuần 🟢│
                │                         │  • Khách doanh nghiệp 🟡    │
                │                         │    (chờ VAT/extension)      │
                │                         │  • Worker chi nhánh 🟢      │
                │                         │  • Signer chi nhánh 🟡      │
                │                         │  • Ban giảng viên AI20K 🟢   │
                │                         │  • (Đèn đỏ nếu 30' không duyệt│
                │                         │    → Manager xử lý)         │
                └─────────────────────────┴─────────────────────────────┘
```

> **Ghi chú quan trọng:** Stance thực tế **không** luôn trùng nhãn quadrant.
> - **Luật sư tư vấn Gcar** nằm vùng Champion (Influence cao + Interest cao) nhưng stance thực tế là 🔴 **chưa ủng hộ** vì chưa ký hợp đồng tư vấn → team cần chuyển sang ủng hộ bằng cách ký hợp đồng trước.
> - **Kế toán Gcar** nằm Champion nhưng stance 🟡 **trung lập** vì merchant sandbox chưa đăng ký → cản trở VNPay integration.
> - **Reviewer chi nhánh** stance 🟢 ủng hộ → nhưng chỉ 1 reviewer/chi nhánh, nếu nghỉ → pipeline tắc.

---

## 4. Team — 4 stakeholder ưu tiên & chiến lược

### 4.1. Hai stakeholder đang ủng hộ mạnh — **TẬN DỤNG**

#### 🌟 **Founder / Admin Gcar** (Product Owner)
- **Quan tâm điều gì:** Tốc độ rollout thật (chi nhánh HN-01 → HCM-01 trong Q4/2026), tuân thủ pháp lý, không có scandal hợp đồng
- **Có thể giúp:** Duyệt scope nhanh, giới thiệu với Luật sư tư vấn Gcar, kết nối với kế toán Gcar để mở merchant sandbox
- **Cản trở nếu:** Mất kiên nhẫn nếu demo chậm → scope creep
- **Hành động 1-2 tuần tới:**
  - Thái Anh gửi ADR 0011 + 0012 kèm prototype demo bản đồ chi nhánh Leaflet + 6-role login UI trước **thứ Sáu tuần này**
  - Trung setup 30' demo online với Admin để xin quyết định "có tiếp tục tháng tới hay không"

#### 🌟 **Reviewer chi nhánh HN-01**
- **Quan tâm điều gì:** Duyệt nhanh, ít phải sửa hồ sơ, có audit log để bảo vệ mình khi có khiếu nại
- **Có thể giúp:** Test thật flow duyệt + ký hợp đồng, phát hiện edge case (thiếu GPLX, KYC fail, payment timeout)
- **Cản trở nếu:** 30 phút không duyệt → Manager highlight → nếu xảy ra thường xuyên → người dùng bỏ Gcar
- **Hành động 1-2 tuần tới:**
  - Thái Anh viết walkthrough 1 trang A4 cho Reviewer về 6 trạng thái mới (pending_review → approved → contract_ready → payment_pending → customer_signed → signed) — deadline **Day 7**
  - Trung book 1 buổi shadow 2h tại HN-01 với Reviewer thật — deadline **Day 10**

### 4.2. Hai stakeholder chưa ủng hộ / có rủi ro cản trở — **ƯU TIÊN THUYẾT PHỤC**

#### ⚠️ **Luật sư tư vấn Gcar** (chưa ký HĐ)
- **Quan tâm điều gì:** Phí tư vấn, hợp đồng có rủi ro pháp lý không, có case thực tế để review không
- **Có thể cản trở:** Từ chối ký hợp đồng (đặc biệt CL-17 chính sách hủy chuyến — đang để trống vì mẫu HĐCTXTL không quy định), kéo dài thời gian launch 4-6 tuần
- **Hành động 1-2 tuần tới:**
  - Trung chuẩn bị **Legal review checklist** (1 file Markdown): 12 điểm cần review (Điều 1-7, Phụ lục 1 bàn giao, Phụ lục 2 bảng giá, CL-17, quyền xử lý dữ liệu cá nhân) — deadline **Day 5**
  - Thái Anh ping Admin Gcar qua Slack/Telegram xin intro luật sư — deadline **Day 3**

#### ⚠️ **VNPay support** (chậm verify IPN → cản trở thanh toán online)
- **Quan tâm điều gì:** Hợp đồng merchant đầy đủ, IPN URL public & stable, không spam test
- **Có thể cản trở:** Chậm cấp TMN code + hash secret (thường 5-7 ngày làm việc), reject nếu IPN URL chưa ổn định
- **Hành động 1-2 tuần tới:**
  - Thái Anh viết template email đăng ký merchant sandbox VNPay, gửi cho Kế toán Gcar ký & gửi — deadline **Day 4**
  - Trung deploy IPN endpoint `https://gcar-p030.vercel.app/api/v1/payments/vnpay/ipn` lên Vercel production với health check log — deadline **Day 7**

---

## 5. Gate 1 Checklist

| Tiêu chí | Đạt? |
|---|---|
| ≥ 6 stakeholder **cụ thể** (có tên/nhóm + bối cảnh) — không viết "khách hàng" chung | ✅ 10 stakeholder |
| Map theo Influence × Interest rõ ràng | ✅ 10/10 |
| Stance (mức độ ủng hộ) thực tế của từng stakeholder | ✅ Đánh dấu 🟢🟡🔴 cho cả 10 |
| 4 hành động cụ thể cho 4 stakeholder ưu tiên (2 ủng hộ + 2 cản trở) | ✅ Founder/Admin + Luật sư + Reviewer + VNPay |
| Mỗi hành động có owner + deadline cụ thể | ✅ 4/4 |

---

## 6. Phụ lục — 6 stakeholder còn lại (chưa ưu tiên hành động tuần này)

| Stakeholder | Lý do chưa ưu tiên |
|---|---|
| Manager khu vực | Phụ thuộc Admin Gcar — sẽ thảo luận sau khi Admin duyệt ADR 0011 |
| Khách cá nhân/doanh nghiệp | Hành động qua UI/UX (Phase 3 — AI Team Design) |
| Worker/Signer tại chi nhánh | Hành động qua UI/UX (Phase 3 — AI Team Design) |
| Kế toán Gcar | Phụ thuộc Admin Gcar — chờ merchant sandbox |
| Sở GTVT HN/HCM | Theo dõi qua newsletter — không có hành động tức thì |
| Ban giảng viên AI20K | Theo dõi qua feedback tổng duyệt G5 |
| Đối tác bảo hiểm | Hành động qua config gói bảo hiểm (LMS-024 tuần 3-4) |