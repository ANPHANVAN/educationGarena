# 06 — Hệ quả thiết kế platform (sau khi nhìn toàn ngành)

Tài liệu này trả lời: *Biết cấu trúc các môn rồi thì BA/dev phải giữ nguyên tắc gì?*

---

## 1. Một engine — nhiều template

Đừng viết `MathExamService`. Hãy có:

| Lớp | Ví dụ |
|-----|--------|
| `ItemFormat` | MCQ_SINGLE, TRUE_FALSE_GROUP, SHORT_ANSWER, ESSAY, (ORDERING…) |
| `ScorePolicy` | `tn_thpt_toan_2025`, `tn_thpt_ly_2025`, `tn_thpt_anh_2025`, `school_mix_70_30` |
| `BlueprintTemplate` | Số câu từng phần + filter + track (Tin) |
| `SubjectContentPack` | Topic tree + media rules + short-answer normalizer |

Mọi môn TN 2025 chỉ là **cấu hình** trên cùng mô hình đã mô tả cho Toán.

---

## 2. Checklist format — môn nào cần gì

| Format / capability | Toán | Lý Hóa Sinh Địa | Sử GDKTPL CN | Tin | Anh | Văn |
|---------------------|------|-----------------|--------------|-----|-----|-----|
| MCQ | ✓ | ✓ | ✓ | ✓ | ✓ | — |
| Đ/S group 4 ý | ✓ | ✓ | ✓ | ✓ | — | — |
| Short answer | ✓ | ✓ | — | — | — | — |
| Essay / viết dài | — | (định kỳ) | (định kỳ) | — | (định kỳ) | ✓ TN |
| Stimulus dùng chung | hữu ích | **rất cần** | **rất cần** | cần | **bắt buộc** | **bắt buộc** |
| Track / nhánh đề | — | — | — | **có** | — | — |
| LaTeX | ✓ | ✓ | ít | ít | — | — |
| Code block | — | — | — | ✓ | — | — |
| Bản đồ / Atlat UX | — | Địa | Sử (lược đồ) | — | — | — |

**MVP Toán đã cover cột quan trọng nhất cho 80% môn trắc nghiệm.** Thiếu sớm nhất khi mở rộng: **Stimulus UX** (Anh/Sử) và **Track** (Tin).

---

## 3. Ma trận vẫn là ngôn ngữ chung của ngành

Dù môn gì, giáo viên vẫn nghĩ:

```
(Chủ đề / dạng bài) × (NB|TH|VD|VDC) × (dạng thức câu) → số câu / điểm
```

Khác nhau chỉ là:

- Cây chủ đề  
- Template số ô mặc định (18-4-6 vs 24-4-0 vs 40-0-0)  
- Có tự luận kèm không (định kỳ 10–11)

→ File BA `03-Ma-tran-va-sinh-de.md` **vẫn đúng** khi mở môn; chỉ thêm template.

---

## 4. Thứ tự mở môn đề xuất (cân bằng effort & thị trường)

| Ưu tiên | Môn | Lý do |
|---------|-----|-------|
| 0 | **Toán** | Đang làm; đủ 3 format khó |
| 1 | **Vật lí hoặc Hóa** | Copy template 18-4-6; short 0,25; cùng GV tự nhiên |
| 2 | **Tiếng Anh** | Nhu cầu lớn; scoring dễ; cần passage UX |
| 3 | **Sinh / Địa** | Giống Lý về khung |
| 4 | **Sử / GDKTPL** | Bỏ short; nặng ngữ liệu |
| 5 | **Tin** | Thêm track |
| 6 | **Văn** | Chấm tay / quy trình khác |
| ? | Công nghệ | Market hẹp hơn trừ trung tâm nghề |

---

## 5. Cạm bẫy khi “nhìn toàn ngành”

1. **Ôm 17 môn từ đầu** → bank chết, sản phẩm không demo được.  
2. **Hard-code điểm short 0,5** → gãy Lý/Hóa.  
3. **Không có Stimulus** → Anh/Sử/Địa làm xấu.  
4. **Coi Đ/S như 4 MCQ độc lập khi chấm** → sai mọi môn có Phần II.  
5. **Làm Văn sớm vì “ai cũng học Văn”** → kẹt chấm bài.  
6. **Bỏ qua kiểm tra định kỳ** — đây mới là tần suất GV dùng ma trận quanh năm; TN chỉ là mùa cao điểm.

---

## 6. Một hình dung “toàn ngành” đóng gói

```
CT GDPT 2018
    │
    ├─ Đánh giá thường xuyên / định kỳ (trường)
    │     └─ Ma trận × đặc tả × (TN 3 dạng + TL)
    │
    ├─ Thi tốt nghiệp THPT (Bộ)
    │     ├─ Văn: Đọc + Viết
    │     ├─ Toán & KHTN+Địa: 3 dạng thức
    │     ├─ Sử/GDKTPL/CN: MCQ + Đ/S
    │     ├─ Tin: MCQ + Đ/S có nhánh
    │     └─ Ngoại ngữ: 40 MCQ ngữ cảnh
    │
    └─ Thi địa phương (vào 10, chuyên…)
          └─ Sở quy định — đa dạng, thường TL nặng
```

Sản phẩm startup = **nằm giữa** định kỳ + thi thử theo chuẩn TN; không thay Bộ, không ôm hết Sở ngày đầu.

---

## 7. Việc cập nhật tài liệu này

- [ ] Mỗi năm đối chiếu lại phụ lục số câu QĐ Bộ (nếu có chỉnh).  
- [ ] Khi chọn môn mở rộng thứ 2: viết thêm 1 file `mon-<ten>.md` (topic seed + template JSON mô tả).  
- [ ] Giáo viên partner xác nhận tỷ lệ NB/TH/VD thực tế khi soạn bank.
