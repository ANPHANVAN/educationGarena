# 09 — Đặc tả đề & các quy tắc đã chốt (2026-11-04)

Tài liệu này **ghi quyết định** từ founder sau khi review BA Demo. Override các chỗ “cần xác nhận” / “khuyến nghị MVP đơn giản” ở file 02–03–05 nếu mâu thuẫn.

---

## 1. Đặc tả đề = bắt buộc trong MVP

### 1.1. Khái niệm (theo nghiệp vụ ngành / [CV 7991](./11-Chu-thich.md#cv-7991))

| Tài liệu | Vai trò |
|----------|---------|
| **[Ma trận](./11-Chu-thich.md#ma-tran)** | Bảng **ĐẾM**: [chủ đề](./11-Chu-thich.md#chu-de) × [dạng thức](./11-Chu-thich.md#dang-thuc) × [mức](./11-Chu-thich.md#cap-do-tu-duy) → bao nhiêu câu / điểm |
| **[Đặc tả đề](./11-Chu-thich.md#dac-ta-de)** | Bảng **MÔ TẢ + DANH SÁCH CÂU ĐÃ CHỌN**: mỗi vị trí trên đề gắn [yêu cầu cần đạt](./11-Chu-thich.md#yccd) / mô tả ngắn + metadata câu thực tế |
| **Đề** | Nội dung thí sinh làm ([ExamVersion](./11-Chu-thich.md#exam-version)) |

Trong sản phẩm: sau khi **[bốc câu](./11-Chu-thich.md#sinh-de)**, hệ thống sinh **bản đặc tả draft** từ câu đã chọn → giáo viên **xem / chỉnh** (đổi câu, đổi thứ tự, chỉnh mô tả YCCĐ nếu cần) → mới **[khóa](./11-Chu-thich.md#khoa-de) & xuất bản**.

### 1.2. Luồng MVP (chốt)

```
Khung bài thi (số phần, cách tính, tổng điểm từng phần)
        │
        ▼
Ma trận (Blueprint)
        │
        ▼
   Bốc câu (generate)
        │
        ▼
 ExamVersion DRAFT + Đặc tả DRAFT
        │
        ▼
 GV điều chỉnh (swap câu, reorder, sửa ghi chú đặc tả)
        │
        ▼
 Validate khớp ma trận (số câu/mức/format từng ô)
        │
        ▼
 LOCK → ExamVersion PUBLISHED (+ snapshot đặc tả)
```

**Không** cho học sinh làm trên bản chưa khóa (trừ mode preview GV).

### 1.3. Nội dung một dòng đặc tả (tối thiểu)

| Trường | Bắt buộc |
|--------|----------|
| Vị trí đề (Phần, số câu) | ✓ |
| Topic / đơn vị kiến thức | ✓ |
| Cognitive level của **câu** | ✓ |
| Item format | ✓ |
| Mô tả yêu cầu cần đạt / ghi chú đặc tả (text) | ✓ (có thể auto-fill từ [bank](./11-Chu-thich.md#ngan-hang-cau-hoi) rồi sửa) |
| Question id (hoặc [snapshot](./11-Chu-thich.md#snapshot)); Đ/S kèm 4 ý trong nội dung | ✓ |
| Điểm tối đa dòng (Đ/S: trần 1 điểm/câu theo policy TN) | ✓ |

Xuất: xem trên web + (P1) export PDF/Word giống hồ sơ trường.

### 1.4. Điều chỉnh sau bốc — phép / cấm

| Thao tác | Cho phép? |
|----------|-----------|
| Đổi câu A → câu B cùng ô ma trận (cùng filter) | ✓ |
| Đổi thứ tự trong phần (nếu template cho phép) | ✓ |
| Sửa text “Yêu cầu cần đạt” trên đặc tả | ✓ |
| Thêm/bớt câu làm lệch số ô ma trận | ✗ trừ khi GV sửa ma trận rồi sinh lại |
| Sửa đáp án trên đề đã khóa đã có [Attempt](./11-Chu-thich.md#attempt) | ✗ (tạo version mới) |

---

## 2. Cấp độ tư duy — có VDC; báo cáo 3 mức thì gộp

| Trong bank & ma trận | [NB](./11-Chu-thich.md#nb), [TH](./11-Chu-thich.md#th), [VD](./11-Chu-thich.md#vd), **[VDC](./11-Chu-thich.md#vdc)** (4 mức) |
|----------------------|----------------------------|
| Khi báo cáo / xuất theo khung Bộ 3 mức (Biết–Hiểu–Vận dụng) | **VDC ⊂ Vận dụng (VD)** |

Công thức báo cáo:

```
NB_report = count(NB)
TH_report = count(TH)
VD_report = count(VD) + count(VDC)
```

UI: luôn nhập/lọc 4 mức; toggle “Xem theo 3 mức (gộp VDC→VD)” trên dashboard / đặc tả xuất Bộ.

---

## 3. Trả lời ngắn — chấm nghiêm (kiểu thi ĐH / TN)

**Đã chốt:**

1. Quy ước làm tròn / đơn vị / số chữ số **phải nằm trong đề bài ([stem](./11-Chu-thich.md#stem))**.  
2. Hệ thống **chỉ chấp nhận đáp án khớp đúng** với key đã chuẩn hóa ([exact match](./11-Chu-thich.md#exact-match) sau normalize).  
3. **Không** dùng `tolerance` / sai số tương đối kiểu “gần đúng cũng cho điểm” ở MVP thi chính thức.

Normalize tối thiểu trước so khớp:

- Trim khoảng trắng  
- Thống nhất dấu thập phân `,` → `.` (hoặc ngược lại một chiều cố định)  
- Bỏ khoảng nghìn nếu có  
- So sánh **chuỗi đã chuẩn hóa** với danh sách `accepted_answers` (có thể nhiều alias **tương đương tuyệt đối**, vd. `1/2` và `0.5` chỉ khi GV chủ động khai báo cả hai)

Nếu stem yêu cầu “làm tròn đến hàng đơn vị” thì key phải là giá trị **đã làm tròn**; thí sinh điền khác → **sai**.

> Luyện tập sau này có thể có mode “gợi ý sai số” — **không** trộn vào mode thi.

---

## 4. Độ chi tiết ma trận — user chọn

Hai mode trên cùng Blueprint:

| Mode | Ô filter | Khi nào dùng |
|------|----------|--------------|
| **[COARSE](./11-Chu-thich.md#coarse)** (mặc định nhanh) | `section/phần` + `topic` + `cognitive_level` (+ format) | Luyện / GV không muốn soi từng dạng con |
| **[FINE](./11-Chu-thich.md#fine)** | COARSE + tag [dạng bài](./11-Chu-thich.md#l2) / đơn vị kiến thức mịn hơn / (optional) [competency](./11-Chu-thich.md#nang-luc) | Kiểm soát sát đề năm, trung tâm |

User chọn mode khi tạo ma trận; tồn kho và bốc câu theo đúng độ chi tiết đã chọn.  
Template `TN_THPT_TOAN_*` có thể ship sẵn bản COARSE (theo chủ đề bảng dưới) và bản FINE (tách dạng: cực trị, tiệm cận, min-max thực tế…).

---

## 5. [Đúng/Sai](./11-Chu-thich.md#dung-sai) — mức độ khó theo **cả câu** (đã chỉnh lại 2026-11-05)

> Override quyết định “theo từng ý” trong commit docs trước: quá phức tạp cho thiết kế lẫn user vận hành.

**Chốt đơn giản:**

- Một câu Đ/S = **1 đơn vị** trong bank / ma trận / đặc tả / [tồn kho](./11-Chu-thich.md#ton-kho).  
- `cognitive_level` + `topic` gắn ở **cấp câu (group)**, không gắn từng ý.  
- 4 ý (a/b/c/d) là **cấu trúc cố định** của câu: stem ý + đáp án Đ/S + (optional) lời giải ý. User **không** chỉnh mức từng ý, cũng không bốc/lọc theo mức ý.  
- [Stimulus](./11-Chu-thich.md#stimulus) / đoạn mở đầu chung thuộc câu đó.

### Vì sao hợp lý hơn

| Theo từng ý (bỏ) | Theo cả câu (giữ) |
|------------------|-------------------|
| Ma trận Phần II phải profile 4 mức / group | Ô ma trận: “1 câu Đ/S topic X mức Y” — giống MCQ |
| Tồn kho & thiếu pool khó giải thích cho GV | Đếm câu như các phần khác |
| Sinh đề ràng buộc bộ ý phức tạp | Random theo filter câu |

### Chấm điểm — không đổi

Vẫn theo **số ý đúng trong câu**. Thang % nằm trên [khung bài thi](./11-Chu-thich.md#khung-bai-thi), không gắn vào từng câu trong bank. Khung TN mặc định: 1→10% · 2→25% · 3→50% · 4→100% (trần câu 1 điểm thì ra 0,1 / 0,25 / 0,5 / 1,0).  
(Điểm phụ thuộc làm đúng bao nhiêu ý; **phân loại độ khó** thì vẫn là thuộc tính của cả câu.)

### Sinh đề Phần II

```
Filter: topic (+ L2 nếu FINE) + cognitive_level + format=TRUE_FALSE_GROUP
→ lấy N câu (group đủ 4 ý) thỏa filter
```

---

## 6. Entity bổ sung (cập nhật model)

- `ExamSpec` / `ExamSpecification` — đặc tả gắn `exam_version_id`, status draft|locked  
- `ExamSpecRow` — từng dòng đặc tả (Đ/S: **1 dòng / câu**, có thể liệt kê 4 ý trong nội dung)  
- [`Blueprint.granularity`](./11-Chu-thich.md#granularity) — `COARSE` | `FINE`  
- `cognitive_level` — bắt buộc trên **[Question](./11-Chu-thich.md#question-item)** ([MCQ](./11-Chu-thich.md#mcq) / Đ/S group / [Short](./11-Chu-thich.md#tra-loi-ngan)); ý Đ/S **không** có level riêng  
- Bỏ `tolerance` khỏi short-answer policy thi; chỉ còn `accepted_answers[]`

---

## 7. Bộ khung bài thi — trước ma trận (2026-11-05)

Trước khi vào ma trận chọn câu, user cấu hình [khung bài thi](./11-Chu-thich.md#khung-bai-thi):

1. Bài có bao nhiêu phần.
2. Cách tính điểm của từng phần.
3. Tổng điểm của từng phần.

Phần Đúng/Sai cấu hình % điểm theo số ý đúng (1 ý, 2 ý, 3 ý, 4 ý), không chia đều. Phần trắc nghiệm và trả lời ngắn: điểm mỗi câu = tổng điểm phần / số câu.

Ảnh ví dụ và công thức: [03 §0](./03-Ma-tran-va-sinh-de.md).
