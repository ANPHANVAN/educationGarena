# 09 — Đặc tả đề & các quy tắc đã chốt (2026-11-04)

Tài liệu này **ghi quyết định** từ founder sau khi review BA Demo. Override các chỗ “cần xác nhận” / “khuyến nghị MVP đơn giản” ở file 02–03–05 nếu mâu thuẫn.

---

## 1. Đặc tả đề = bắt buộc trong MVP

### 1.1. Khái niệm (theo nghiệp vụ ngành / CV 7991)

| Tài liệu | Vai trò |
|----------|---------|
| **Ma trận** | Bảng **ĐẾM**: chủ đề × dạng thức × mức → bao nhiêu câu / điểm |
| **Đặc tả đề** | Bảng **MÔ TẢ + DANH SÁCH CÂU ĐÃ CHỌN**: mỗi vị trí trên đề gắn yêu cầu cần đạt / mô tả ngắn + metadata câu thực tế |
| **Đề** | Nội dung thí sinh làm (ExamVersion) |

Trong sản phẩm: sau khi **bốc câu**, hệ thống sinh **bản đặc tả draft** từ câu đã chọn → giáo viên **xem / chỉnh** (đổi câu, đổi thứ tự, chỉnh mô tả YCCĐ nếu cần) → mới **khóa & xuất bản**.

### 1.2. Luồng MVP (chốt)

```
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
| Vị trí đề (Phần, số câu, ý a/b/c/d nếu Đ/S) | ✓ |
| Topic / đơn vị kiến thức | ✓ |
| Cognitive level của **đơn vị chấm** (câu hoặc ý) | ✓ |
| Item format | ✓ |
| Mô tả yêu cầu cần đạt / ghi chú đặc tả (text) | ✓ (có thể auto-fill từ bank rồi sửa) |
| QuestionItem id (hoặc snapshot) | ✓ |
| Điểm tối đa dòng | ✓ |

Xuất: xem trên web + (P1) export PDF/Word giống hồ sơ trường.

### 1.4. Điều chỉnh sau bốc — phép / cấm

| Thao tác | Cho phép? |
|----------|-----------|
| Đổi câu A → câu B cùng ô ma trận (cùng filter) | ✓ |
| Đổi thứ tự trong phần (nếu template cho phép) | ✓ |
| Sửa text “Yêu cầu cần đạt” trên đặc tả | ✓ |
| Thêm/bớt câu làm lệch số ô ma trận | ✗ trừ khi GV sửa ma trận rồi sinh lại |
| Sửa đáp án trên đề đã khóa đã có Attempt | ✗ (tạo version mới) |

---

## 2. Cấp độ tư duy — có VDC; báo cáo 3 mức thì gộp

| Trong bank & ma trận | NB, TH, VD, **VDC** (4 mức) |
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

1. Quy ước làm tròn / đơn vị / số chữ số **phải nằm trong đề bài (stem)**.  
2. Hệ thống **chỉ chấp nhận đáp án khớp đúng** với key đã chuẩn hóa (exact match sau normalize).  
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
| **COARSE** (mặc định nhanh) | `section/phần` + `topic` + `cognitive_level` (+ format) | Luyện / GV không muốn soi từng dạng con |
| **FINE** | COARSE + tag dạng bài / đơn vị kiến thức mịn hơn / (optional) competency | Kiểm soát sát đề năm, trung tâm |

User chọn mode khi tạo ma trận; tồn kho và bốc câu theo đúng độ chi tiết đã chọn.  
Template `TN_THPT_TOAN_*` có thể ship sẵn bản COARSE (theo chủ đề bảng dưới) và bản FINE (tách dạng: cực trị, tiệm cận, min-max thực tế…).

---

## 5. Đúng/Sai — chuẩn theo **từng ý** (không gộp mức cả group)

**Đã chốt hướng chuẩn (không làm bản “MVP đơn giản gộp mức group”):**

- **Stimulus / mở đầu chung** = bối cảnh dùng chung (không mang `cognitive_level` để filter ma trận).  
- Mỗi **ý (a/b/c/d)** = `QuestionItem` độc lập về:
  - `cognitive_level` (NB|TH|VD|VDC) — **bắt buộc**
  - `topic` (thường cùng topic group, vẫn cho phép lệch nếu cần)
  - đáp án Đ/S + lời giải ý
- Ma trận Phần II / filter bank: đếm và bốc theo **ý** (hoặc theo ràng buộc “đủ 4 ý thuộc cùng group thỏa phân bố mức”).

### Hệ quả sinh đề Phần II

Có hai chiến lược kỹ thuật (cùng model dữ liệu):

**A. Bốc theo group có ràng buộc mức các ý (khuyến nghị UX gần đề thật)**  
- Chọn group (stimulus + 4 ý) sao cho **bộ 4 mức** khớp ô ma trận (vd. 1 TH + 2 VD + 1 VDC).  
- Hiển thị vẫn là 1 câu Đ/S 4 ý.

**B. Bốc từng ý rồi ghép**  
- Rủi ro mất tính thống nhất ngữ cảnh — chỉ dùng khi bank gắn `group_id` sẵn và chỉ lấy đủ 4 ý cùng group.

→ **MVP implement A**, dữ liệu vẫn per-ý để báo cáo/đặc tả/tồn kho đúng chuẩn.

Chấm điểm: vẫn theo **số ý đúng trong group** (0,1 / 0,25 / 0,5 / 1) khi dùng score policy TN — không đổi.

---

## 6. Entity bổ sung (cập nhật model)

- `ExamSpec` / `ExamSpecification` — đặc tả gắn `exam_version_id`, status draft|locked  
- `ExamSpecRow` — từng dòng đặc tả  
- `Blueprint.granularity` — `COARSE` | `FINE`  
- `QuestionItem.cognitive_level` — bắt buộc với mọi item chấm được (MCQ = 1 item; Đ/S = 4 items; Short = 1 item)  
- Bỏ `tolerance` khỏi short-answer policy thi; chỉ còn `accepted_answers[]`
