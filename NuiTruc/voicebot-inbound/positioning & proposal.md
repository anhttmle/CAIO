# 1. Executive Summary
- **Vấn đề**: "Phòng khám răng" mất khách vì
  - missed calls.
  - lễ tân quá tải.
  - nhắc hẹn thủ công.
  - bệnh nhân không được phục vụ nhanh.
  - hậu chăm sóc (post-op care) và follow-up bệnh nhân chưa đủ tốt.
  - nhân sự mới còn nhiều bỡ ngỡ khi chăm sóc khách hàng.
- **Giải pháp**:
  - Dental Voice AI Platform (long-term)
  - freemium web/Zalo assistant (freemium)
  - paid voice phone + scheduling/reminders (premium)
  - xây dựng app/knowledge base multi‑clinic
  - mức độ automation “khuyến nghị”:
    - Human with AI support
    - hybrid AI + human (trong giờ sử dụng human, ngoài giờ sử dụng AI)
- **Lợi ích chính**:
  - giảm missed calls (scale)
  - giảm no‑show (scale)
  - giảm giờ lễ tân (tối ưu chi phí)
  - cải thiện trải nghiệm bệnh nhân. (scale)
  - kết nối clinic & khách hàng
- **Chiến lược go‑to‑market**: (với tình trạng cạnh tranh và công nghệ phổ biến, cần đi đường dài với từng baby step)
  - **service‑led**: triển khai cho vài clinic/agency tiềm năng, tập trung vào hỗ trợ xây dựng giải pháp và xây dựng lòng tin với họ.
  - **freemium**: để giảm rào cản chi phí và thử nghiệm chất lượng đối với những clinic lo ngại về chi phí và ảnh hướng tới khách hàng hiện tại.
 
# 2. Problem & Context (Mô tả vấn đề theo framework 4U)
- **Unworkable**: missed calls, no‑show, manual reminders, PMS rời rạc → quy trình front‑desk “gãy”, mất doanh thu.
- **Unavoidable**: mọi phòng khám đều phải nhận cuộc gọi, đặt lịch, nhắc hẹn; không làm thì mất khách.
- **Urgent**: với clinic đang quá tải, đây là top pain ngắn hạn (lễ tân burnout, bệnh nhân phàn nàn).
- **Underserved**: vertical “nha khoa + Việt/ASEAN + PMS nội địa + voice AI” chưa được phục vụ đúng mức; hiện chủ yếu là chatbot/omnichannel generic.

> Context này đúng và sai tuỳ thuộc vào trạng thái của từng phòng khám: quy mô lớn hay nhỏ?, đã chuyển đổi số hay chưa?, đang ưu tiên scale hay tối ưu chi phí?, khách hàng nhỏ lẻ hay doanh nghiệp/tổ chức?

# 3. Competitive Landscape & Positioning
### Global:
- Dental‑native platforms (Arini, Dentina, TensorLinks, Viva…)
- omnichannel (AnveVoice, CloudTalk, Weave).

### Việt Nam:
- Chatbot/omnichannel cho nha khoa (ChatPilot, Preny, Addy, ChatbotViet, AI CRM…)
- voice/auto bot đa ngành (BussCall, Sokucom).

### Positioning:
- Dental Voice AI vertical cho Việt Nam/ASEAN:
  - Việt hóa sâu (giọng, ngôn ngữ, kịch bản).
  - Pack model + hybrid automation.
  - PMS & kênh nội địa, privacy‑first health data.
 
# 4. Risks & Mitigation
### Rủi ro:
- SMB SaaS tarpit (ACV thấp, sales cycle dài).
- Voice quality/telephony VN, PMS integration phức tạp.
- Patient satisfaction & trust, privacy/data monetization.

### Cách giảm:
- Service‑led triển khai, rất chọn lọc clinic/agency pilot.
- Phased rollout & hybrid AI+human, automation recommended (~60–70%).
- Privacy‑by‑design, không gắn freemium với bán data, mọi program thương mại trên data là opt‑in.

