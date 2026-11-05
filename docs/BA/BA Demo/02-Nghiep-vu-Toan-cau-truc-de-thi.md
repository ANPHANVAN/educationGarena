# 02 — Nghiệp vụ Toán & cấu trúc đề thi thực tế

Tài liệu này tổng hợp logic ngành Toán phổ thông Việt Nam (CT GDPT 2018) để team dev hiểu **vì sao ma trận đề phải có những trục phân loại nào**. Giáo viên partner cần review lại số liệu/tỷ lệ trước khi “chốt BA”.

---

## 1. Ba lớp khái niệm dễ bị lẫn (bắt buộc tách trong hệ thống)

| Khái niệm | Tiếng Việt thường gặp | Dùng để làm gì | Ví dụ Toán |
|-----------|----------------------|----------------|------------|
| **Đơn vị kiến thức / chủ đề** | chuyên đề, chương, dạng bài | “Bốc câu thuộc phần nào” | Khảo sát hàm số; Tích phân; Oxyz |
| **Cấp độ tư duy / mức độ** | nhận biết, thông hiểu, vận dụng, (vận dụng cao) | “Khó dễ theo Bloom/VN” | Câu NB vs câu VD |
| **Dạng thức câu hỏi** | trắc nghiệm 4 lựa chọn, đúng/sai, trả lời ngắn, tự luận | “UI + cách chấm” | Phần I / II / III đề TN THPT |

Ngoài ra, CT 2018 còn trục **năng lực toán học** (dùng trong bảng NL–CĐT của Bộ):

1. Tư duy và lập luận toán học (TD)  
2. Giải quyết vấn đề toán học (GQ)  
3. Mô hình hóa toán học (MH)  
4. (Trong chương trình còn giao tiếp toán học, sử dụng công cụ… — đề tốt nghiệp thường nhấn 3 năng lực trên)

**Khuyến nghị MVP:** bắt buộc gắn câu hỏi với **(chủ đề + cấp độ tư duy + dạng thức)**. Trường `năng lực` để optional — giáo viên gắn sau khi quen hệ thống.

---

## 2. Cấp độ tư duy (mức độ khó) — chuẩn nhà trường VN

Trong kiểm tra định kỳ (giữa kỳ / cuối kỳ), giáo viên quen dùng **4 mức**:

| Mã | Tên | Ý nghĩa nghiệp vụ (tóm tắt) | Thường xuất hiện ở |
|----|-----|----------------------------|--------------------|
| NB | Nhận biết | Nhớ định nghĩa, công thức, nhận dạng đối tượng | TN nhiều lựa chọn |
| TH | Thông hiểu | Giải thích, chuyển đổi biểu diễn, tính toán chuẩn | TN, đúng/sai ý dễ |
| VD | Vận dụng | Áp dụng vào tình huống quen / bài toán có quy trình | Đúng/sai ý khó, trả lời ngắn, tự luận |
| VDC | Vận dụng cao | Tình huống mới, liên kết nhiều kiến thức, phân hóa điểm cao | Trả lời ngắn khó, tự luận cuối |

> **Lưu ý đề TN THPT từ 2025:** bảng chính thức của Bộ thường ghi **3 mức: Biết – Hiểu – Vận dụng** (gộp VDC vào nhóm vận dụng hoặc thể hiện qua độ khó câu Phần III). Trên thị trường ôn thi, giáo viên vẫn hay gọi “vận dụng cao” cho câu phân hóa.  
> **Hệ thống nên hỗ trợ 4 mức** (NB/TH/VD/VDC); template ma trận “chuẩn Bộ” map VDC ⊂ VD nếu cần báo cáo 3 mức.

---

## 3. Kỳ thi tốt nghiệp THPT môn Toán (từ 2025) — neo chuẩn chính

### 3.1. Thông số chính thức / thực tế đã áp dụng

| Hạng mục | Giá trị |
|----------|---------|
| Thời gian | 90 phút |
| Hình thức | Trắc nghiệm khách quan (giấy hiện tại; CBT là hướng tổ chức sau) |
| Số câu hỏi | **22 câu** |
| Số lệnh hỏi (ý) | **34 ý** (vì 4 câu đúng/sai × 4 ý) |
| Thang điểm | 10 |

### 3.2. Ba dạng thức (Phần I–II–III)

#### Phần I — Trắc nghiệm nhiều phương án lựa chọn (MCQ)

- **12 câu**, mỗi câu 4 phương án A/B/C/D, chọn 1.  
- Mức độ điển hình: **Nhận biết – Thông hiểu**.  
- Điểm: **0,25 / câu đúng** → tối đa **3,0 điểm**.

#### Phần II — Trắc nghiệm Đúng / Sai

- **4 câu**, mỗi câu **4 ý** (a,b,c,d); mỗi ý chọn Đúng hoặc Sai.  
- Mức độ điển hình: **Thông hiểu – Vận dụng** (các ý trong cùng câu có thể lệch mức).  
- Cách tính điểm **theo số ý đúng trong cùng 1 câu** (không chia đều 0,25 như cũ):

