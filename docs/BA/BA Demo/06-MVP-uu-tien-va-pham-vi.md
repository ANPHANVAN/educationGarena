# 06 — MVP, ưu tiên & phạm vi

Team: **2 dev (junior–middle) + 1 giáo viên**. Mục tiêu: **MVP demo được**, không phải sản phẩm hoàn chỉnh.

---

## 1. Định hướng đã chỉnh (tóm tắt)

| Quyết định | Nội dung |
|------------|----------|
| **Đa môn ngay MVP** | Không “chỉ Toán rồi mới mở”. Engine + template theo môn từ đầu. |
| **Trong đợt đầu** | Các môn TN trắc nghiệm quen thuộc: Toán, Lý, Hóa, Sinh, Địa, Sử, GDKTPL, Ngoại ngữ… |
| **Chưa làm riêng** | **Ngữ văn**, **Tin học**, **Công nghệ** — để ngỏ mở rộng (tự luận / nhánh đề / UX đặc thù). |
| **Đề ĐGNL** | Hỗ trợ tạo đề **trộn nhiều môn** (chủ yếu trắc nghiệm). |
| **Linh hoạt phần thi** | Chọn phần / môn / chủ đề đưa vào đề — không bắt full cấu trúc TN mỗi lần. |
| **Xáo đề** | Xáo thứ tự câu + xáo phương án A–D (giữ nguyên bundle stimulus). |

Toán vẫn là **môn seed nội dung + template đầy đủ nhất** (3 dạng); các môn khác tái dùng cùng engine, khác topic tree + score template.

---

## 2. Mục tiêu MVP (định nghĩa “xong”)

Một giáo viên có thể:

1. Thêm câu hỏi theo môn ([MCQ](./11-Chu-thich.md#mcq), [Đ/S](./11-Chu-thich.md#dung-sai) mức theo câu + 4 ý, [trả lời ngắn](./11-Chu-thich.md#tra-loi-ngan) khi môn có Phần III) kèm [chủ đề](./11-Chu-thich.md#chu-de) + [mức độ](./11-Chu-thich.md#cap-do-tu-duy).  
2. Tạo [ma trận](./11-Chu-thich.md#ma-tran) từ template kỳ (TN theo môn, kiểm tra, hoặc **đề trộn môn / ĐGNL-style**), chọn [COARSE](./11-Chu-thich.md#coarse)/[FINE](./11-Chu-thich.md#fine), chọn phần cần thi.  
3. [Sinh đề](./11-Chu-thich.md#sinh-de) khi đủ [tồn kho](./11-Chu-thich.md#ton-kho); báo thiếu nếu không đủ.  
4. Xem **[đặc tả](./11-Chu-thich.md#dac-ta-de) draft**, đổi câu/chỉnh [YCCĐ](./11-Chu-thich.md#yccd), bật xáo câu / xáo A–D, **[khóa đề](./11-Chu-thich.md#khoa-de)** rồi mở kỳ thi / luyện.

Một học sinh có thể:

5. Đăng nhập → làm bài [CBT](./11-Chu-thich.md#cbt) tối giản (timer, palette, nộp bài; layout 1 hoặc 2 cột khi có [stimulus](./11-Chu-thich.md#stimulus)).  
6. Nhận điểm đúng [score policy](./11-Chu-thich.md#score-policy) của template; short answer **[exact match](./11-Chu-thich.md#exact-match)**.

**Ngoài định nghĩa xong:** ranking, meme, AI PDF, chống gian lận ML, tự luận vào 10, audio nghe, pipeline riêng Văn/Tin/CN, thanh toán phức tạp.

---

## 3. Phạm vi môn & template

### Trong MVP (cùng engine)

| Họ cấu trúc | Môn | Format cần |
|-------------|-----|------------|
| 3 phần I+II+III | Toán, Lý, Hóa, Sinh, Địa | MCQ + Đ/S + Short |
| 2 phần I+II | Sử, GDKTPL | MCQ + Đ/S |
| Chỉ MCQ | Ngoại ngữ | MCQ (+ stimulus đọc hiểu) |
| Trộn môn | Đề ĐGNL / thi thử năng lực kiểu trắc nghiệm | Các format trên theo từng khối câu |

### Để ngỏ (không ưu tiên đợt đầu)

| Môn | Vì sao trì | Mở sau cần gì |
|-----|------------|---------------|
| **Ngữ văn** | Tự luận / rubric / chấm tay | ESSAY + workflow chấm |
| **Tin học** | Phần II có nhánh định hướng | Track trên blueprint + UX chọn nhánh |
| **Công nghệ** | Market hẹp hơn; cấu trúc gần Sử nhưng ít nhu cầu sớm | Template 2 phần + stimulus hình kỹ thuật |

Audio (nghe Anh / media): **P2+** — schema media sẵn chỗ gắn, chưa build player/pipeline.

---

## 4. Backlog cắt lớp

### P0 — phải có

| Hạng mục | Ghi chú |
|----------|---------|
| Auth cơ bản (học sinh / giáo viên) | Email + password OK |
| `subject_id` + CRUD câu 3 format + LaTeX; Đ/S mức theo câu | Không hard-code một môn |
| [Taxonomy](./11-Chu-thich.md#taxonomy) seed theo môn ([L1](./11-Chu-thich.md#l1) + [L2](./11-Chu-thich.md#l2) tối thiểu) | Toán xem file 10; môn khác seed mỏng OK |
| [Blueprint](./11-Chu-thich.md#ma-tran) COARSE/FINE + chọn phần + sinh đề + tồn kho | Core |
| Template scoring theo môn (vd. `TN_THPT_TOAN_2025`, `TN_THPT_LY_2025`…) | Config, không `if (math)` |
| Đề **trộn môn** (nhiều `subject` trong một blueprint) | ĐGNL-style / thi thử liên môn |
| **Đặc tả draft → chỉnh → khóa đề** | Core (file 09) |
| Xáo thứ tự câu + xáo A–D khi sinh / phát đề | Bundle stimulus không bị tách |
| [Attempt](./11-Chu-thich.md#attempt) + chấm MCQ / ĐS group / short exact | |
| UI làm bài tối giản (demo Bộ; 2 cột nếu có stimulus) | |

### P1 — ngay sau khi P0 chạy

| Hạng mục | Ghi chú |
|----------|---------|
| Luyện tập chọn môn / chủ đề × số câu | Tái dùng blueprint engine |
| Xem lại bài + lời giải | |
| Báo cáo đơn giản cho GV (điểm lớp) | |
| Import text template hàng loạt | |
| Gói trial / paywall thô | Siết sau khi bank đủ |
| Tab blur warning (log) | Chống gian lận nhẹ; không ML |
| Stimulus UX ổn cho đọc hiểu / bảng số liệu | Quan trọng Anh, Sử, Địa… |

### P2 — khi có user thật

| Hạng mục | |
|----------|--|
| Audio / nghe | |
| Mở riêng **Tin** (track), **Công nghệ**, **Văn** (essay) | |
| Multi-tenant trung tâm | |
| AI parse PDF bằng API key user | |
| Ranking / badge / meme mode luyện | |
| Đề tự luận + xuất PDF | |
| Thống kê độ khó câu từ data | |
| App mobile native | Web responsive trước |

### Out of scope gần như chắc (năm đầu)

- Thị giác máy phát hiện điện thoại  
- Thi quốc gia quy mô Bộ (LAN đề án, cơ yếu…)  
- Nhượng quyền thương mại đa partner trước khi có PMF  

---

## 5. Kiến trúc — mức “đủ sống”

- **Monolith** hoặc modular monolith (API + Web).  
- DB quan hệ (Postgres).  
- Render math client-side.  
- Deploy 1 VPS / PaaS rẻ; object storage cho ảnh / (sau) audio.  
- Không microservices, không Kafka, không tự host LLM.

Chi tiết SA để tài liệu riêng sau khi BA chốt.

---

## 6. Kế hoạch nội dung (song song code)

Không có câu hỏi thì product chết dù code đẹp.

| Tuần | Nội dung |
|------|----------|
| 1–2 | Chốt taxonomy Toán 40–80 chủ đề; nhập ~50 câu mẫu đủ 3 format; seed mỏng 1–2 môn khác (vd. Lý hoặc Anh) |
| 3–4 | Ít nhất **1 đề TN full Toán** + **1 đề trộn môn ngắn** (ĐGNL-style) sinh được |
| 5–8 | Đẩy bank theo môn có nhu cầu demo; ưu tiên chủ đề hay ra TN |

Dev viết tool nhập; **giáo viên là bottleneck chất lượng** — bảo vệ thời gian GV khỏi feature không core.

---

## 7. Rủi ro & giảm thiểu

| Rủi ro | Giảm thiểu |
|--------|------------|
| Ôm mọi môn + mọi UX đặc thù | Gate: chưa Văn/Tin/CN; audio sau; doc 01 + 06 |
| Bank mỏng trải nhiều môn | Seed sâu Toán; môn khác template + vài chục câu demo |
| Đề trộn môn thiếu tồn kho | Shortage report theo từng ô/môn |
| Sai rule chấm Phần II / điểm short khác môn | Unit test theo score policy template |
| Xáo câu làm vỡ stimulus | Xáo theo **khối** (bundle), không xáo lẻ câu trong cùng ngữ liệu |
| Burn tiền AI | Không AI server-side trả phí team |
| Nhầm tư cách “phần mềm Bộ” | Branding riêng; “thi thử theo cấu trúc…” |

---

## 8. Tiêu chí demo (gợi ý)

- [ ] GV tạo ma trận 2 chủ đề × 3 mức (một môn) → sinh đề ~15 câu.  
- [ ] Sinh 1 đề full TN Toán từ template.  
- [ ] Sinh 1 đề **trộn ≥2 môn** (ĐGNL-style) từ blueprint.  
- [ ] Bật xáo câu + xáo A–D; học sinh làm → điểm khớp đáp án mẫu.  
- [ ] Ít nhất 1 luồng luyện khác UI thi (dù chỉ khác màu / hiện giải ngay).

Nếu trượt timeline: **cắt luyện UI + thu hẹp số môn seed**, giữ engine đa môn + matrix + khóa đề + 1 mode làm bài.