# 5. Solution Overview (theo framework 3D)
- **Disruptive** (biz model thay đổi luật chơi):
  - đang ở mức “mildly disruptive”: pack + freemium localized + service‑led overlay là khác đối thủ hiện tại
  - cốt lõi vẫn là subscription + minutes (mô hình thuê bao).
- **Discontinuous** (làm được thứ trước đây gần như không thể hoặc cực kỳ khó):
  - đang ride trên một discontinuous wave global (voice AI healthcare), và localized cho VN/ASEAN => không chỉ chúng ta.
  - ở thị trường nội địa, nếu execute tốt, có thể coi là discontinuous cho clinic nhỏ – nhưng không phải breakthrough toàn ngành.
  - **Bổ sung**: AI coach cho newbie lễ tân + smart fallback cho nhân sự cấp cao hơn hoặc chuyên gia.
- **Defensible** (moats quanh biz model):
  - domain data, integration, privacy nếu có client/user
  - Integration (nhiều competitor cũng có)
  - Workflow & UX moat (nhiều competitor cũng có)
  - Compliance & trust moat (???)
  - **Bổ sung**: Xây dựng user app/knowledge base multi‑clinic => có thể thiết kế “matchmaking” giữa bệnh nhân và clinic; nhiều clinic → nhiều lựa chọn cho bệnh nhân, nhiều bệnh nhân → clinic càng muốn vào network.
 
# 6. Product Description
### 6.1 Tổng quan
<details>
<summary>Chi tiết</summary>
Sản phẩm là một Dental Voice AI Platform dành cho phòng khám răng tại Việt Nam/ASEAN, giúp tự động hóa các giao tiếp front‑desk bằng giọng nói và đa kênh (website, Zalo, SMS) mà không yêu cầu phòng khám phải thay đổi PMS, CRM hay hệ thống hiện có.

Nền tảng cung cấp một “lễ tân AI” hoạt động 24/7, có thể:
- Nhận và xử lý cuộc gọi từ bệnh nhân.
- Tra cứu dịch vụ và chi phí tham khảo.
- Đặt, sửa, hủy lịch hẹn.
- Nhắc hẹn và tái khám tự động.
- Hỗ trợ đào tạo lễ tân mới.
- Chuyển tiếp thông minh tới nhân sự cấp cao (CS senior, y tá, bác sĩ) khi cần.
Thiết kế sản phẩm theo triết lý hybrid AI + người thật, với mức độ tự động hóa “khuyến nghị” (AI xử lý routine, người thật xử lý ca khó) để bảo toàn trải nghiệm bệnh nhân và danh tiếng phòng khám.
</details>

