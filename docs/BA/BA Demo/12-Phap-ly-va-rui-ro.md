# 12 — Pháp lý & rủi ro (checklist ngắn)

> Không thay thế tư vấn luật sư. Chỉ để team nhớ **không làm gì / phải làm gì** trước khi thu tiền.  
> Ngày: 2026-11-11

## Nguyên tắc 1 dòng

**Không mạo danh Bộ · Không scrap đề · Không lỏng dữ liệu học sinh · Có giấy tờ khi bán.**

---

## Cấm tuyệt đối

| Việc | Vì sao |
|------|--------|
| Quảng cáo “phần mềm thi Bộ”, logo Bộ, “đề/đáp án thật”, “cam kết điểm / đỗ” | Quảng cáo sai sự thật / gây nhầm cơ quan nhà nước |
| Scrape / copy bank từ Moon, Tuyensinh247, VietJack, PDF trường, sách NXB rồi bán | Bản quyền — chỗ vibe-edtech hay “bế” nhất |
| Đưa đề mật (`secret`) của trung tâm ra public trước giờ thi | Lộ đề + mất trust + trách nhiệm hợp đồng |
| Bán / chia sẻ dữ liệu học sinh (điểm, SĐT, lớp) | Luật bảo vệ dữ liệu cá nhân |
| Camera / sinh trắc chống gian lận ở MVP | Dữ liệu nhạy cảm; chưa đủ năng lực tuân thủ |

---

## Phải làm (theo giai đoạn)

### Trước khi public demo (chưa thu tiền)

- [ ] Footer ghi rõ: sản phẩm **luyện / thi thử độc lập**, **không** thuộc Bộ GD&ĐT.  
- [ ] ToS upload: GV tự chịu trách nhiệm bản quyền câu họ nhập.  
- [ ] Bank hệ thống chỉ nhận câu **tự soạn / có nguồn hợp pháp** + duyệt [ContentAdmin](./11-Chu-thich.md#content-admin).  
- [ ] Mỗi câu lưu `created_by` + nguồn (đã có trong [01](./01-Tong-quan-san-pham.md)).  
- [ ] Có kênh báo cáo / gỡ nội dung vi phạm (notice & takedown).

### Trước khi thu tiền (gói HS / GV)

- [ ] Đăng ký HKD hoặc DN + ngành nghề phù hợp.  
- [ ] Thông báo website TMĐT bán hàng tại [online.gov.vn](https://online.gov.vn).  
- [ ] Công khai: tên pháp lý, MST, địa chỉ, hotline/email khiếu nại.  
- [ ] Trang: Điều khoản · Chính sách bảo mật · Hoàn tiền / hủy gói.  
- [ ] Tài khoản học sinh: xin **đồng ý phụ huynh** (đối tượng lớp 10–12 = trẻ em theo NĐ 13 / Luật BVDLCN).  
- [ ] Chỉ thu dữ liệu cần thiết (không bắt CCCD nếu chỉ luyện đề).

### Khi có trung tâm / white-label

- [ ] Hợp đồng rõ quyền nội dung + bảo mật đề `secret`.  
- [ ] Kiểm tra lại: bán hàng của mình = **thông báo**; cho nhiều bên bán = có thể phải **đăng ký sàn**.

---

## Ưu tiên rủi ro (cho sản phẩm này)

1. **Bản quyền ngân hàng câu** — cao nhất.  
2. **Dữ liệu học sinh / phụ huynh** — cao.  
3. **Marketing gắn “Bộ / đề thật”** — cao khi mùa thi.  
4. **Thủ tục TMĐT + thuế** — trung bình, bắt buộc khi bán.  
5. **Code vibe / license OSS** — thấp hơn nhưng vẫn scan trước production.

---

## Định vị marketing an toàn

| Được nói | Không nói |
|----------|-----------|
| Luyện / thi thử theo **cấu trúc** đề phổ biến | “Phần mềm thi chính thức của Bộ” |
| UI học theo vibe CBT trên máy | “Có đề thi / đáp án Bộ năm nay” |
| Ngân hàng do đội ngũ / GV soạn, đã duyệt | “Cam kết điểm thi tốt nghiệp / đỗ ĐH” |

Chi tiết định hướng sản phẩm: [01 — Tổng quan](./01-Tong-quan-san-pham.md) mục 3.

---

## Việc team cần chốt thêm (legal backlog)

1. Bản disclaimer 2–3 câu gắn footer + trang đăng ký.  
2. Checkbox “Tôi là phụ huynh / đã được phụ huynh đồng ý”.  
3. Form báo cáo bản quyền + SLA gỡ (vd. 24–72h).  
4. 1 buổi hỏi luật sư trước khi bật paywall quy mô.
