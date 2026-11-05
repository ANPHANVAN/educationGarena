# 06 — MVP, ưu tiên & phạm vi vốn hạn chế

Team: **2 dev (junior–middle) + 1 giáo viên**. Deadline nội bộ từng nhắc ~tháng 12 — tài liệu này giả định **MVP có thể demo được**, không phải sản phẩm hoàn chỉnh.

---

## 1. Mục tiêu MVP (định nghĩa “xong”)

Một giáo viên có thể:

1. Thêm câu hỏi Toán (MCQ, Đ/S **mức theo câu** + 4 ý cố định, trả lời ngắn) kèm chủ đề + mức độ.  
2. Tạo ma trận (template TN hoặc bảng chủ đề × mức), chọn COARSE/FINE.  
3. Sinh đề khi đủ tồn kho; báo thiếu nếu không đủ.  
4. Xem **đặc tả draft**, đổi câu/chỉnh YCCĐ, **khóa đề** rồi mở kỳ thi / luyện.  

Một học sinh có thể:

5. Đăng nhập → làm bài CBT tối giản (timer, palette, nộp bài).  
6. Nhận điểm đúng rule 3 phần; short answer **exact match**.

**Ngoài định nghĩa xong:** ranking, meme, AI PDF, chống gian lận ML, tự luận vào 10, đa môn, thanh toán phức tạp.

---

## 2. Backlog cắt lớp

### P0 — phải có

| Hạng mục | Ghi chú |
|----------|---------|
| Auth cơ bản (học sinh / giáo viên) | Email + password OK |
| CRUD câu hỏi 3 format + LaTeX; Đ/S mức theo câu | |
| Taxonomy seed L1 (+ L2 tối thiểu) | Xem file 10; GV chỉnh |
| Blueprint COARSE/FINE + sinh đề + tồn kho | Core |
| **Đặc tả draft → chỉnh → khóa đề** | Core (file 09) |
| Attempt + chấm MCQ / ĐS group / short exact | |
| Template `TN_THPT_TOAN_2025` scoring | |
| UI làm bài tối giản (demo Bộ) | |

### P1 — ngay sau khi P0 chạy

| Hạng mục | Ghi chú |
|----------|---------|
| Luyện tập chọn chủ đề × số câu | Tái dùng blueprint engine |
| Xem lại bài + lời giải | |
| Báo cáo đơn giản cho GV (điểm lớp) | |
| Import text template hàng loạt | |
| Gói trial / paywall thô | Đầu kỳ mở rộng; siết sau khi bank đủ |
| Tab blur warning (log) | Đủ “có chống gian lận nhẹ”; không ML |

### P2 — khi có user thật

| Hạng mục | |
|----------|--|
| Multi-tenant trung tâm | |
| AI parse PDF bằng API key user | |
| Ranking / badge / meme mode luyện | |
| Đề tự luận + xuất PDF | |
| Thống kê độ khó câu từ data | |
| App mobile native | Web responsive trước |

### Out of scope gần như chắc (năm đầu)

- Thị giác máy phát hiện điện thoại  
- Thi quốc gia quy mô Bộ (LAN đề án, cơ yếu…)  
- Nhượng quyền đa môn trước khi PMF Toán  

---

## 3. Kiến trúc — mức “đủ sống”, chưa SA nặng

Gợi ý cho junior–middle, vốn ít:

- **Monolith** hoặc modular monolith (API + Web).  
- DB quan hệ (Postgres).  
- Render math client-side.  
- Deploy 1 VPS / PaaS rẻ; object storage cho ảnh.  
- Không microservices, không Kafka, không tự host LLM.

Chỉ tách service khi có nút thắt thật (ví dụ chấm hàng loạt) — hiện chưa cần.

Chi tiết SA để tài liệu riêng sau khi BA chốt.

---

## 4. Kế hoạch nội dung (song song code)

Không có câu hỏi thì product chết dù code đẹp.

| Tuần | Nội dung |
|------|----------|
| 1–2 | Chốt taxonomy 40–80 chủ đề; nhập 50 câu mẫu đủ 3 format |
| 3–4 | Phủ bank để **ít nhất 1 đề TN full** sinh được + 2–3 chuyên đề luyện |
| 5–8 | Đẩy lên 300+ câu; ưu tiên chủ đề hay ra TN |

Dev viết tool nhập; **giáo viên là bottleneck chất lượng** — bảo vệ thời gian GV khỏi feature không core.

---

## 5. Rủi ro & giảm thiểu

| Rủi ro | Giảm thiểu |
|--------|------------|
| Ôm quá nhiều ý tưởng (chat Facebook) | Gate bằng doc 01 + 06; mọi PR phải map P0/P1 |
| Bank thiếu → sinh đề fail | Dashboard tồn kho; đừng marketing “đề vô hạn” sớm |
| Sai rule chấm Phần II | Unit test bảng điểm; GV verify bằng đề mẫu |
| Burn tiền AI | Không AI server-side trả phí team; API key user sau |
| Lộ đề trung tâm | Snapshot + phân quyền + (sau) watermark / rate limit |
| Nhầm tư cách “phần mềm Bộ” | Branding riêng; chỉ “thi thử theo cấu trúc…” |

---

## 6. Tiêu chí demo tháng 12 (gợi ý)

- [ ] Giáo viên tạo ma trận 2 chủ đề × 3 mức → sinh đề 15 câu.  
- [ ] Sinh 1 đề full TN THPT Toán (22 câu) từ template.  
- [ ] Học sinh làm hết → điểm khớp đáp án mẫu ±0 (trừ short tolerance đã chốt).  
- [ ] Ít nhất 1 luồng luyện tập khác UI thi (dù chỉ khác màu / hiện giải ngay).

Nếu trượt timeline: **cắt luyện tập UI**, giữ bank + matrix + 1 mode làm bài.
