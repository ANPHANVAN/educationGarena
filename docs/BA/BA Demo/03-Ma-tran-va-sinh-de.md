# 03 — Ma trận đề thi & logic “bốc câu” / sinh đề

Đây là **trái tim nghiệp vụ** của core. Nếu phần này sai, ngân hàng câu hỏi chỉ là kho dump.

---

## 1. Ma trận là gì (trong ngữ cảnh sản phẩm)

**Ma trận đề** = bảng quy tắc phân bổ câu hỏi cho một đề / một phiên sinh đề.

Mỗi ô ma trận trả lời: *“Lấy bao nhiêu câu thỏa điều kiện X?”*

Điều kiện X tối thiểu (MVP):

- `subject` = Toán  
- `grade` hoặc `topic` (chủ đề / dạng bài)  
- `cognitive_level` ∈ {NB, TH, VD, VDC}  
- `item_format` ∈ {MCQ_SINGLE, TRUE_FALSE_GROUP, SHORT_ANSWER, …}  
- (optional) `competency`, `chapter`, tags

**Sinh đề** = với mỗi ô, lấy ngẫu nhiên (hoặc theo trọng số) đủ số câu từ ngân hàng **còn đủ tồn kho**, rồi ghép thành một **ExamVersion** (đề cụ thể / mã đề).

```
Ma trận (Blueprint)
        │
        ▼
  Với mỗi ô: query QuestionBank
        │
        ▼
  Chọn N câu thỏa filter + ràng buộc toàn cục
        │
        ▼
  ExamVersion (danh sách câu đã khóa thứ tự/điểm)
        │
        ▼
  Gắn vào Session thi / Luyện tập
```

---

## 2. Hai cách user tạo ma trận

### A. Dùng template có sẵn (nên làm trước)

Ví dụ template `TN_THPT_TOAN_2025` đã khai báo sẵn các ô:

| Phần | Format | Số đơn vị | Gợi ý mức | Điểm rule |
|------|--------|-----------|-----------|-----------|
| I | MCQ_SINGLE | 12 câu | NB–TH | 0,25/câu |
| II | TRUE_FALSE_GROUP | 4 nhóm × 4 ý | TH–VD | bảng 0,1/0,25/0,5/1 |
| III | SHORT_ANSWER | 6 câu | VD–VDC | 0,5/câu |

User có thể:

- Giữ nguyên số lượng phần, chỉ chỉnh **phân bổ chủ đề** (ô con), hoặc  
- Chỉ nhấn “Sinh đề chuẩn TN” → hệ thống dùng phân bổ mặc định (cấu hình bởi giáo viên).

### B. Ma trận tự do (giáo viên / luyện tập)

UI kiểu bảng:

| Chủ đề \ Mức | NB | TH | VD | VDC |
|--------------|----|----|----|-----|
| Khảo sát hàm số | 2 | 2 | 1 | 0 |
| Tích phân | 1 | 1 | 1 | 1 |
| … | | | | |

User nhập số → hệ thống kiểm tra **pool có đủ câu không** trước khi sinh.

Đây đúng ý: *“từ dạng đề và mức độ khó, bốc ra được số lượng câu hỏi”*.

---

## 3. Đơn vị đếm trong ô — tránh bug nghiệp vụ

| Format | Đếm gì trong ma trận? | Ghi chú |
|--------|------------------------|---------|
| MCQ_SINGLE | 1 câu = 1 item | Đơn giản |
| SHORT_ANSWER | 1 câu = 1 item | Đơn giản |
| TRUE_FALSE_GROUP | **1 nhóm = 1 đơn vị ma trận** (gồm 4 ý) | Không đếm 4 ô riêng trừ khi giáo viên muốn ma trận theo ý |
| Stimulus + nhiều câu | Stimulus không tính điểm; các item con mới tính | Giống ngữ liệu bên trái demo Bộ |

**Khuyến nghị:** ma trận Phần II đếm theo **số câu Đ/S (group)**. Metadata mức độ có thể gắn per-ý; khi filter theo mức, rule cần chốt:

- **MVP đơn giản:** gắn 1 mức đại diện cho cả group (mức cao nhất trong 4 ý), hoặc  
- **Chuẩn hơn:** mỗi ý là item riêng cùng `group_id`, ma trận Phần II filter theo ý (phức tạp hơn — để sau).

---

## 4. Ràng buộc khi sinh đề (business rules)

### 4.1. Ràng buộc bắt buộc

1. Mỗi ô: `available_count >= requested_count`, nếu không → báo thiếu (liệt kê ô thiếu), **không sinh đề cụt**.  
2. Không lấy trùng cùng một `question_id` trong một ExamVersion.  
3. Câu thuộc group/stimulus: lấy cả bundle, không tách nửa.  
4. Tôn trọng `status = approved` (chỉ câu đã duyệt mới vào đề thi chính thức; luyện tập có thể cho `approved` + `practice_ok`).