| Số ý đúng trong 1 câu | Điểm |
|----------------------|------|
| 1 | 0,1 |
| 2 | 0,25 |
| 3 | 0,5 |
| 4 | 1,0 |

→ Tối đa Phần II: **4,0 điểm**.  
→ Xác suất đoán đúng cả 4 ý = 1/16 — đúng mục tiêu phân hóa của Bộ.

#### Phần III — Trả lời ngắn (short answer)

- **6 câu**; thí sinh điền kết quả (số / biểu thức ngắn theo quy ước đề).  
- Mức độ điển hình: **Vận dụng (– vận dụng cao)**.  
- Điểm Toán: **0,5 / câu đúng** → tối đa **3,0 điểm**.  
  (Các môn khác thường 0,25/câu — đừng hard-code 0,5 cho mọi môn.)

### 3.3. Ma trận chủ đề tham khảo (phân tích đề chính thức / ôn thi — có thể lệch từng năm)

Nguồn tổng hợp cộng đồng (MathVN, phân tích đề 2025–2026) — **không phải văn bản pháp quy**, dùng để seed taxonomy:

**Phần I (12 MCQ)** — ví dụ phân bố:

| Lớp | Chủ đề | Số câu (mẫu) |
|-----|--------|--------------|
| 11 | Lượng giác | 1 |
| 11 | Cấp số cộng – Cấp số nhân | 1 |
| 11 | Hình học không gian (thuần túy) | 2 |
| 11 | Hàm số mũ và logarit | 1 |
| 11 | Thống kê | 1 |
| 12 | Khảo sát hàm số | 1 |
| 12 | Nguyên hàm – Tích phân – Ứng dụng | 2 |
| 12 | Hình học Oxyz | 3 |

**Phần II (4 câu Đ/S)** — thường nặng lớp 12: khảo sát hàm số, tích phân, Oxyz, xác suất có điều kiện.

**Phần III (6 trả lời ngắn)** — trải lớp 10–12: bất PT bậc nhất 2 ẩn, tổ hợp, xác suất cổ điển, HHKG, hàm số, tích phân…

**Tỷ lệ kiến thức thường được nhắc:** ~30% lớp 11 + ~70% lớp 12 (có lẫn lớp 10 ở Phần III).  
**Tỷ lệ cấp độ (nhận định đề 2025):** khoảng **40% biết / 30% hiểu / 30% vận dụng** theo ý hỏi — phục vụ tốt nghiệp + vẫn phân hóa ĐH.

### 3.4. Hệ quả cho phần mềm

1. Một “câu” Phần II là **QuestionGroup** chứa 4 **Item** (ý) — chấm theo rule bảng điểm, không chấm 4 câu độc lập rồi cộng.  
2. Phần III cần schema **đáp án chuẩn hóa** (số thập phân, sai số chấp nhận?, nhiều đáp án tương đương?).  
3. Ma trận “chuẩn TN THPT Toán” là **template cố định 3 phần** + các ô (chủ đề × mức × dạng thức) quy định số lượng.

---

## 4. Kiểm tra định kỳ lớp 10, 11, 12 (giữa kỳ / cuối kỳ)

Đây là nhu cầu **hàng ngày của giáo viên / trung tâm**, khác đề TN:

- Thời lượng thường 45–90 phút tùy nhà trường.  
- Có thể **trộn trắc nghiệm + tự luận**.  
- Bắt buộc có **ma trận + đặc tả đề** theo hướng dẫn tập huấn của ngành (Thông tư đánh giá + tài liệu xây dựng đề theo ma trận).

### Cấu trúc ma trận nhà trường (mô hình phổ biến)

Hàng = **nội dung / chủ đề** (theo chương đang học).  
Cột = **cấp độ tư duy** (NB / TH / VD / VDC) × đôi khi tách thêm cột **hình thức** (TN / TL).  
Ô = số câu + điểm.

Ví dụ logic (minh họa, không phải đề thật):

| Chủ đề | NB | TH | VD | VDC | Tổng câu | Tổng điểm |
|--------|----|----|----|-----|----------|-----------|
| Hàm số mũ – logarit | 2 | 2 | 1 | 0 | 5 | … |
| Xác suất | 1 | 1 | 1 | 0 | 3 | … |
| … | | | | | | |

**Đặc tả đề** = bản “dịch” ma trận ra yêu cầu từng câu (câu số mấy, kiểm tra kỹ năng gì, đáp án kỳ vọng). Hệ thống MVP có thể chưa sinh đặc tả tự động; chỉ cần ma trận + danh sách câu đã bốc.

### Taxonomy chủ đề theo lớp (seed — giáo viên chỉnh)

**Lớp 10 (mạch chính CT 2018):** mệnh đề – tập hợp; hàm số & đồ thị; phương trình – bất phương trình; hệ PT; lượng giác cơ bản; vectơ – tích vô hướng (tùy SGK); thống kê – xác suất mở đầu; hình học phẳng / không gian mở đầu…

