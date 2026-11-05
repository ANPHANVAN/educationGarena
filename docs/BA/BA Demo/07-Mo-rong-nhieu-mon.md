# 07 — Mở rộng nhiều môn & nhượng quyền sau này

Câu hỏi: *“Làm Toán trước, sau có mở Lý/Hóa/Anh được không?”*  
**Trả lời ngắn: Có**, nếu từ đầu **không nhét Toán vào code cứng**, mà tách **engine khảo thí** khỏi **gói nội dung môn**.

---

## 1. Phần dùng chung mọi môn (platform)

- User, org, thanh toán, kỳ thi, [attempt](./11-Chu-thich.md#attempt), timer, palette UI shell  
- [Blueprint](./11-Chu-thich.md#ma-tran) engine ([ô](./11-Chu-thich.md#o-ma-tran) filter + count + [sinh đề](./11-Chu-thich.md#sinh-de) + shortage report)  
- Vòng đời câu hỏi (draft → approved)  
- [Score policy](./11-Chu-thich.md#score-policy) **cấu hình được** (không hard-code 0,25 / 0,5)  
- [CBT](./11-Chu-thich.md#cbt) layout: 1 cột / 2 cột ([stimulus](./11-Chu-thich.md#stimulus) | questions)

Đây là thứ team xây một lần.

---

## 2. Phần riêng từng môn (content pack)

Mỗi môn = pack cấu hình + [bank](./11-Chu-thich.md#ngan-hang-cau-hoi):

| Thành phần | Toán | Lý / Hóa | Tiếng Anh |
|------------|------|----------|-----------|
| Topic tree | Chuyên đề ĐS–HH–XS | Chuyên đề chương | Skill + theme |
| [Item formats](./11-Chu-thich.md#dang-thuc) dùng | [MCQ](./11-Chu-thich.md#mcq), [Đ/S](./11-Chu-thich.md#dung-sai), [Short](./11-Chu-thich.md#tra-loi-ngan) | Tương tự TN THPT | Chủ yếu MCQ (+ điền từ sau) |
| Score policies | Template TN Toán | Template môn đó | 40 câu × điểm/câu |
| Render đặc thù | LaTeX nặng, hình HH | Công thức + hình thí nghiệm | Audio (sau) |
| Short answer rules | Số / làm tròn | Số + đơn vị? | Từ vựng |

**Nhượng quyền môn** ≈ giao pack + quy trình duyệt nội dung + (optional) brand riêng trên cùng platform.

---

## 3. Việc phải làm đúng từ MVP Toán (để khỏi đập đi)

1. `subject_id` trên mọi Question, Blueprint, Exam.  
2. `ItemFormat` và `ScorePolicy` là dữ liệu/config, không `if (math) return 0.5`.  
3. [Topic](./11-Chu-thich.md#chu-de) là bảng dữ liệu, không enum hard-code trong source.  
4. TRUE_FALSE_GROUP và SHORT_ANSWER là first-class (Lý/Hóa TN THPT cũng dùng).  
5. Tránh tên bảng kiểu `math_questions` — dùng `questions`.

---

## 4. Khác biệt môn sẽ đau nếu chủ quan

| Vấn đề | Cách xử lý |
|--------|------------|
| Ngữ văn tự luận | Format ESSAY + chấm tay; không nhét vào auto-grade |
| Ngoại ngữ chỉ MCQ (đề TN) | Template 1 phần; không bắt buộc đủ 3 dạng |
| Nghe / nói | Media pipeline — P2+ |
| Vào 10 tự luận theo Sở | Blueprint khác + PDF export |

Platform không cần hỗ trợ hết ngày đầu; chỉ **đừng chặn** bằng thiết kế hẹp.

---

## 5. Điều kiện mở môn thứ 2

Chỉ nên mở khi:

1. Toán có doanh thu hoặc cohort trung tâm trả phí ổn định.  
2. Có **chủ trì nội dung** môn mới (giáo viên/partner) — 2 dev không tự viết bank Lý.  
3. Tái dùng ≥70% code delivery/blueprint; effort chủ yếu là nội dung + template scoring.

---

## 6. Kết luận cho founder

- **Có mở rộng được.**  
- Mở rộng = nhân bản **content + template**, không phải viết lại hệ thống thi.  
- Vốn hạn chế → độc quyền thời gian cho Toán đến khi matrix + bank + CBT ổn.
