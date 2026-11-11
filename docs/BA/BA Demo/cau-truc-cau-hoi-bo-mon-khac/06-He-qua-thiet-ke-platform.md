# 06 — Hệ quả thiết kế platform (sau khi nhìn toàn ngành)

Tài liệu này trả lời: *Biết cấu trúc các môn rồi thì BA/dev phải giữ nguyên tắc gì?*

---

## 1. Một engine — nhiều template

Đừng viết `MathExamService`. Hãy có:

| Lớp | Ví dụ |
|-----|--------|
| [`ItemFormat`](../11-Chu-thich.md#dang-thuc) | [MCQ_SINGLE](../11-Chu-thich.md#mcq), [TRUE_FALSE_GROUP](../11-Chu-thich.md#dung-sai), [SHORT_ANSWER](../11-Chu-thich.md#tra-loi-ngan), ESSAY, (ORDERING…) |
| [`ScorePolicy`](../11-Chu-thich.md#score-policy) | `tn_thpt_toan_2025`, `tn_thpt_ly_2025`, `tn_thpt_anh_2025`, `school_mix_70_30` |
| [`BlueprintTemplate`](../11-Chu-thich.md#blueprint-template) | Số câu từng phần + filter + track (Tin) |
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
| [Stimulus](../11-Chu-thich.md#stimulus) dùng chung | hữu ích | **rất cần** | **rất cần** | cần | **bắt buộc** | **bắt buộc** |
| Track / nhánh đề | — | — | — | **có** | — | — |
| LaTeX | ✓ | ✓ | ít | ít | — | — |
| Code block | — | — | — | ✓ | — | — |
| Bản đồ / Atlat UX | — | Địa | Sử (lược đồ) | — | — | — |

**Engine 3 dạng + stimulus cover phần lớn môn TN.** Đợt đầu **chưa** làm cột Tin (track) / Văn (essay) / CN. Stimulus UX cần sớm cho Anh–Sử–Địa; audio sau.

---

## 3. [Ma trận](../11-Chu-thich.md#ma-tran) vẫn là ngôn ngữ chung của ngành

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

## 4. Phạm vi môn (khớp BA Demo 06/07)

**MVP (cùng engine, Toán seed sâu):** Toán, Lý, Hóa, Sinh, Địa, Sử, GDKTPL, Ngoại ngữ + đề **trộn môn** (ĐGNL-style).  
Bank thực tế có thể mỏng ở môn phụ — quan trọng là **template + subject_id**, không phải đủ bank mọi môn ngày đầu.

| Để ngỏ | Lý do trì | Khi mở cần thêm |
|--------|-----------|-----------------|
| **Tin** | Nhánh đề Phần II | Track trên blueprint + code render |
| **Công nghệ** | Nhu cầu hẹp hơn sớm | Template 2 phần + stimulus kỹ thuật |
| **Văn** | Tự luận / chấm tay | ESSAY + workflow chấm |

Audio = P2+. Chi tiết cắt lớp: [../06-MVP-uu-tien-va-pham-vi.md](../06-MVP-uu-tien-va-pham-vi.md).

---

## 5. Cạm bẫy khi “nhìn toàn ngành”

1. **Ôm UX đặc thù mọi môn** (Văn/Tin/CN/audio) ngay → loãng vốn. Đa môn TN OK; đặc thù để ngỏ.  
2. **Hard-code điểm short 0,5** → gãy Lý/Hóa.  
3. **Không có Stimulus / xáo làm vỡ bundle** → Anh/Sử/Địa và Đ/S thí nghiệm hỏng.  
4. **Coi Đ/S như 4 MCQ độc lập khi chấm** → sai mọi môn có Phần II.  
5. **Làm Văn sớm vì “ai cũng học Văn”** → kẹt chấm bài.  
6. **Bỏ qua kiểm tra định kỳ / chọn phần linh hoạt** — tần suất GV quanh năm; TN chỉ mùa cao điểm.  
7. **Nhầm L1/L2 với loại kỳ thi** — L1/L2 là cây chủ đề trong môn; nhiều dạng đề = nhiều template.

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