**Lớp 11:** lượng giác; dãy số – CSC – CSN; tổ hợp – xác suất; hàm mũ – logarit; hình học không gian (đường thẳng – mặt phẳng – khối); giới hạn – liên tục – đạo hàm (tùy phân phối)…

**Lớp 12:** ứng dụng đạo hàm / khảo sát hàm số; mũ – log (ôn); nguyên hàm – tích phân; số phức (nếu còn trong phân phối địa phương); hình học Oxyz; xác suất nâng cao; chuyên đề học tập (đồ thị, … — không phải HS nào cũng học).

> Hệ thống **không hard-code** danh sách chủ đề vào code business. Chủ đề là dữ liệu cấu hình theo `Subject + Grade + CurriculumVersion`.

---

## 5. Thi tuyển sinh vào lớp 10 môn Toán

Khác hẳn TN THPT: **đa số địa phương vẫn tự luận**, cấu trúc do **Sở** quy định.

| Địa phương (ví dụ) | Hình thức | Gợi ý cấu trúc |
|--------------------|-----------|----------------|
| Hà Nội | Tự luận, ~120 phút, ~5 bài | 3 mạch: Số–Đại số; Hình học–Đo lường; Thống kê–Xác suất. Điểm NL mẫu: TD 3đ, GQ 4,5đ, MH 2,5đ |
| TP.HCM | Tự luận, 7 bài | Hàm bậc 2; PT bậc 2 / Viète; thống kê–XS; bài thực tế; hình học; hệ PT; hình học phẳng chứng minh. Tỷ lệ mẫu: HH 45%, ĐS 40%, TK–XS 15% |

**Hệ quả sản phẩm:**

- Chấm tự luận = chấm tay / bán tự động → **không phải MVP CBT chấm máy**.  
- Có thể hỗ trợ sau: ngân hàng câu tự luận + ma trận + xuất PDF đề giấy.  
- Đừng thiết kế DB chỉ cho MCQ rồi kẹt khi mở vào 10.

---

## 6. Các “dạng đề” sản phẩm nên hỗ trợ bằng template

Không chỉ một loại ma trận. Nên có **ExamBlueprintTemplate**:

| Template code | Mô tả | Ưu tiên |
|---------------|-------|---------|
| `TN_THPT_TOAN_2025` | 12 MCQ + 4 Đ/S×4 + 6 short; scoring chuẩn | P0 |
| `SCHOOL_PERIODIC_TOAN` | Ma trận tự do NB/TH/VD/VDC theo chủ đề; thời gian tùy chỉnh | P1 |
| `PRACTICE_TOPIC_DRILL` | Luyện theo 1–n chủ đề, chọn số câu × mức | P0 (luyện tập) |
| `GRADE10_ENTRANCE_*` | Theo Sở — tự luận | P2+ |

User “bốc câu” = chọn template hoặc tự tạo ma trận → hệ thống lấy ngẫu nhiên từ pool thỏa điều kiện từng ô.

---

## 7. Điểm khác biệt nghiệp vụ Toán so với môn khác (để nhớ khi code)

- Công thức: **LaTeX** gần như bắt buộc.  
- Hình vẽ (HHKG, đồ thị): ảnh hoặc SVG; câu có thể phụ thuộc hình chung (stimulus).  
- Phần III: quy ước làm tròn **ghi trong stem**; chấm **khớp đúng** key (xem [09](./09-Dac-ta-de-va-quy-tac-da-chot.md)).  
- Câu Đ/S: **mức độ gắn cả câu**; 4 ý cố định trong câu (xem [09](./09-Dac-ta-de-va-quy-tac-da-chot.md) §5).

---

## 8. Quyết định đã chốt (2026-11-04) — không còn “chờ xác nhận”

Chi tiết đầy đủ: **[09-Dac-ta-de-va-quy-tac-da-chot.md](./09-Dac-ta-de-va-quy-tac-da-chot.md)** · danh mục seed: **[10-Danh-muc-chu-de-Toan-seed.md](./10-Danh-muc-chu-de-Toan-seed.md)**.

| # | Câu hỏi cũ | Quyết định |
|---|------------|------------|
| 1 | Danh mục chủ đề? | Seed L1/L2 theo đề & ôn các năm (file 10); GV được chỉnh trước production |
| 2 | VDC riêng hay gộp? | **Lưu 4 mức** (có VDC). Báo cáo 3 mức Bộ: **VDC gộp vào VD** |
| 3 | Short answer sai số? | Quy ước làm tròn **trong câu hỏi**; chỉ **so khớp đúng** mới cho điểm (nghiêm như thi ĐH/TN) |
| 4 | Ma trận sát tỷ lệ năm? | **User chọn**: mode COARSE (phần + chủ đề + mức) hoặc FINE (chi tiết dạng bài) |
| — | Đ/S mức theo ý hay câu? | **Theo cả câu** (đơn giản vận hành); 4 ý cố định, chấm vẫn theo số ý đúng |
| — | Đặc tả đề? | **MVP bắt buộc**: sau bốc → đặc tả draft → GV chỉnh → khóa mới xuất bản |