### 6.2 Các thành phần chính
#### a. Voice AI cho hotline phòng khám (gói trả phí)
<details>
<summary>Chi tiết</summary>
- **Chức năng cốt lõi**:
  - Nhận và xử lý cuộc gọi 24/7 <br>
  AI tiếp nhận cuộc gọi vào số điện thoại của phòng khám, chào hỏi theo thương hiệu, hiểu nhu cầu (đặt lịch, đổi lịch, hủy, hỏi dịch vụ, hỏi khẩn cấp) và dẫn dắt cuộc hội thoại một cách tự nhiên.
  - **Đặt, sửa, hủy lịch hẹn tự động** <br>
  Kết nối với hệ thống lịch/PMS (hoặc Google Calendar) để:
    - Kiểm tra slot trống theo dịch vụ, bác sĩ, chi nhánh.
    - Đề xuất khung giờ phù hợp.
    - Tạo mới, sửa đổi, hủy lịch hẹn trực tiếp trong hệ thống của phòng khám.
  - **Nhắc hẹn & recall bệnh nhân cũ** <br>
  Gọi và/hoặc gửi SMS/Zalo để:
    - Nhắc bệnh nhân trước ngày khám (confirm, đổi lịch, hủy).
    - Nhắc tái khám định kỳ: cạo vôi răng, kiểm tra niềng, follow‑up implant…
    - Gửi link bản đồ, hướng dẫn trước khi khám, phiếu đánh giá sau khám.
  - **Chuyển tiếp (handover) sang lễ tân hoặc bác sĩ** <br>
    Khi cuộc gọi vượt ngoài phạm vi AI (ca khẩn, câu hỏi phác đồ điều trị, khiếu nại, vấn đề nhạy cảm), hệ thống chuyển tiếp sang lễ tân/y tá/bác sĩ trực, kèm theo:
      - Tóm tắt nội dung hội thoại.
      - Thông tin bệnh nhân đã thu thập.
      - Intent và thao tác đã thực hiện. <br>
        Giúp người thật tiếp nhận nhanh, không phải hỏi lại từ đầu.

  - **Mức độ tự động hóa “khuyến nghị”** <br>
    Mặc định, AI xử lý khoảng 60–70% cuộc gọi routine (đặt lịch, đổi lịch, nhắc hẹn, FAQ đơn giản), phần còn lại (~30–40%) được chuyển sang người thật theo rule và tín hiệu AI → giảm rủi ro ảnh hưởng tới patient satisfaction.
</details>

#### b. Web/Zalo Assistant (freemium)

<details>
<summary>Chi tiết</summary>
Đây là tầng freemium/low‑risk, giúp phòng khám có thể thử AI mà gần như không phải đầu tư chi phí đầu tiên.

**Chức năng**:

- **Tra cứu dịch vụ & chi phí tham khảo** <br>
  Bệnh nhân có thể chat/voice với assistant trên website hoặc Zalo OA của phòng khám để hỏi:
  - Các loại dịch vụ (niềng, implant, trám, tẩy trắng…).
  - Chi phí tham khảo cho từng dịch vụ/gói.
  - Thời gian thực hiện, quy trình cơ bản, lưu ý trước/sau điều trị.
- **FAQ nâng cao** <br>
  Assistant được huấn luyện trên knowledge base của từng phòng khám (giờ mở cửa, địa chỉ chi nhánh, bác sĩ, chính sách bảo hành, cách thanh toán…) để trả lời câu hỏi nhanh, nhất quán và thân thiện.
- **Hỗ trợ flow đặt lịch trên web** <br>
  Assistant có thể dẫn dắt bệnh nhân đi qua form đặt lịch trực tuyến (họ tên, số điện thoại, dịch vụ, chi nhánh, khung giờ), giúp giảm bỏ dở trong quá trình tự đặt lịch trên website.
 <br>
Freemium tier này giải bài toán: clinic lo chi phí và chất lượng AI, có thể “thử cảm giác” mà chưa phải để AI xử lý hotline thật.
</details>

#### c. Dashboard & Portal cho phòng khám

<details>
<summary>Chi tiết</summary>
**Dashboard vận hành**:
  - Thống kê theo ngày/tuần/tháng:
    - Số cuộc gọi AI xử lý, số cuộc gọi chuyển tiếp.
    - Số lịch hẹn được đặt/đổi/hủy qua AI.
    - Tỷ lệ no‑show trước/sau khi bật nhắc hẹn.
    - Các intent phổ biến (booking, cancel, FAQ, khẩn cấp…).

**Clinic profile & cấu hình flow**:
- Khai báo: giờ làm việc, loại dịch vụ, thời lượng slot, chi nhánh, bác sĩ, quy tắc phân công.
- Cấu hình:
  - Ngưỡng automation (bao nhiêu % cuộc gọi AI xử lý).
  - Rule khẩn cấp (triệu chứng nào phải chuyển bác sĩ trực).
  - Tone và giọng nói của lễ tân AI (trẻ trung, nghiêm túc, thân thiện…).
**Quản lý pack/tính năng**:
- Bật/tắt từng pack:
  - Appointment, Reminders, Upsale, PMS Integration.
