# 07 — Nhiều môn, template kỳ thi & mở rộng sau

**Định hướng:** hỗ trợ **nhiều môn ngay từ đầu** (cùng engine). Không hard-code một môn.  
**Chưa làm riêng đợt đầu:** Ngữ văn, Tin học, Công nghệ — để ngỏ. Chi tiết cắt phạm vi: [06](./06-MVP-uu-tien-va-pham-vi.md).

---

## 1. Bức tranh gọn

```
Platform (dùng chung)
  · user, kỳ thi, attempt, timer, CBT UI
  · blueprint engine + tồn kho + đặc tả + khóa đề
  · score policy config · xáo câu / xáo A–D
  · stimulus bundle (ngữ liệu dùng chung)

Content theo môn (pack)
  · topic tree L1/L2 · bank câu · template số câu / điểm

Một môn  ──►  nhiều template kỳ   (TN THPT, kiểm tra, ô trong đề ĐGNL…)
Một đề    ──►  có thể trộn nhiều môn (ĐGNL-style)
```

Hầu hết môn TN chỉ xoay quanh **2–3 dạng thức** (MCQ, Đ/S, short) → cùng model đã có cho Toán là đủ kỹ thuật; khác chủ yếu ở **nội dung + template**.

---

## 2. Một môn ↔ nhiều “dạng đề” (không nhầm với L1/L2)

