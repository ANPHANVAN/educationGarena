# 01 — Tổng quan sản phẩm & định hướng core

## 1. Bài toán

Xây nền tảng **thi / luyện tập trực tuyến** cho học sinh phổ thông Việt Nam, lấy cảm hứng từ giao diện thi trên máy tính của Bộ GD&ĐT (Cục Quản lý chất lượng), nhưng **không cố thay kỳ thi chính thức của Bộ**.

Sản phẩm phục vụ:

| Phân khúc | Nhu cầu chính | Ai trả tiền |
|-----------|---------------|-------------|
| Học sinh / phụ huynh | Luyện đề chuẩn cấu trúc, thi thử, theo dõi tiến bộ | Cá nhân (gói tài khoản) |
| Giáo viên / trung tâm | Ngân hàng câu hỏi + **sinh đề theo ma trận** + tổ chức thi online | Trung tâm / giáo viên |
| (Sau) Nhượng quyền môn khác | Cùng mô hình cho Lý, Hóa, Anh… | Partner môn |

## 2. Core vs “râu ria” (đã thống nhất hướng từ chat nội bộ)

### Core (phải làm trước — quyết định sống còn)

1. **Ngân hàng câu hỏi** có gắn metadata (môn, lớp, chủ đề/dạng bài, mức độ khó / cấp độ tư duy, dạng thức câu hỏi).  
2. **Ma trận đề thi** → quy tắc “bốc” số lượng câu theo (dạng bài × mức độ × dạng thức…).  
3. **Sinh đề / phiên bản đề** từ ma trận (random trong pool đủ điều kiện).  
4. **Thi trên máy** đủ dùng: đăng nhập phiên thi, đồng hồ, palette câu, lưu đáp án, chấm tự động (phần khách quan), xem điểm.  
5. **Luyện tập** tái sử dụng cùng ngân hàng / đề (UI có thể vui hơn sau).

### Không phải core (làm sau hoặc không làm ở MVP)

| Ý tưởng | Vì sao trì hoãn |
|---------|-----------------|
| AI phát hiện cầm điện thoại / gian lận camera | ML đắt, false positive cao, user trả tiền sẽ phản cảm; Bộ cũng chưa “cấm máy” kiểu Netflix |
| QR / chống chụp màn hình phức tạp | Chi phí >> giá trị giai đoạn đầu |
| Ranking / meme / gamification nặng | Chỉ có ý nghĩa khi đã có traffic và nội dung |
| Import PDF/Word → AI parse đề hoàn hảo | Khó về UX + chất lượng; làm sau bằng API key user |
| Nhượng quyền đa môn | Chỉ khi core Toán đã chạy và có doanh thu |

**Nguyên tắc:** mọi feature phải trả lời được: *“Có giúp giáo viên tạo đề đúng ma trận / học sinh thi–luyện theo chuẩn đề thật không?”* Nếu không → backlog.

## 3. Demo Bộ GD&ĐT (tham chiếu UX, không copy pháp lý)

Ảnh trong `docs/Pictures/` mô tả flow thí sinh của phần mềm thi thử nghiệm:

1. **Đăng nhập** — mã thí sinh + mật khẩu + chọn đợt thi.  
2. **Dashboard** — thông tin thí sinh, hội đồng/điểm thi, danh sách môn → “Vào thi”.  
3. **Làm bài** — header (timer, tiến độ), vùng nội dung (có thể split: ngữ liệu trái / câu hỏi phải), palette câu dưới (đã làm / chưa làm).  
4. **Kết quả** — số câu đã trả lời + điểm /10.

**Ý nghĩa với sản phẩm mình:**

- Phần **thi chính thức / thi thử “chuẩn Bộ”**: UI nghiêm túc, ít phân tâm, giống vibe demo.  
- Phần **luyện tập**: được phép khác biệt (feedback nhanh, giải thích, meme — giai đoạn sau).  
- Phân tách rõ 2 mode giúp tránh nhầm: user trả tiền ≠ thí sinh bị “cấm thi” như Bộ.

> Lưu ý thời sự (2026): lộ trình **thi tốt nghiệp THPT trên máy tính 2027** bị chỉ đạo chưa thí điểm chính thức khi chưa đủ điều kiện; Bộ khuyến khích thử nghiệm ở kiểm tra thường xuyên / thi thử trước. Thị trường “làm quen thi máy + ngân hàng câu” vẫn còn chỗ, nhưng **không bán sản phẩm như “phần mềm thi Bộ”**.

## 4. Định dạng đề mục tiêu (giai đoạn 1)

Ưu tiên **đề trắc nghiệm theo cấu trúc tốt nghiệp THPT từ 2025** (Toán: 3 dạng thức), vì:

- Chuẩn quốc gia, học sinh lớp 12 (và ôn sớm lớp 10–11) có nhu cầu rõ.  
- Chấm máy được → phù hợp team nhỏ.  
- Demo Bộ cũng là CBT trắc nghiệm.

Thi vào 10 (tự luận) và kiểm tra định kỳ nhà trường (trộn TN + TL) là **mở rộng schema**, không phải MVP đầu.

## 5. Mô hình kiếm tiền (sơ bộ — chưa chốt giá)

1. Gói học sinh (tháng / kỳ / năm), có trial.  
2. Gói giáo viên / trung tâm (ngân hàng riêng, số học sinh, số kỳ thi).  
3. (Sau) White-label / nhượng quyền môn.

Chi phí AI: **API key của user** khi cần parse đề — tránh burn vốn startup vào LLM.

## 6. Câu hỏi còn mở (cần giáo viên + founder chốt)

- [ ] Segment đầu tiên: chỉ lớp 12 ôn TN THPT, hay cả 10–11 kiểm tra định kỳ?  
- [ ] Ai sở hữu câu hỏi: chỉ team + giáo viên partner, hay cho GV upload riêng (tenant)?  
- [ ] Luyện tập free một phần hay toàn bộ sau paywall?  
- [ ] Có bán “đề đóng gói” (fixed exam) ngoài sinh ngẫu nhiên từ ma trận không?