- Xem hiệu quả từng pack (booking tăng, no‑show giảm, recall hiệu quả…) để quyết định tiếp tục, mở rộng hoặc thu hẹp.
</details>
### 6.3. Hỗ trợ nhân sự & fallback an toàn
#### a. AI coach cho lễ tân newbie
<details>
<summary>Chi tiết</summary>
Mục tiêu: giúp nhân sự mới (lễ tân mới tuyển, CS mới) tự tin xử lý cuộc gọi từ sớm, giảm lỗi đặt lịch, tăng chất lượng tư vấn.

**Chức năng**:
- **Shadow mode & gợi ý trong lúc gọi** <br>
  Khi lễ tân mới đang nói chuyện với bệnh nhân, hệ thống AI chạy song song, hiển thị:
    - Câu hỏi gợi ý tiếp theo (dịch vụ, triệu chứng, bác sĩ ưu tiên).
    - Slot lịch phù hợp để offer.
    - Thông tin/FAQ liên quan để giải thích cho bệnh nhân.
- **Flow helper theo kịch bản chuẩn** <br>
  UI gợi ý từng bước theo script của phòng khám (VD: bước 1 hỏi thông tin cơ bản, bước 2 hỏi lý do khám, bước 3 chọn dịch vụ…). Giúp người mới không bỏ sót trường quan trọng và bám đúng quy trình.
- **Validation dữ liệu theo thời gian thực** <br>
  AI kiểm tra dữ liệu lễ tân nhập (ngày giờ, dịch vụ, chi nhánh, bác sĩ) để tránh double‑booking hoặc đặt sai dịch vụ; nếu phát hiện bất thường, hệ thống cảnh báo ngay trên màn hình.
- **Training & review sau ca trực** <br>
  Dashboard cung cấp:
    - Danh sách cuộc gọi do lễ tân mới xử lý.
    - Highlight lỗi thường gặp và đề xuất cải thiện.
    - Transcript đi kèm nhận xét AI (những chỗ nên hỏi sâu hơn, chỗ trả lời chưa rõ).
</details>

#### b. Smart fallback tới nhân sự cấp cao

<details>
<summary>Chi tiết</summary>
Mục tiêu: bảo đảm mọi ca phức tạp hoặc nhạy cảm đều được xử lý bởi người phù hợp (CS lâu năm, y tá, bác sĩ), không để AI hoặc người mới tự “xoay” một mình.
**Chức năng**:
  - **Rule‑based & AI‑based escalation**
    - Rule cứng:
      - Ca khẩn (đau dữ dội, chảy máu nhiều, tai nạn…) → chuyển bác sĩ trực.
      - Câu hỏi về phác đồ điều trị → chuyển bác sĩ.
      - Khiếu nại/góp ý → chuyển CS senior hoặc quản lý.
    - AI bổ sung: phát hiện tín hiệu căng thẳng/khó chịu trong giọng nói/nội dung, gợi ý chuyển người thật dù chưa match rule.
  - **Tiered routing (đa tầng)**
    - Lễ tân newbie có thể bấm “Cần hỗ trợ” để mời senior join call hoặc chuyển thẳng cuộc gọi.
    - AI đang xử lý call có thể chuyển tiếp sang lễ tân senior, y tá, bác sĩ tùy intent.
  - **Transfer giàu ngữ cảnh** <br>
    Khi chuyển, hệ thống gửi:
      - Tóm tắt hội thoại.
      - Thông tin bệnh nhân (nếu đã xác minh).
      - Intent chính và các bước đã thực hiện. <br>
        Giúp người nhận call hiểu nhanh vấn đề mà không làm bệnh nhân lặp lại quá nhiều.
  - **Escalation dashboard & tối ưu staffing** <br>
    Phòng khám có thể xem:
      - Tần suất và loại case bị chuyển tiếp.
      - Nhóm nhân sự nhận nhiều escalation nhất.
      - Thời gian xử lý trung bình và kết quả. <br>
        Từ đó điều chỉnh rule, tăng/giảm ca trực, phân công nhân sự cho giờ cao điểm.
