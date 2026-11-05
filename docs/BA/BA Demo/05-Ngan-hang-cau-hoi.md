# 05 — Quản lý ngân hàng câu hỏi

Ngân hàng tốt = ma trận mới có cái để bốc. Với team nhỏ, **quy trình nội dung** quan trọng không kém schema.

---

## 1. Nguyên tắc thiết kế

1. **Câu hỏi không tồn tại nếu thiếu metadata bắt buộc** (chặn publish).  
2. **Tách nội dung hiển thị** (stem, choices, media) khỏi **metadata phân loại** (topic, level, format).  
3. **Một lần duyệt** trước khi vào đề thi có tính “chính thức”.  
4. **Snapshot khi vào ExamVersion** — sửa bank không làm đổi đề đã thi.  
5. Schema **agnostic môn** — Toán chỉ là bộ Topic + Format config.

---

## 2. Metadata bắt buộc (MVP)

| Trường | Bắt buộc | Ghi chú |
|--------|----------|---------|
| subject_id | ✓ | |
| grade_levels[] | ✓ | Một câu có thể ôn cho nhiều lớp (vd. hàm số 11–12) |
| topic_ids[] | ✓ ≥1 | Chủ đề chính; phụ để tag |
| cognitive_level | ✓ | NB/TH/VD/VDC — **trên câu** (Đ/S: 1 mức cho cả group). Báo cáo 3 mức: VDC→VD |
| item_format | ✓ | |
| status | ✓ | draft / in_review / approved / rejected / archived |
| ownership_layer | ✓ | personal / center / system / secret / … (bảng động) |
| created_by | ✓ | Nguồn gốc tác giả — luôn lưu để tham chiếu |
| organization_id | optional | Nếu thuộc trung tâm |
| stem (nội dung) | ✓ | Text + LaTeX |
| answer key | ✓ | Theo format |
| default_score | optional | Thường lấy từ blueprint cell |
| estimated_time_sec | optional | |
| competency | optional | |
| difficulty_manual | optional | 1–5 nếu muốn ngoài 4 mức CĐT |
| language | ✓ | vi |

---

## 3. Mô hình theo từng dạng thức

### 3.1. MCQ một đáp án đúng

```
Question
  stem
  choices[4]: {label, content, is_correct}
  explanation
```

Ràng buộc: đúng đúng 1 choice.  
(Đa đáp án đúng để sau — ít dùng trong đề TN Toán hiện tại.)

### 3.2. Đúng / Sai (group) — mức theo cả câu (đã chốt lại)

```
Question (format=TRUE_FALSE_GROUP)
  cognitive_level: NB|TH|VD|VDC   // BẮT BUỘC — 1 mức cho cả câu
  topic_ids[]
  stimulus? / stem_chung
  ideas[4]:                      // cố định 4 ý; không có level riêng
    stem_idea
    correct: true|false
    explanation?
```

UI thí sinh: 4 ý, mỗi ý Đ/S.  
Chấm điểm theo số ý đúng trong câu (policy TN: 0,1/0,25/0,5/1).  
Ma trận / tồn kho / đặc tả / bốc câu: theo **câu** (giống MCQ).

### 3.3. Trả lời ngắn — chấm nghiêm (đã chốt)

```
Question
  stem   // PHẢI chứa quy ước làm tròn / đơn vị nếu cần
         // vd. "Kết quả làm tròn đến hàng phần trăm"
  accepted_answers[]: {value_normalized, aliases[]}  // alias = tương đương tuyệt đối do GV khai
  answer_type: number | string | expression
  // KHÔNG dùng tolerance trong mode thi
```

**Chấm:** normalize (trim, dấu thập phân) rồi **exact match** với key. Sai khác biệt làm tròn → 0 điểm.  
Giống kỷ luật đáp án thi ĐH/TN: đề đã nói cách làm tròn thì chỉ đáp án đúng quy ước mới được tính.

### 3.4. Tự luận (P2)

Chỉ lưu stem + rubric + điểm tối đa; chấm tay. Không nằm MVP CBT auto-grade.

