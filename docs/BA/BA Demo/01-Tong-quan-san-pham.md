# 01 — Tổng quan sản phẩm & định hướng core

## 1. Bài toán

Xây nền tảng **thi / luyện tập trực tuyến** cho học sinh phổ thông Việt Nam, lấy cảm hứng từ giao diện thi trên máy tính của Bộ GD&ĐT (Cục Quản lý chất lượng), nhưng **không cố thay kỳ thi chính thức của Bộ**.

Sản phẩm phục vụ:

| Phân khúc | Nhu cầu chính | Ai trả tiền |
|-----------|---------------|-------------|
| Học sinh / phụ huynh | Luyện đề chuẩn cấu trúc, thi thử, theo dõi tiến bộ | Cá nhân (gói tài khoản) |
| Giáo viên / trung tâm | [Ngân hàng câu hỏi](./11-Chu-thich.md#ngan-hang-cau-hoi) + **[sinh đề](./11-Chu-thich.md#sinh-de) theo [ma trận](./11-Chu-thich.md#ma-tran)** + tổ chức thi online | Trung tâm / giáo viên |
| Trung tâm / GV đa môn | Cùng engine cho các môn TN; đề trộn môn (ĐGNL-style) | Trung tâm / giáo viên |
| (Sau) Partner nội dung môn khó | Văn / Tin / CN hoặc white-label | Partner môn |

## 2. Core vs “râu ria” (đã thống nhất hướng từ chat nội bộ)

### Core (phải làm trước — quyết định sống còn)

1. **Ngân hàng câu hỏi** có gắn metadata (môn, lớp, [chủ đề](./11-Chu-thich.md#chu-de)/dạng bài, mức độ khó / [cấp độ tư duy](./11-Chu-thich.md#cap-do-tu-duy), [dạng thức](./11-Chu-thich.md#dang-thuc) câu hỏi).  
2. **Ma trận đề thi** → quy tắc “[bốc](./11-Chu-thich.md#sinh-de)” số lượng câu theo (dạng bài × mức độ × dạng thức…).  
3. **Sinh đề / [phiên bản đề](./11-Chu-thich.md#exam-version)** từ ma trận (random trong pool đủ điều kiện).  
4. **Thi trên máy** đủ dùng: đăng nhập phiên thi, đồng hồ, palette câu, lưu đáp án, chấm tự động (phần khách quan), xem điểm.  
5. **Luyện tập** tái sử dụng cùng ngân hàng / đề (UI có thể vui hơn sau).

### Không phải core (làm sau hoặc không làm ở MVP)

| Ý tưởng | Vì sao trì hoãn |
|---------|-----------------|
| AI phát hiện cầm điện thoại / gian lận camera | ML đắt, false positive cao, user trả tiền sẽ phản cảm; Bộ cũng chưa “cấm máy” kiểu Netflix |
| QR / chống chụp màn hình phức tạp | Chi phí >> giá trị giai đoạn đầu |
| Ranking / meme / gamification nặng | Chỉ có ý nghĩa khi đã có traffic và nội dung |
| Import PDF/Word → AI parse đề hoàn hảo | Khó về UX + chất lượng; làm sau bằng API key user |
| Pipeline riêng Văn / Tin / Công nghệ | Tự luận, nhánh đề, UX đặc thù — để ngỏ sau MVP |
| Audio nghe | Media pipeline P2+ |

**Nguyên tắc:** mọi feature phải trả lời được: *“Có giúp giáo viên tạo đề đúng ma trận / học sinh thi–luyện theo chuẩn đề thật không?”* Nếu không → backlog.

## 3. Demo Bộ GD&ĐT (tham chiếu UX, không copy pháp lý)

Ảnh trong `docs/Pictures/` mô tả flow thí sinh của phần mềm thi thử nghiệm:

1. **Đăng nhập** — mã thí sinh + mật khẩu + chọn [đợt thi](./11-Chu-thich.md#exam-campaign).  
2. **Dashboard** — thông tin thí sinh, hội đồng/điểm thi, danh sách môn → “Vào thi”.  
3. **Làm bài** — header (timer, tiến độ), vùng nội dung (có thể split: ngữ liệu trái / câu hỏi phải), palette câu dưới (đã làm / chưa làm).  
4. **Kết quả** — số câu đã trả lời + điểm /10.

**Ý nghĩa với sản phẩm mình:**

- Phần **thi chính thức / thi thử “chuẩn Bộ”**: UI nghiêm túc, ít phân tâm, giống vibe demo.  
- Phần **luyện tập**: được phép khác biệt (feedback nhanh, giải thích, meme — giai đoạn sau).  
- Phân tách rõ 2 mode giúp tránh nhầm: user trả tiền ≠ thí sinh bị “cấm thi” như Bộ.

> Lưu ý thời sự (2026): lộ trình **thi tốt nghiệp THPT trên máy tính 2027** bị chỉ đạo chưa thí điểm chính thức khi chưa đủ điều kiện; Bộ khuyến khích thử nghiệm ở kiểm tra thường xuyên / thi thử trước. Thị trường “làm quen thi máy + ngân hàng câu” vẫn còn chỗ, nhưng **không bán sản phẩm như “phần mềm thi Bộ”**.

## 4. Định dạng đề mục tiêu (giai đoạn 1)

**Phạm vi lớp (đã chốt):** phục vụ **cả lớp 10, 11, 12** (ôn TN + kiểm tra / luyện theo chương trình), không chỉ lớp 12.

Ưu tiên kỹ thuật giai đoạn 1: **đề trắc nghiệm theo cấu trúc TN THPT từ 2025** trên **nhiều môn** (Toán seed đủ 3 dạng; môn khác theo họ 2–3 phần / chỉ MCQ), cộng **đề trộn môn** kiểu ĐGNL, vì:

- Hầu hết môn TN chỉ vài dạng thức → cùng engine.  
- Chấm máy được → phù hợp team nhỏ.  
- Demo Bộ cũng là [CBT](./11-Chu-thich.md#cbt) trắc nghiệm.  
- GV chọn phần / môn linh hoạt; không bắt full đề Bộ mỗi lần.

**Chưa làm riêng đợt đầu:** Ngữ văn, Tin học, Công nghệ.  
Thi vào 10 (tự luận thuần) là **P2**; kiểm tra định kỳ dùng lại ma trận + dạng TN + (sau) tự luận. Chi tiết phạm vi: [06](./06-MVP-uu-tien-va-pham-vi.md), [07](./07-Mo-rong-nhieu-mon.md).

## 5. Mô hình kiếm tiền (sơ bộ)

1. Gói học sinh (tháng / kỳ / năm), có trial.  
2. Gói giáo viên / trung tâm (ngân hàng riêng, số học sinh, số kỳ thi).  
3. (Sau) White-label / nhượng quyền môn.

**Thời gian đầu (đã chốt):** bank còn nhỏ, user ít → **mở toàn bộ luyện/thi thử cho chất lượng trải nghiệm**, chưa siết paywall / giới hạn kho. Paywall bật sau khi có đủ nội dung + traffic.

Chi phí AI: **API key của user** khi cần parse đề — tránh burn vốn startup vào LLM.

## 6. Quyết định đã chốt

### 6.0. Phạm vi môn (2026-11-11)

- [x] **Đa môn ngay MVP** (engine + template); Toán seed sâu nhất.  
- [x] Hỗ trợ đề **trộn môn** (ĐGNL-style, trắc nghiệm).  
- [x] **Chưa làm riêng:** Ngữ văn, Tin học, Công nghệ (để ngỏ).  
- [x] Xáo thứ tự câu (theo khối stimulus) + xáo A–D.  
- [x] Audio / nghe: P2+.

### 6.1. Segment (2026-11-05)

- [x] **Cả lớp 10, 11, 12.**

### 6.2. Ngân hàng câu hỏi & phê duyệt

| Loại nội dung | Ai tạo | Vào đâu | Duyệt? |
|---------------|--------|---------|--------|
| Câu của GV / cá nhân | Giáo viên | Bank **cá nhân** (và/hoặc trung tâm nếu thuộc org) | Tự chịu trách nhiệm; dùng cho đề của họ |
| Câu đóng góp hệ thống | GV / editor | Chờ duyệt → **bank hệ thống** | **Bắt buộc** [ContentAdmin](./11-Chu-thich.md#content-admin) / người duyệt: đúng đề + đáp án |
| Đề do GV tạo | Giáo viên | Đề riêng của người đó (ma trận → ExamVersion) | Không cần duyệt hệ thống để dùng nội bộ |

Mỗi câu **lưu nguồn gốc** (`created_by`, thời điểm, org nếu có) để tham chiếu / audit — kể cả sau khi đã vào bank chung.

### 6.3. [Lớp sở hữu (ownership)](./11-Chu-thich.md#ownership-layer) — bảng động

Không hard-code 2–3 enum cố định. Dùng **bảng / danh mục layer sở hữu** có thể thêm mới, ví dụ seed:

| code (ví dụ) | Ý nghĩa |
|--------------|---------|
| `personal` | Chỉ chủ sở hữu (GV) |
| `center` | Trong phạm vi trung tâm / org |
| `system` | Bank / đề công khai trên nền tảng (sau duyệt) |
| `secret` | Đề mật / chưa công bố (thi thật trung tâm) |
| … | Thêm sau: `licensed`, `partner_pack`, … |

Gắn layer vào **câu hỏi** và/hoặc **đề (ExamVersion)** + rule ai được xem/dùng/thi. Chi tiết schema: cập nhật ở file 04/05 khi implement.

### 6.4. Free vs paywall

- [x] Đầu kỳ: **cho dùng rộng** (không giới hạn kho vì chưa có gì để giới hạn).  
- Paywall / gói bán: chốt sau khi bank đủ lớn.

### 6.5. “[Đề đóng gói](./11-Chu-thich.md#de-dong-goi)” là gì — và thi công bằng thế nào?

Hai khái niệm **không loại trừ nhau**:

| Khái niệm | Nghĩa trong BA | Học sinh thi thế nào |
|-----------|----------------|----------------------|
| **Sinh từ ma trận** | Random **một lần** theo [ô](./11-Chu-thich.md#o-ma-tran) ma trận → ra **một** `ExamVersion` (danh sách câu đã khóa) | Cả lớp / cả đợt mở **cùng link / cùng ExamVersion** → **cùng một đề** → công bằng |
| **Đề đóng gói (Fixed Exam)** | Đề đã cố định sẵn: GV soạn tay chọn từng câu, hoặc đề bán/đóng gói sẵn, hoặc bản đã sinh từ ma trận rồi **lưu lại** như sản phẩm | Cũng là một `ExamVersion` cố định + link |

**Trả lời đúng lo của bạn:** sinh ngẫu nhiên **không** có nghĩa mỗi học sinh một đề khác.  
Flow đúng:

```
Ma trận → Bốc 1 lần → Đặc tả/chỉnh → Khóa ExamVersion → Tạo link/đợt thi
→ Nhiều học sinh vào cùng ExamVersion (cùng đề)
```

Chỉ khi GV **cố ý** sinh thêm mã đề 2, 3… (nhiều ExamVersion từ cùng ma trận) thì mới có đề khác nhau — phục vụ chống quay cóp, không phải mặc định.

**Đề đóng gói** trong câu hỏi mở trước đây = có hỗ trợ thêm kênh “chọn/cố định câu sẵn / bán gói đề”, ngoài nút “sinh từ ma trận”. Cả hai đều kết thúc ở **ExamVersion + link dùng chung**.

- [x] Có hỗ trợ đề cố định / đóng gói (Fixed Exam).  
- [x] Đề sinh ma trận sau khi khóa = cũng là đề cố định để chia sẻ link thi chung.