</details>

### 6.4 Kiến trúc kỹ thuật & tích hợp
Ở mức high‑level, sản phẩm gồm:
- CoreAI / Voice Agent Engine
  - Pipeline STT/TTS/LLM xử lý giọng nói tiếng Việt (và ngôn ngữ khác nếu cần).
  - Workflow engine quản lý kịch bản hội thoại và logic pack.
- Dental Domain Backend
  - Service cho lịch hẹn (appointment), nhắc hẹn (reminders), upsale/recall, FAQ, triage cơ bản.
- Integration Layer
  - Adapter tới PMS/CRM nội địa hoặc Google Calendar.
  - Adapter tới telephony nội địa (SIP, tổng đài ảo) và kênh SMS/Zalo.
- Dashboard & Portal
  - Web UI cho clinic owner/manager cấu hình, theo dõi, phân tích.

## 6.5 Packs:
<details>
<summary>Chi tiết</summary>
  
- Base (Freemium) Pack:
  - Web/Zalo assistant: FAQ về dịch vụ, chi phí tham khảo, quy trình, giờ mở cửa, địa chỉ.
  - Triaging cơ bản (phân loại câu hỏi, không triage lâm sàng).
  - Shadow mode for evaluate newbie
  - Recommend mode for support newbie
  - Một số phút thử trên số test (optional).

- Paid Packs:
  - Appointment Pack: đặt/sửa/hủy lịch qua voice phone, sync với PMS/Calendar.
  - Reminders Pack: nhắc hẹn và recall tự động qua phone + SMS/Zalo, follow‑up sau điều trị.
  - Upsale/Recall Advanced Pack: chiến dịch tái kích hoạt bệnh nhân cũ (cạo vôi định kỳ, niềng, implant) với consent rõ.
  - PMS Integration Pack: deep integration với PMS nội địa / Google Calendar (read‑write)

</details>

## 6.6 Data & Privacy
<details>
<summary>Chi tiết</summary>
  
- Nguyên tắc:
  - Health data/bệnh nhân thuộc clinic/bệnh nhân; hệ thống là processor/platform.
  - Dùng dữ liệu de‑identified cho model improvement & analytics; mọi chương trình merchant/marketplace là opt‑in riêng biệt với consent rõ.
- Thiết kế:
  - Encryption, role‑based access, audit logs, phân tách PII vs analytics.
  - Documentation về data retention, quyền xoá, và governance.

</details>

# 7. Go-to-market Strategy
<details>
<summary>Chi tiết</summary>
  
### 7.1 Target Segment
- Clinic nha khoa tư nhân 2–5 ghế (số lượng khách có thể serve cùng lúc tối đa) ở Hà Nội/Tp.HCM đang:
  - Missed calls cao.
  - Lễ tân quá tải.
  - Chưa có automation nhắc hẹn.

### 7.2 Freemium / Trial
- Cung cấp:
  - Web/Zalo assistant + FAQ/triage miễn phí, kịch bản Việt hóa với brand của clinic.
  - Hoặc short trial gói voice appointment/reminders trên số test, với quota phút gọi rõ.
- Mục tiêu freemium:
  - Giảm rào cản chi phí.
  - Cho clinic trải nghiệm chất lượng AI (giọng, logic, UX).
  - Thu feedback để refine domain.

### 7.3 Monetization & Pricing Sketch
- Paid revenue từ:
  - Gói deployment/implementation cụ thể cho mỗi clinic/agency (setup + kịch bản + integration).
  - Subscription cho pack voice appointment/reminders (per clinic/per minute hybrid).
  - Commission from matching Clinic & khách (Clinic có thêm khách, khách được chiết khấu, Nuitruc được hoa hồng)
</details>
