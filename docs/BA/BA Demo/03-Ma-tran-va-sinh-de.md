# 03 — Ma trận đề thi & logic “bốc câu” / sinh đề

Đây là **trái tim nghiệp vụ** của core. Nếu phần này sai, ngân hàng câu hỏi chỉ là kho dump.

---

## 0. Bộ khung bài thi — trước khi vào ma trận

Trước khi mở [ma trận](./11-Chu-thich.md#ma-tran) để chọn câu, user phải cấu hình [khung bài thi](./11-Chu-thich.md#khung-bai-thi). Ma trận chỉ đổ câu vào các phần đã có trong khung.

Khung chốt ba thứ:

1. Bài thi có **bao nhiêu phần**.
2. **Cách tính điểm** của từng phần.
3. **Tổng điểm** của từng phần.

Template TN đổ sẵn khung (Toán: 3 phần, trần 3 + 4 + 3). Đề nhà trường thì user tự dựng. Dù đổ sẵn hay tự dựng, user thấy khung và sửa được **trước** khi vào ma trận.

### Phần tính điểm đều theo câu

User nhập số câu và tổng điểm phần. Điểm mỗi câu = tổng điểm phần / số câu. Câu đúng lấy hết mức đó, câu sai thì 0. Dùng cho trắc nghiệm nhiều lựa chọn và trả lời ngắn.

Ví dụ trên ảnh: 8 câu, tổng phần 8 điểm → mỗi câu 1 điểm.

![Phần trắc nghiệm: số câu, tổng điểm, điểm mỗi câu](<../../Pictures/Toan Phần 1 - cấu hình điểm.jpg>)

### Phần Đúng/Sai — thang % theo số ý đúng

Không chia đều. User nhập % điểm của câu khi đúng 1 ý, 2 ý, 3 ý, 4 ý. Điểm thực của câu = % đó × (tổng điểm phần / số câu phần).

Ví dụ trên ảnh, khớp thang tốt nghiệp khi trần một câu Đúng/Sai là 1 điểm (10% → 0,1 · 25% → 0,25 · 50% → 0,5 · 100% → 1):

| Số ý đúng | % điểm câu |
|-----------|------------|
| 1 | 10% |
| 2 | 25% |
| 3 | 50% |
| 4 | 100% |

![Thang điểm Đúng/Sai theo số ý đúng](<../../Pictures/Toan phần 2 số lượng câu đúng.jpg>)

Tổng điểm bài = cộng tổng điểm các phần trong khung. Template chuẩn vẫn ra 10. Khung lệch thang thì cảnh báo, không chặn bằng một số 10 gắn cứng trong code.

---

## 1. Ma trận là gì (trong ngữ cảnh sản phẩm)

**[Ma trận đề](./11-Chu-thich.md#ma-tran)** = bảng quy tắc phân bổ câu hỏi cho một đề / một phiên sinh đề.

Mỗi [ô ma trận](./11-Chu-thich.md#o-ma-tran) trả lời: *“Lấy bao nhiêu câu thỏa điều kiện X?”*

Điều kiện X tối thiểu (MVP):

- `subject` = Toán  
- `grade` hoặc `topic` ([chủ đề](./11-Chu-thich.md#chu-de) / dạng bài)  
- `cognitive_level` ∈ {[NB](./11-Chu-thich.md#nb), [TH](./11-Chu-thich.md#th), [VD](./11-Chu-thich.md#vd), [VDC](./11-Chu-thich.md#vdc)}  
- `item_format` ∈ {[MCQ_SINGLE](./11-Chu-thich.md#mcq), [TRUE_FALSE_GROUP](./11-Chu-thich.md#dung-sai), [SHORT_ANSWER](./11-Chu-thich.md#tra-loi-ngan), …}  
- (optional) [`competency`](./11-Chu-thich.md#nang-luc), `chapter`, tags

**[Sinh đề](./11-Chu-thich.md#sinh-de)** = với mỗi ô, lấy ngẫu nhiên (hoặc theo trọng số) đủ đơn vị từ [ngân hàng](./11-Chu-thich.md#ngan-hang-cau-hoi) **còn đủ [tồn kho](./11-Chu-thich.md#ton-kho)**, tạo **[ExamVersion](./11-Chu-thich.md#exam-version) DRAFT + [Đặc tả](./11-Chu-thich.md#dac-ta-de) DRAFT** → GV chỉnh → **[khóa](./11-Chu-thich.md#khoa-de)** mới đưa vào thi/luyện chính thức.

```
Khung bài thi (số phần, cách tính, tổng điểm từng phần)
        │
        ▼
Ma trận (Blueprint)  [COARSE | FINE]
        │
        ▼
  Với mỗi ô: query QuestionBank (theo câu; Đ/S = 1 câu)
        │
        ▼
  Chọn N đơn vị thỏa filter + ràng buộc toàn cục
        │
        ▼
  ExamVersion DRAFT + ExamSpec DRAFT (đặc tả)
        │
        ▼
  GV điều chỉnh (đổi câu cùng ô, reorder, sửa YCCĐ)
        │
        ▼
  Validate khớp ma trận → LOCK (snapshot)
        │
        ▼
  Gắn vào Session thi / Luyện tập
```

Chi tiết đặc tả & quyết định chốt: **[09-Dac-ta-de-va-quy-tac-da-chot.md](./09-Dac-ta-de-va-quy-tac-da-chot.md)**.

---

## 2. Cách user tạo ma trận + độ chi tiết

User chọn **[granularity](./11-Chu-thich.md#granularity)**:

| Mode | Filter ô | Ai dùng |
|------|----------|---------|
| **[COARSE](./11-Chu-thich.md#coarse)** | Phần + chủ đề [L1](./11-Chu-thich.md#l1) + mức (NB/TH/VD/VDC) + format | Nhanh, luyện, không soi sát năm |
| **[FINE](./11-Chu-thich.md#fine)** | COARSE + dạng bài [L2](./11-Chu-thich.md#l2) / đơn vị kiến thức mịn | Kiểm soát chi tiết, sát phân bố năm |

### A. Template có sẵn

Ví dụ `TN_THPT_TOAN_2025`:

| Phần | Format | Số đơn vị | Filter bank | Điểm rule |
|------|--------|-----------|-------------|-----------|
| I | MCQ_SINGLE | 12 câu | 12 câu | 0,25/câu |
| II | TRUE_FALSE_GROUP | 4 câu (mỗi câu cố định 4 ý) | **4 câu** theo topic + mức câu | 0,1/0,25/0,5/1 theo số ý đúng |
| III | SHORT_ANSWER | 6 câu | 6 câu | 0,5/câu |

Phân bổ chủ đề mặc định: xem [10](./10-Danh-muc-chu-de-Toan-seed.md). User COARSE chỉ sửa số theo L1; FINE sửa thêm L2.

### B. Ma trận tự do

| Chủ đề \ Mức | NB | TH | VD | VDC |
|--------------|----|----|----|-----|
| Khảo sát hàm số | 2 | 2 | 1 | 1 |
| Tích phân | 1 | 1 | 1 | 1 |

Với Đ/S: ô = **số câu** (group) đúng chủ đề × mức — giống MCQ. Không profile mức từng ý.

---

## 3. Đơn vị đếm — Đ/S theo **cả câu** (đã chốt lại 2026-11-05)

| Format | Đơn vị ma trận / mức độ | Ghi chú |
|--------|-------------------------|---------|
| MCQ_SINGLE | 1 câu | |
| SHORT_ANSWER | 1 câu | [Exact match](./11-Chu-thich.md#exact-match); làm tròn ghi trong [stem](./11-Chu-thich.md#stem) |
| TRUE_FALSE_GROUP | **1 câu = 1 đơn vị**; `cognitive_level` trên câu | 4 ý cố định trong câu; không gắn/lọc mức theo ý |
| Stimulus | Thuộc câu / không tính điểm riêng | |

**Chốt:**

- Bank, ma trận, đặc tả, tồn kho: đếm **câu Đ/S**.  
- 4 ý chỉ phục vụ hiển thị + chấm điểm từng ý trong câu.  
- Sinh đề Phần II: `RandomSample` các câu thỏa topic + mức + format.

---

## 4. Ràng buộc khi sinh đề (business rules)

### 4.1. Ràng buộc bắt buộc

1. Mỗi ô: `available_count >= requested_count`, nếu không → báo thiếu (liệt kê ô thiếu), **không sinh đề cụt**.  
2. Không lấy trùng cùng một `question_id` trong một ExamVersion.  
3. Câu thuộc group/[stimulus](./11-Chu-thich.md#stimulus): lấy cả bundle, không tách nửa.
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
Input: Blueprint (cells, granularity, score policies)
Output: ExamVersion DRAFT + ExamSpec DRAFT  |  ShortageReport

1. Validate tổng điểm bài = tổng các phần trong khung (template chuẩn vẫn ≈ 10; lệch thì cảnh báo).
2. For each Cell (theo section):
     candidates = Query(bank, filters ở mức CÂU, status=approved)
     // Phần II: mỗi candidate = 1 câu Đ/S (đủ 4 ý cố định)
     candidates = ApplyExclusion(...)
     if không đủ: fail ShortageReport (liệt kê ô)
     picked = RandomSample / weighted
     append câu (kèm 4 ý nếu Đ/S)
3. Build ExamSpec rows từ metadata câu + YCCĐ mặc định (từ bank)
4. Assign display_order (draft — GV còn sửa được)
5. Return DRAFT (chưa snapshot khóa)
6. Sau khi GV chỉnh + Validate khớp ma trận → LOCK:
     snapshot toàn bộ stem/key/metadata vào ExamVersion + ExamSpec
```

**[Snapshot](./11-Chu-thich.md#snapshot) chỉ sau LOCK.** Draft được sửa; đề đã có [Attempt](./11-Chu-thich.md#attempt) thì không sửa — clone version mới.

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

Blueprint cố định phần I/II/III + [scoring](./11-Chu-thich.md#score-policy).  
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

## 8. Phân biệt “[Đề cố định](./11-Chu-thich.md#de-dong-goi)” vs “Đề theo ma trận”

| Loại | Khi nào dùng | Lưu gì |
|------|--------------|--------|
| Fixed / đóng gói | GV chọn tay từng câu; hoặc bán gói đề sẵn; hoặc tái dùng đề đã khóa | Danh sách câu cố định → ExamVersion |
| Matrix-generated | Bốc theo ma trận (random **một lần** lúc sinh) | Blueprint + kết quả bốc → ExamVersion |

**Quan trọng (công bằng):** sau khi khóa, học sinh trong một đợt thi mở **cùng link / cùng ExamVersion** — cùng một đề. Không random lại theo từng thí sinh. Muốn nhiều mã đề thì sinh thêm nhiều ExamVersion có chủ đích.

Chi tiết đã chốt: [`01` §6.5](./01-Tong-quan-san-pham.md).

---

## 9. UX tối thiểu cho giáo viên (MVP)

1. Xem tồn kho theo (chủ đề × mức × format) — **Đ/S đếm theo câu**.  
2. Chọn template + mode COARSE/FINE; nhập/chỉnh bảng số.  
3. Preview thiếu/đủ theo ô.  
4. **Sinh đề** → màn **Đặc tả + danh sách câu** (đổi câu cùng ô, reorder, sửa [YCCĐ](./11-Chu-thich.md#yccd)).  
5. **Khóa đề** (validate khớp ma trận) → xuất bản kỳ thi / luyện.  
6. (Nice) Nhân bản ma trận; export đặc tả PDF.

---

## 10. Anti-pattern cần tránh

- Chỉ tag “dễ/khó” 2 mức rồi gọi là ma trận.  
- Hard-code 50 câu × 0,2 điểm kiểu đề cũ 2006–2024.  
- Coi 4 ý Đ/S như 4 câu độc lập khi **tính điểm** (điểm vẫn theo số ý đúng trong câu).  
- Gắn / lọc mức độ **từng ý** Đ/S — phức tạp không cần thiết; mức gắn **cả câu**.  
- Bỏ qua đặc tả / xuất bản ngay sau random mà GV không review.  
- Sinh đề khi thiếu pool rồi “bù câu lung tung” không theo ô.  
- Short answer cho điểm “gần đúng” khi mode thi.