### 3.5. Stimulus dùng chung

Một hình / bảng / đoạn cho nhiều câu (Passages kiểu demo Bộ môn đọc hiểu; Toán: bài thực tế nhiều ý).

---

## 4. Vòng đời câu hỏi

```
draft → in_review → approved ⇄ archived
                 ↘ rejected → draft
```

| Status | Bank personal/center (đề của GV) | Bank **system** |
|--------|----------------------------------|------------------|
| draft | Author dùng / preview | Không |
| in_review | — | Chờ ContentAdmin duyệt stem + đáp án |
| approved | Dùng được | Vào kho chung hệ thống |
| rejected | Sửa lại | Không vào system |
| archived | Không bốc đề mới | Giữ qua snapshot đề cũ |

Checklist duyệt (người duyệt hệ thống): đúng đáp án, LaTeX render, mức độ/topic đúng, không trùng stem, hình rõ.  
Câu personal **không bắt buộc** duyệt hệ thống để GV tự tạo đề; chỉ câu muốn vào kho chung mới bắt buộc duyệt.

---

## 5. Chiến lược nhập liệu (khớp vốn hạn chế)

| Cách | Chi phí | Chất lượng | Ưu tiên |
|------|---------|------------|---------|
| Form web + editor LaTeX | Thấp | Cao nếu GV nhập | **P0** |
| Copy/paste theo template Word/Markdown có delimiter | Thấp | Trung bình | P0.5 |
| Import Excel metadata + nội dung đơn giản | Thấp | Trung bình | P1 |
| User dán API key → AI parse PDF/Word | User trả AI | Không ổn định | P2 |
| AI sinh câu mới | Rủi ro sai / bản quyền | Cần duyệt chặt | P2+ |

**Tháng đầu:** giáo viên partner nhập tay / bán cấu trúc theo template. Đừng block MVP vì “AI đọc PDF”.

Gợi ý template text:

```
## Q1
FORMAT: MCQ
TOPIC: Khao_sat_ham_so
LEVEL: TH
STEM: ...
A. ...
B. ...
C. ...
D. ...
ANSWER: B
SOLUTION: ...
```

---

## 6. Chống trùng & chất lượng bank

MVP:

- Search full-text stem.  
- Cảnh báo trùng khi tạo (similarity đơn giản / exact normalize).  

Sau:

- Thống kê tỷ lệ đúng sau N lượt làm → gợi ý chỉnh `cognitive_level`.  
- Flag câu quá dễ/quá khó so với nhãn.

**Tồn kho tối thiểu để ma trận TN THPT có ý nghĩa:**  
Rough: mỗi ô chủ đề × mức × format nên có **≥ 5–10 câu** trước khi bán “sinh đề không trùng”.  
Ước lượng bank khởi động: **300–800 câu Toán** đã duyệt (tùy độ phủ chủ đề) — cần giáo viên ước lượng thực tế.

---

## 7. Media & công thức

- Lưu LaTeX trong DB; render KaTeX/MathJax phía client.  
- Ảnh: object storage; giới hạn dung lượng.  
- Không nhúng base64 lung tung trong DB nếu tránh được.

---

## 8. Phân quyền nội dung

| Hành động | Teacher (tenant) | ContentAdmin | Student |
|-----------|------------------|--------------|---------|
| Tạo câu bank riêng | ✓ | ✓ | ✗ |
| Sửa câu người khác (bank chung) | ✗ | ✓ | ✗ |
| Duyệt approved | ✗ / theo config | ✓ | ✗ |
| Xem đáp án khi làm bài thi | ✗ | ✓ | Sau nộp / tùy mode |
| Export bank | ✓ (của mình) | ✓ | ✗ |

---

## 9. Chỉ số vận hành bank (dashboard đơn giản)

- Số câu theo (topic × level × format × status).  
- Ô ma trận template chuẩn: xanh đủ / đỏ thiếu.  
- Top câu bị report sai đáp án.

Không có dashboard này, giáo viên không tin “bốc theo ma trận”.
