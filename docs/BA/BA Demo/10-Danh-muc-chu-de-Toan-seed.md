# 10 — Danh mục chủ đề Toán (seed) từ đề / ôn các năm

> **Mục đích:** seed `Topic` cho năm đầu. Không phải văn bản pháp quy — tổng hợp từ phân tích đề TN, tài liệu ôn, ma trận cộng đồng (MathVN, Toanmath, ma trận ôn 2024 kiểu 50 câu CT cũ, đề 2025+ CT 2018).  
> Giáo viên partner **được quyền sửa/gộp/tách** trước khi khóa [taxonomy](./11-Chu-thich.md#taxonomy) production.

Hai lớp tag:

- **[L1](./11-Chu-thich.md#l1) — [Chủ đề](./11-Chu-thich.md#chu-de) ([COARSE](./11-Chu-thich.md#coarse)):** dùng [ma trận](./11-Chu-thich.md#ma-tran) nhanh / báo cáo  
- **[L2](./11-Chu-thich.md#l2) — Dạng bài ([FINE](./11-Chu-thich.md#fine)):** khi user bật kiểm soát chi tiết  

---

## 1. Phân bố tham khảo đề TN cấu trúc mới (2025–2026)

Nguồn tổng hợp MathVN (phân tích đề chính thức, hướng 2026):

### Phần I — MCQ (12)

| Lớp | Chủ đề L1 | Số câu (mẫu) |
|-----|-----------|--------------|
| 11 | Lượng giác | 1 |
| 11 | Cấp số cộng – Cấp số nhân | 1 |
| 11 | Hình học không gian (thuần túy) | 2 |
| 11 | Hàm số mũ và logarit | 1 |
| 11 | Thống kê | 1 |
| 12 | Khảo sát hàm số (ứng dụng đạo hàm) | 1 |
| 12 | Nguyên hàm – Tích phân – Ứng dụng | 2 |
| 12 | Hình học Oxyz | 3 |

### Phần II — Đ/S (4 câu ≈ 16 ý)

| Lớp | Chủ đề L1 | Số câu group |
|-----|-----------|--------------|
| 12 | Khảo sát hàm số | 1 |
| 12 | Nguyên hàm – Tích phân – Ứng dụng | 1 |
| 12 | Hình học Oxyz | 1 |
| 12 | Xác suất có điều kiện | 1 |

### Phần III — Short (6)

| Lớp | Chủ đề L1 | Số câu |
|-----|-----------|--------|
| 10 | Hệ bất phương trình bậc nhất hai ẩn | 1 |
| 10 | Đại số tổ hợp | 1 |
| 11 | Xác suất cổ điển | 1 |
| 11 | Hình học không gian (thuần túy) | 1 |
| 12 | Khảo sát hàm số | 1 |
| 12 | Nguyên hàm – Tích phân – Ứng dụng | 1 |

> Template mặc định `TN_THPT_TOAN_2025` có thể embed phân bố này ở mode COARSE; từng năm admin cập nhật số liệu nếu đề thật lệch.

---

## 2. Chủ đề L1 đề xuất seed (gắn lớp gợi ý)

Mạch CT 2018: **Số–Đại số–Giải tích** | **Hình học–Đo lường** | **Thống kê–Xác suất**.

### Lớp 10 (hay gặp ôn / Phần III)

| code | Tên L1 | Mạch |
|------|--------|------|
| `m10_pt_bpt` | Phương trình & bất phương trình | Đại số |
| `m10_he_bpt_2an` | Hệ bất phương trình bậc nhất hai ẩn | Đại số |
| `m10_to_hop` | Đại số tổ hợp | Đại số |
| `m10_xs_co_dien` | Xác suất cổ điển (mở đầu) | XS |
| `m10_thong_ke` | Thống kê (mở đầu) | TK |
| `m10_luong_giac_cb` | Lượng giác cơ bản | Đại số |
| `m10_hh_phang` | Hình học phẳng | HH |
| `m10_hhkg_mo_dau` | Hình học không gian mở đầu | HH |

### Lớp 11

| code | Tên L1 | Mạch |
|------|--------|------|
| `m11_luong_giac` | Lượng giác | Đại số |
| `m11_day_so_csc_csn` | Dãy số – CSC – CSN | Đại số |
| `m11_gioi_han` | Giới hạn | Giải tích |
| `m11_mu_logarit` | Hàm số mũ và logarit | Giải tích |
| `m11_dao_ham` | Đạo hàm | Giải tích |
| `m11_hhkg_song_song` | HHKG — quan hệ song song | HH |
| `m11_hhkg_vuong_goc` | HHKG — quan hệ vuông góc / thuần túy | HH |
| `m11_thong_ke` | Thống kê | TK |
| `m11_xs_co_dien` | Xác suất cổ điển | XS |
| `m11_lt_do_thi` | Lý thuyết đồ thị *(chuyên đề — không bắt buộc mọi HS)* | Chuyên đề |

### Lớp 12

| code | Tên L1 | Mạch |
|------|--------|------|
| `m12_khao_sat_ham_so` | Ứng dụng đạo hàm / khảo sát hàm số | Giải tích |
| `m12_nguyen_ham_tich_phan` | Nguyên hàm – Tích phân – Ứng dụng | Giải tích |
| `m12_oxyz` | Hình học tọa độ Oxyz | HH |
| `m12_xs_co_dk` | Xác suất có điều kiện | XS |
| `m12_thong_ke_nang` | Thống kê (số đặc trưng / nâng) | TK |
| `m12_toan_thuc_te` | Toán thực tế / tối ưu *(tag ngang hoặc L1 tùy GV)* | Liên mạch |

### CT cũ / ít còn trong TN 2018 (giữ optional, không seed mặc định bắt buộc)

`so_phuc`, `khoi_da_dien`, `khoi_tron_xoay` — còn trong bank ôn đề cũ 2024 (50 câu); đánh dấu `curriculum=CT2006_legacy` để không lẫn ma trận 2018.

---

## 3. Dạng bài L2 mẫu (FINE) — vài chủ đề hay ra

### `m12_khao_sat_ham_so`

- Đơn điệu  
- Cực trị  
- GTLN – GTNN  
- Tiệm cận  
- Đồ thị & điểm đặc biệt  
- Tiếp tuyến / tiếp xúc  
- Tương giao đồ thị  
- Bài toán thực tế gắn hàm số  

### `m12_nguyen_ham_tich_phan`

- Nguyên hàm cơ bản  
- Tích phân xác định  
- Diện tích hình phẳng  
- Thể tích khối quay  
- Ứng dụng thực tế tích phân  

### `m12_oxyz`

- Vectơ & tọa độ điểm  
- Phương trình mặt phẳng  
- Phương trình đường thẳng  
- Mặt cầu  
- Góc – khoảng cách  
- Min/max / thực tế Oxyz  

### `m11_mu_logarit` / tổ hợp / XS

- Phương trình – bất phương trình mũ/log  
- Tổ hợp đếm / nhị thức  
- XS cổ điển / XS có điều kiện / bảng phân phối  

*(GV bổ sung L2 khi bật FINE; MVP có thể chỉ seed L2 cho 3 chủ đề lớp 12 nặng nhất.)*

---

## 4. Gợi ý từ ma trận ôn đề cũ 2024 (50 MCQ) — chỉ tham khảo lịch sử

Chương hay xuất hiện trước 2025: Ứng dụng đạo hàm, Mũ–logarit, Số phức, Nguyên hàm–tích phân, Khối đa diện, Khối tròn xoay, Oxyz, Tổ hợp–XS, Quan hệ vuông góc…  
Dùng để hiểu **thói quen phân loại của GV**, không copy số câu vào template 2025+.

---

## 5. Quy tắc dùng trong hệ thống

1. Mỗi [`QuestionItem`](./11-Chu-thich.md#question-item) gắn **≥1 topic L1**; L2 optional (bắt buộc nếu blueprint FINE yêu cầu).  
2. Template TN mặc định filter **L1 + mức + format/phần**.  
3. Đổi danh mục: versioning `Topic.taxonomy_version` — đề đã [snapshot](./11-Chu-thich.md#snapshot) không đổi tên topic cũ.  
4. Chuyên đề không bắt buộc (đồ thị, …): flag `elective=true` — ma trận chuẩn Bộ mặc định **không** bắt buộc ô này trừ khi GV bật.