### 4.2. Ràng buộc nên có sớm

5. Tránh trùng đề gần đây (cùng user/lớp): giảm xác suất câu đã ra trong N đề trước.  
6. `exclude_used_in_session` khi học sinh luyện nhiều lần cùng ma trận (optional toggle).  
7. Giới hạn số lần một câu xuất hiện toàn hệ thống / tháng (chống lộ đề nếu bán trung tâm).

### 4.3. Ràng buộc để sau

8. IRT / độ khó thống kê từ lịch sử làm bài (p-value, discrimination).  
9. Tạo nhiều mã đề tương đương (đảo thứ tự + thay biến số).

---

## 5. Thuật toán sinh đề (mức nghiệp vụ, chưa phải code tối ưu)

```
Input: Blueprint (danh sách Cell {filters, count, score_rule, section})
Output: ExamVersion hoặc lỗi thiếu pool

1. Validate tổng điểm ≈ 10 (với template chuẩn) hoặc cảnh báo nếu lệch.
2. For each Cell in Blueprint.cells (theo thứ tự section):
     candidates = Query(bank, filters, status=approved)
     candidates = ApplyExclusion(candidates, already_picked, recent_history)
     if len(candidates) < cell.count: fail with ShortageReport
     picked = RandomSample(candidates, cell.count)  // hoặc weighted
     append to exam with section order + score_rule
3. Assign display_order (có thể shuffle trong section nếu template cho phép)
4. Snapshot: lưu bản sao metadata câu vào ExamVersion
   (đề đã phát hành không bị sửa khi bank sửa câu sau này)
5. Return ExamVersion
```

**Snapshot:** rất quan trọng với đề thi trung tâm / tranh chấp điểm. Luyện tập có thể reference live hoặc snapshot nhẹ.

---

## 6. Ví dụ cụ thể: user bốc đề luyện “Hàm số + Tích phân”

Ma trận luyện:

| Chủ đề | NB | TH | VD |
|--------|----|----|-----|
| Khảo sát hàm số | 3 | 3 | 2 |
| Nguyên hàm – Tích phân | 2 | 2 | 2 |

Format: chỉ MCQ + short (user chọn).  
→ Hệ thống cần ít nhất 3+3+2 câu hàm số và 2+2+2 câu tích phân đúng mức trong bank.

UI nên hiện **tồn kho realtime**:

`NB hàm số: có 40 — yêu cầu 3 ✓`

---

## 7. Ví dụ: sinh đề thi thử TN THPT

Blueprint cố định phần I/II/III + scoring.  
Phân bổ chủ đề: dùng config mặc định của năm (bảng seed từ giáo viên).  
Sau sinh: tạo Session 90 phút, palette 22 “câu” (Phần II hiện 4 câu, mỗi câu 4 ý trên UI).

Chấm:

```
score = sum(MCQ correct)*0.25
      + sum(TF_group_score(correct_ideas))
      + sum(SHORT correct)*0.5
```

`TF_group_score`: map {1→0.1, 2→0.25, 3→0.5, 4→1.0}; 0 ý đúng → 0.

---

## 8. Phân biệt “Đề cố định” vs “Đề theo ma trận”

| Loại | Khi nào dùng | Lưu gì |
|------|--------------|--------|
| Fixed Exam | Đề thi thử đóng gói, đề giáo viên soạn tay | Danh sách câu cố định |
| Matrix-generated | Thi trung tâm nhiều ca, luyện không trùng | Blueprint + seed random + ExamVersion |

Cả hai đều cần **ExamVersion** cuối cùng để thí sinh làm. Matrix chỉ là cách tạo Version.

---

## 9. UX tối thiểu cho giáo viên (MVP)

1. Xem tồn kho theo (chủ đề × mức × format).  
2. Chọn template hoặc nhập bảng số.  
3. Preview thiếu/đủ.  
4. Nút **Sinh đề** → xem danh sách câu (ẩn đáp án tùy role) → **Xuất bản** vào kỳ thi / cho học sinh luyện.  
5. (Nice) Nhân bản ma trận, khóa ma trận đã dùng thi thật.

---

## 10. Anti-pattern cần tránh

- Chỉ tag “dễ/khó” 2 mức rồi gọi là ma trận.  
- Hard-code 50 câu × 0,2 điểm kiểu đề cũ 2006–2024.  
- Coi 4 ý Đ/S như 4 câu MCQ độc lập khi tính điểm.  
- Sinh đề khi thiếu pool rồi “bù câu lung tung” không theo ô — phá uy tín với giáo viên.