| Khái niệm | Nghĩa trong hệ thống |
|-----------|----------------------|
| **Môn (Subject)** | Toán, Lý, Anh… — gắn `subject_id` trên câu / ô ma trận |
| **Template kỳ thi** | Cấu trúc đề: TN 3 phần, TN 2 phần, chỉ MCQ, kiểm tra trường, **ĐGNL trộn môn**… |
| **[L1](./11-Chu-thich.md#l1) / [L2](./11-Chu-thich.md#l2)** | Cây **chủ đề / dạng bài trong một môn** — dùng để lọc ma trận COARSE/FINE, **không** phải “loại kỳ thi” |

**Đã ghi nhận:** cùng một môn có thể nằm trong **nhiều template** khác nhau. Ví dụ Toán:

- Full đề TN THPT (22 câu, 3 phần)  
- Kiểm tra định kỳ (chọn vài chương / vài phần)  
- Một khối câu trong đề ĐGNL trộn với Lý/Hóa/…  

GV **chọn phần / môn / chủ đề** khi soạn blueprint → linh hoạt giữa các môn, không bắt mỗi lần thi full cấu trúc Bộ.

Câu hỏi: gắn **≥1 topic L1** trong môn đó; L2 optional (bắt buộc khi ô FINE đòi dạng đó). Xem [10](./10-Danh-muc-chu-de-Toan-seed.md), [11](./11-Chu-thich.md#l1).

---

## 3. Phần dùng chung vs phần theo môn

### Dùng chung (platform)

- User, org, kỳ thi, [attempt](./11-Chu-thich.md#attempt), timer, palette  
- [Blueprint](./11-Chu-thich.md#ma-tran) (filter + count + [sinh đề](./11-Chu-thich.md#sinh-de) + shortage) — ô có thể thuộc môn khác nhau  
- Vòng đời câu (draft → approved)  
- [Score policy](./11-Chu-thich.md#score-policy) cấu hình được  
- [CBT](./11-Chu-thich.md#cbt): 1 cột / 2 cột ([stimulus](./11-Chu-thich.md#stimulus) \| câu)  
- Xáo thứ tự **khối câu** + xáo phương án A–D  

### Theo môn (content pack)

| Thành phần | Ví dụ |
|------------|--------|
| Topic tree L1/L2 | Toán: ĐS–HH–XS; Anh: skill + theme |
| Item formats dùng | Toán đủ 3 dạng; Anh chủ yếu MCQ; Sử: MCQ+Đ/S |
| Score / blueprint template | `TN_THPT_*`, `SCHOOL_*`, `DGNL_MIX_*` |
| Render | LaTeX, hình, bảng; (sau) audio |
| Short-answer rules | Số / làm tròn; đơn vị (Lý/Hóa) khi cần |

---

## 4. Đề đánh giá năng lực (trộn nhiều môn)

- Blueprint **multi-subject**: mỗi ô (hoặc mỗi section) chỉ định `subject_id` + filter topic/mức/format.  
- Chấm theo score policy của từng khối / cả bài (config) — ĐGNL thực tế của ĐHQG có format riêng; MVP = **thi thử trắc nghiệm liên môn**, không copy nguyên quy chế một kỳ ĐGNL cụ thể ngày đầu.  
- Bank vẫn tách theo môn; đề chỉ **ghép** lúc sinh.  
- Audio / tự luận ĐGNL: sau.

---

## 5. Stimulus — lưu ý đặc biệt

| # | Lưu ý | Hệ quả |
|---|--------|--------|
| 1 | Stimulus **không phải câu tính điểm** | Entity riêng (hoặc thuộc bundle); điểm nằm ở câu gắn vào |
| 2 | Nhiều câu **dùng chung** một ngữ liệu | Sinh đề / xáo đề: lấy **cả bundle**, không tách nửa |
| 3 | Xáo thứ tự câu | Xáo **khối** (stimulus + các câu thuộc nó) như một đơn vị; trong khối có thể giữ thứ tự cố định hoặc xáo nhẹ tùy policy |
| 4 | Xáo A–D | Chỉ trên MCQ; **không** áp dụng kiểu “đảo” cho Đ/S ý / short |
| 5 | CBT 2 cột | Trái: ngữ liệu; phải: câu — giống vibe demo Bộ |
| 6 | Loại media | Text / ảnh / bảng = MVP; **audio = P2+** (chừa field, chưa pipeline) |
| 7 | Môn nào cần sớm | Anh (đọc hiểu), Sử/GDKTPL/Địa (ngữ liệu), Lý/Hóa (thí nghiệm chung cho Đ/S) |

Chi tiết thuật ngữ: [11 — Stimulus](./11-Chu-thich.md#stimulus).

---

## 6. Việc thiết kế đúng từ đầu (tránh đập đi)

1. `subject_id` trên Question, Blueprint cell, Exam.  
2. `ItemFormat` + `ScorePolicy` + `BlueprintTemplate` là dữ liệu/config.  
3. Topic L1/L2 là bảng dữ liệu theo môn — không enum hard-code.  
4. TRUE_FALSE_GROUP và SHORT_ANSWER first-class (nhiều môn TN dùng).  
5. Bảng `questions` dùng chung — không `math_questions`.  
6. Đề trộn môn = nhiều cell khác `subject_id`, không fork engine.  
7. Chừa chỗ media `audio` trên stimulus; chưa implement nghe.  
8. Văn / Tin / CN: không chặn schema (ESSAY, track) nhưng **không build UX/rule riêng** trong MVP.

---

## 7. Để ngỏ — mở khi có nhu cầu

| Hạng mục | Điều kiện / việc cần thêm |
|----------|---------------------------|
| **Ngữ văn** | ESSAY + chấm tay / rubric; không nhét auto-grade |
| **Tin học** | Blueprint **track** (nhánh KHMT / THƯD); render code |
| **Công nghệ** | Template 2 phần + stimulus bản vẽ / quy trình |
| **Audio** | Player + lưu file + (sau) đề nghe |
| Partner / nhượng quyền môn | Pack nội dung + người chủ trì bank |

Không cần đủ hết ngày đầu — chỉ **đừng thiết kế hẹp** tới mức phải viết lại.

---

## 8. Kết luận

- MVP = **platform đa môn** + seed sâu Toán + template các môn TN phổ biến + đề trộn môn.  
- Chưa làm riêng: Văn, Tin, Công nghệ.  
- L1/L2 = phân loại **trong môn**; “nhiều dạng đề” = **nhiều template / chọn phần** trên cùng môn.  
- Stimulus: bundle + xáo theo khối + UI 2 cột; audio sau.
