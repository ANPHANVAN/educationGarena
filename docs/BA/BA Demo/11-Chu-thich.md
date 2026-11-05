# 11 — Chú thích thuật ngữ

Một nơi giải thích thuật ngữ và chỗ dễ lẫn trong bộ BA Demo. Lần đầu một tài liệu dùng thuật ngữ, chữ đó dẫn tới mục ở đây — kiểu chú thích cuối sách. Nghĩa chi tiết, ví dụ số và quy tắc vận hành vẫn nằm ở tài liệu nghiệp vụ; mục này chỉ để tra.

Sửa định nghĩa ở file này. Các file khác giữ link, không chép lại đoạn giải thích dài.

## Mục lục tra cứu

**Phân loại câu** — [Chủ đề](#chu-de) · [L1](#l1) · [L2](#l2) · [Cấp độ tư duy](#cap-do-tu-duy) · [NB / TH / VD / VDC](#bon-muc) · [Dạng thức](#dang-thuc) · [MCQ](#mcq) · [Đúng/Sai](#dung-sai) · [Trả lời ngắn](#tra-loi-ngan) · [Năng lực](#nang-luc) · [Stem](#stem) · [Stimulus](#stimulus) · [Question / Item](#question-item)

**Ma trận và sinh đề** — [Ngân hàng câu hỏi](#ngan-hang-cau-hoi) · [Ma trận](#ma-tran) · [Ô ma trận](#o-ma-tran) · [Granularity](#granularity) · [COARSE](#coarse) · [FINE](#fine) · [Sinh đề / bốc câu](#sinh-de) · [Tồn kho](#ton-kho) · [Template](#blueprint-template) · [Score policy](#score-policy)

**Đề và thi** — [Đặc tả đề](#dac-ta-de) · [YCCĐ](#yccd) · [ExamVersion](#exam-version) · [Khóa đề](#khoa-de) · [Snapshot](#snapshot) · [Đề đóng gói](#de-dong-goi) · [Attempt](#attempt) · [Đợt thi](#exam-campaign) · [CBT](#cbt) · [Exact match](#exact-match)

**Tổ chức** — [Taxonomy](#taxonomy) · [Ownership layer](#ownership-layer) · [ContentAdmin](#content-admin) · [CV 7991](#cv-7991)

---

<a id="ba-truc"></a>

## Ba trục phân loại

Mỗi câu trong bank mang **ba nhãn độc lập**. Trộn ba trục này thì ma trận mất nghĩa.

| Trục | Trả lời câu hỏi | Ví dụ |
|------|-----------------|-------|
| [Chủ đề](#chu-de) | Kiến thức nào? | Khảo sát hàm số |
| [Cấp độ tư duy](#cap-do-tu-duy) | Đòi hỏi mức nào? | VD |
| [Dạng thức](#dang-thuc) | Thí sinh trả lời và máy chấm thế nào? | MCQ, Đúng/Sai, trả lời ngắn |

Cùng chủ đề “tích phân” có thể là câu NB dạng trắc nghiệm hoặc câu VDC dạng trả lời ngắn. Hai câu đó không nằm cùng một ô ma trận.

Đọc thêm: [02 §1](./02-Nghiep-vu-Toan-cau-truc-de-thi.md).

---

<a id="chu-de"></a>

## Chủ đề (Topic)

Đơn vị kiến thức dùng để lọc “câu này thuộc phần nào”. Trong sản phẩm, chủ đề là **dữ liệu** theo môn + lớp + phiên bản chương trình, không hard-code trong nghiệp vụ sinh đề.

Hai độ sâu: [L1](#l1) và [L2](#l2). Mỗi câu gắn ít nhất một L1. L2 gắn khi cần ma trận [FINE](#fine).

Đọc thêm: [10](./10-Danh-muc-chu-de-Toan-seed.md).

<a id="l1"></a>

## L1 — chủ đề lớn

Tầng chủ đề dùng cho ma trận nhanh và báo cáo. Ví dụ: `m12_khao_sat_ham_so` (khảo sát hàm số), `m12_oxyz`, `m12_nguyen_ham_tich_phan`.

Ô [COARSE](#coarse) lọc tới L1. Giáo viên chỉnh ma trận COARSE chỉ sửa số câu theo L1.

<a id="l2"></a>

## L2 — dạng bài

Tầng mịn hơn, nằm trong một L1. Với khảo sát hàm số: đơn điệu, cực trị, tiệm cận, GTLN–GTNN, tiếp tuyến, bài toán thực tế…

Ô [FINE](#fine) lọc thêm đúng một L2. Câu chưa gắn L2 không lọt vào ô FINE đòi dạng đó, dù L1 khớp.

---

<a id="cap-do-tu-duy"></a>

## Cấp độ tư duy (CognitiveLevel)

Mức đòi hỏi của **cả câu**, theo thói quen ma trận nhà trường Việt Nam. Bắt buộc trên câu. Câu Đúng/Sai cũng một mức cho cả câu, không gắn mức từng ý.

Hệ thống lưu 4 mức. Khi xuất báo cáo theo khung Bộ 3 mức (Biết – Hiểu – Vận dụng), VDC được đếm vào nhóm Vận dụng:

```
NB_report = count(NB)
TH_report = count(TH)
VD_report = count(VD) + count(VDC)
```

Đọc thêm: [02 §2](./02-Nghiep-vu-Toan-cau-truc-de-thi.md), [09 §2](./09-Dac-ta-de-va-quy-tac-da-chot.md).

<a id="bon-muc"></a>
<a id="nb"></a>
<a id="th"></a>
<a id="vd"></a>
<a id="vdc"></a>

## NB, TH, VD, VDC

| Mã | Tên | Ý nghiệp vụ |
|----|-----|-------------|
| **NB** | Nhận biết | Nhớ định nghĩa, công thức, nhận dạng đối tượng |
| **TH** | Thông hiểu | Giải thích, đổi cách biểu diễn, tính toán theo quy trình chuẩn |
| **VD** | Vận dụng | Áp dụng vào tình huống quen, bài có quy trình |
| **VDC** | Vận dụng cao | Tình huống mới, nối nhiều mảng kiến thức, câu phân hóa |

Đề tốt nghiệp THPT từ 2025 trên văn bản Bộ thường ghi 3 mức. Giáo viên ôn thi vẫn gọi “vận dụng cao” cho câu phân hóa, nên bank giữ VDC riêng.

---

<a id="dang-thuc"></a>

## Dạng thức câu hỏi (ItemFormat)

Cách thí sinh trả lời và cách máy chấm. Tách khỏi chủ đề và khỏi cấp độ tư duy.

Ba dạng giai đoạn 1 (đề TN THPT từ 2025): [MCQ](#mcq), [Đúng/Sai](#dung-sai), [trả lời ngắn](#tra-loi-ngan). Tự luận (ESSAY) để sau, chấm tay.

Điểm từng dạng là [score policy](#score-policy) của template, không hard-code chung mọi môn. Toán Phần III là 0,5 điểm/câu; nhiều môn khác là 0,25.

<a id="mcq"></a>

## MCQ (`MCQ_SINGLE`)

Trắc nghiệm nhiều lựa chọn, một đáp án đúng. Đề TN Toán Phần I: 12 câu, 4 phương án A/B/C/D, 0,25 điểm/câu đúng.

Trong ma trận, 1 câu MCQ = 1 đơn vị đếm.

<a id="dung-sai"></a>

## Đúng/Sai (`TRUE_FALSE_GROUP`)

Một câu gồm đúng 4 ý (a, b, c, d). Mỗi ý chọn Đúng hoặc Sai. Đề TN Toán Phần II: 4 câu như vậy.

Đếm ở bank, ma trận, đặc tả, tồn kho: **1 câu = 1 đơn vị**. Bốn ý là cấu trúc cố định bên trong câu, phục vụ hiển thị và chấm. Mức độ và chủ đề gắn trên câu.

Điểm theo số ý đúng trong câu (policy TN): 1 → 0,1 · 2 → 0,25 · 3 → 0,5 · 4 → 1,0. Không ý nào đúng thì 0.

Đọc thêm: [09 §5](./09-Dac-ta-de-va-quy-tac-da-chot.md), [03 §3](./03-Ma-tran-va-sinh-de.md).

<a id="tra-loi-ngan"></a>

## Trả lời ngắn (`SHORT_ANSWER`)

Thí sinh điền kết quả (số hoặc biểu thức ngắn). Đề TN Toán Phần III: 6 câu, 0,5 điểm/câu đúng.

Quy ước làm tròn, đơn vị, số chữ số nằm trong [stem](#stem). Máy chấm bằng [exact match](#exact-match) sau khi chuẩn hóa chuỗi. Mode thi không cho điểm “gần đúng”.

Đọc thêm: [09 §3](./09-Dac-ta-de-va-quy-tac-da-chot.md).

<a id="nang-luc"></a>

## Năng lực (Competency)

Trục chương trình 2018, tách khỏi ba trục bắt buộc. Hay gặp trên bảng năng lực – cấp độ tư duy của nhà trường: tư duy và lập luận (TD), giải quyết vấn đề (GQ), mô hình hóa (MH).

MVP: trường này tùy chọn. Ma trận [FINE](#fine) có thể lọc thêm năng lực khi giáo viên cần.

<a id="stem"></a>

## Stem

Đề bài thí sinh đọc: lời dẫn, công thức, yêu cầu. Với trả lời ngắn, stem phải chứa quy ước làm tròn nếu đáp án phụ thuộc cách làm tròn. Ý Đúng/Sai có stem riêng (`stem_idea`); đoạn mở đầu chung của cả câu có thể là stem chung hoặc [stimulus](#stimulus).

<a id="stimulus"></a>

## Stimulus

Ngữ liệu dùng chung: hình, bảng số, đoạn văn. Thuộc câu (hoặc một nhóm câu), không phải một câu tính điểm riêng. Khi sinh đề, lấy cả bundle; không tách hình khỏi câu dựa vào hình đó.

<a id="question-item"></a>

## Question và QuestionItem

**Question** là đơn vị gán vào đề và là đơn vị đếm của ma trận. **QuestionItem** là ý chấm được bên trong câu.

MCQ: 1 question, 1 item. Đúng/Sai: 1 question, 4 item. Đặc tả ghi 1 dòng cho cả câu Đúng/Sai, có thể liệt kê 4 ý trong nội dung dòng.

---

<a id="ngan-hang-cau-hoi"></a>

## Ngân hàng câu hỏi (Question Bank)

Kho câu đã gắn đủ metadata (môn, lớp, chủ đề, cấp độ, dạng thức, trạng thái duyệt, nguồn gốc). Ma trận chỉ bốc được câu còn trong kho và thỏa filter của ô.

Câu đưa vào đề thi chính thức lấy `status = approved`. Luyện tập có thể mở thêm câu `practice_ok`. Sửa câu trong bank không đổi đề đã [khóa](#khoa-de), vì đề giữ [snapshot](#snapshot).

Đọc thêm: [05](./05-Ngan-hang-cau-hoi.md).

<a id="ma-tran"></a>

## Ma trận đề (Blueprint)

Bảng quy tắc phân bổ: mỗi [ô](#o-ma-tran) trả lời “lấy bao nhiêu câu thỏa điều kiện nào”. Một blueprint là một bản ma trận cụ thể, sinh ra được nhiều [ExamVersion](#exam-version).

Hai độ chi tiết, chọn lúc tạo ma trận: [COARSE](#coarse) hoặc [FINE](#fine). Cả ma trận một mode; không trộn hai mode trong cùng một blueprint.

Đọc thêm: [03](./03-Ma-tran-va-sinh-de.md).

<a id="o-ma-tran"></a>

## Ô ma trận (BlueprintCell)

Một dòng điều kiện + số lượng + cách tính điểm. Ví dụ COARSE: Phần I · MCQ · khảo sát hàm số (L1) · VD · 2 câu.

Sinh đề xử lý từng ô: query bank theo filter của ô, loại câu trùng, bốc đủ số yêu cầu. Đổi câu sau khi bốc chỉ được đổi sang câu khác **cùng ô** (cùng filter).

<a id="granularity"></a>

## Granularity

Trường `Blueprint.granularity`: `COARSE` hoặc `FINE`. Quyết định ô lọc dừng ở [L1](#l1) hay đi tiếp tới [L2](#l2). Tồn kho hiển thị đúng độ sâu đã chọn.

<a id="coarse"></a>

## COARSE

Mode ma trận nhanh. Mỗi ô lọc:

**phần đề + chủ đề L1 + mức (NB/TH/VD/VDC) + dạng thức.**

Giáo viên chỉ sửa số câu theo chủ đề lớn. Mọi dạng bài L2 nằm trong L1 đó đều hợp lệ. Ô “khảo sát hàm số · VD · MCQ · 2 câu” có thể ra hai câu cực trị. Đề vẫn đúng ma trận.

Dùng khi luyện, hoặc khi không cần đề bám từng dạng của một năm. Bank chỉ cần tag L1 là sinh được.

Template `TN_THPT_TOAN_*` có bản COARSE theo bảng phân bố L1 (ví dụ Phần I: lượng giác 1, Oxyz 3, tích phân 2…).

<a id="fine"></a>

## FINE

Mode ma trận chi tiết. Mỗi ô = filter của COARSE **cộng dạng bài L2** (và có thể thêm [năng lực](#nang-luc)).

Cùng nhu cầu “2 câu VD hàm số” được tách thành các ô riêng, ví dụ 1 câu cực trị và 1 câu tiệm cận. Câu cực trị không lấp ô tiệm cận. Vì vậy FINE giữ đề gần phân bố dạng của năm, và tránh dồn một mẹo.

Đổi lại, pool mỗi ô nhỏ hơn: tồn kho dễ thiếu, và câu không có tag L2 không vào ô FINE yêu cầu dạng đó. Giáo viên sửa cả số câu theo L2.

Template TN có thể ship sẵn bản FINE đã tách dạng (cực trị, tiệm cận, min-max, vectơ, khoảng cách…).

Điểm, dạng thức và quy tắc “Đúng/Sai đếm theo câu” giống hệt COARSE. Khác nhau chỉ là độ sâu filter lúc bốc và lúc đối tồn kho.

```
COARSE:  topic L1 + mức + format  →  N câu
FINE:    topic L1 + L2 + mức + format  →  N câu
```

Đọc thêm: [03 §2](./03-Ma-tran-va-sinh-de.md), [09 §4](./09-Dac-ta-de-va-quy-tac-da-chot.md), [10 §3](./10-Danh-muc-chu-de-Toan-seed.md).

<a id="sinh-de"></a>

## Sinh đề / bốc câu

Với từng ô ma trận, lấy ngẫu nhiên (hoặc theo trọng số) đủ câu từ bank còn tồn, ra một đề nháp.

Bốc **một lần** lúc giáo viên sinh. Sau đó đề là một danh sách câu cố định. Học sinh trong cùng đợt mở cùng link thì làm cùng đề. Random lại theo từng thí sinh không nằm trong luồng này. Muốn nhiều mã đề thì chủ đích sinh thêm nhiều ExamVersion.

Thiếu một ô thì dừng cả lần sinh và liệt kê ô thiếu. Không bù câu ngoài filter của ô.

Đọc thêm: [03 §4–§5](./03-Ma-tran-va-sinh-de.md).

<a id="ton-kho"></a>

## Tồn kho

Số câu trong bank đang thỏa filter của một ô và còn được phép bốc (đã duyệt, chưa bị loại vì trùng đề, v.v.).

UI hiện kiểu: `NB · hàm số · MCQ: có 40 — yêu cầu 3`. Ô FINE đếm hẹp hơn, tới từng L2. Đúng/Sai đếm theo câu, không đếm theo ý.

<a id="blueprint-template"></a>

## Template ma trận (BlueprintTemplate)

Khung đề làm sẵn, user nhân ra thành blueprint rồi sửa số. Ví dụ:

| Mã | Việc |
|----|------|
| `TN_THPT_TOAN_2025` | 12 MCQ + 4 câu Đúng/Sai + 6 trả lời ngắn, thang điểm TN |
| `SCHOOL_PERIODIC_TOAN` | Ma trận tự do theo chương, NB/TH/VD/VDC |
| `PRACTICE_TOPIC_DRILL` | Luyện 1–n chủ đề, tự chọn số câu × mức |

<a id="score-policy"></a>

## Score policy

Quy tắc đổi kết quả từng câu thành điểm, gắn template chứ không gắn cứng vào môn trong code. Policy TN Toán: MCQ 0,25; Đúng/Sai theo số ý đúng 0,1 / 0,25 / 0,5 / 1; trả lời ngắn 0,5. Môn khác dùng policy của template môn đó.

---

<a id="dac-ta-de"></a>

## Đặc tả đề (ExamSpec)

Bảng mô tả đề **sau khi đã bốc**: từng vị trí gắn câu thật, chủ đề, mức, dạng thức, điểm, và [YCCĐ](#yccd).

Ma trận thì đếm (“bao nhiêu câu”). Đặc tả thì chỉ mặt (“câu số mấy là câu nào, kiểm tra điều gì”). Sinh đề tạo đặc tả bản nháp cùng ExamVersion nháp. Giáo viên sửa rồi mới khóa. Học sinh không làm trên bản chưa khóa.

Đọc thêm: [09 §1](./09-Dac-ta-de-va-quy-tac-da-chot.md).

<a id="yccd"></a>

## YCCĐ — yêu cầu cần đạt

Lời mô tả ngắn trên một dòng đặc tả: câu này kiểm tra kỹ năng gì. Hệ thống điền sẵn từ metadata / mô tả trong bank; giáo viên được sửa chữ trên đặc tả. Sửa YCCĐ không đổi đáp án câu.

<a id="exam-version"></a>

## ExamVersion

Một đề cụ thể: danh sách câu đã chọn, thứ tự, điểm. Trạng thái nháp (`DRAFT`) rồi khóa (`LOCKED` / xuất bản).

Một blueprint sinh nhiều ExamVersion (đề gốc, mã đề 2, bản sửa sau khi đã có người làm). Một ExamVersion khóa dùng cho nhiều [Attempt](#attempt). Cả lớp cùng link là cùng ExamVersion.

<a id="khoa-de"></a>

## Khóa đề (LOCK)

Bước giáo viên xác nhận đề sau khi đã xem đặc tả. Hệ thống kiểm tra đề còn khớp ma trận (đủ số câu từng ô, đúng mức, đúng dạng). Khóa xong mới gắn vào kỳ thi hoặc luyện chính thức.

Đề đã có bài làm thì không sửa tại chỗ. Muốn đổi thì tạo version mới.

<a id="snapshot"></a>

## Snapshot

Bản chụp stem, đáp án và metadata tại lúc khóa, lưu trong ExamVersion và đặc tả. Bank sửa câu sau đó không làm đổi đề đã thi và không làm đổi bài đã chấm.

<a id="de-dong-goi"></a>

## Đề đóng gói (Fixed Exam)

Đề đã thành danh sách câu cố định: giáo viên chọn tay từng câu, gói đề bán sẵn, hoặc đề sinh từ ma trận rồi lưu lại. Học sinh thi bằng cùng một ExamVersion + cùng link.

“Sinh từ ma trận” và “đề đóng gói” gặp nhau sau bước khóa: cả hai đều là một ExamVersion cố định để chia sẻ.

Đọc thêm: [01 §6.5](./01-Tong-quan-san-pham.md).

<a id="attempt"></a>

## Attempt

Một lần một người làm một ExamVersion: giờ bắt đầu, đáp án từng ý, điểm. Hết giờ thì nộp tự động. Đáp án Đúng/Sai lưu từng ý để chấm theo số ý đúng.

<a id="exam-campaign"></a>

## Đợt thi (ExamCampaign)

Kỳ thi gắn một hoặc nhiều đề cho một nhóm học sinh. Trên demo Bộ, màn “đợt thi” tương ứng entity này. Ca / phòng (`ExamSession`) là tùy chọn, chưa bắt buộc ở MVP.

<a id="cbt"></a>

## CBT

Thi trên máy tính (computer-based test): đăng nhập phiên, đồng hồ, một câu hoặc một nhóm ý trên màn hình, palette câu, lưu đáp án, nộp, chấm máy. Demo Cục Quản lý chất lượng là tham chiếu giao diện, không phải sản phẩm này đóng vai phần mềm thi của Bộ.

<a id="exact-match"></a>

## Exact match

Cách chấm trả lời ngắn ở mode thi. Chuẩn hóa chuỗi (cắt khoảng trắng, thống nhất dấu thập phân, bỏ dấu ngăn nghìn) rồi so với danh sách đáp án giáo viên đã khai. `1/2` và `0,5` chỉ cùng đúng khi cả hai được khai là đáp án chấp nhận. Giá trị “gần” đáp án thì không có điểm.

---

<a id="taxonomy"></a>

## Taxonomy

Bộ danh mục dùng chung để gắn nhãn: môn, lớp, phiên bản chương trình, cây chủ đề, cấp độ tư duy, dạng thức, năng lực. Đổi tên chủ đề thì version taxonomy; đề đã snapshot giữ tên tại lúc khóa.

<a id="ownership-layer"></a>

## Ownership layer

Lớp sở hữu của câu hoặc đề, là danh mục thêm được, không khóa cứng vài giá trị trong code. Seed: `personal` (của giáo viên), `center` (trong trung tâm), `system` (kho nền tảng, phải duyệt), `secret` (đề chưa công bố).

Đọc thêm: [01 §6.3](./01-Tong-quan-san-pham.md).

<a id="cv-7991"></a>

## CV 7991

Công văn 7991/BGDĐT-GDTrH (2019), tài liệu tập huấn xây dựng ma trận và đặc tả đề kiểm tra định kỳ. BA nhắc tới để chỉ cách nhà trường tách **ma trận** (bảng đếm) khỏi **đặc tả** (mô tả từng câu). Không phải văn bản cấu trúc đề tốt nghiệp.

<a id="content-admin"></a>

## ContentAdmin

Người duyệt câu đưa vào kho chung của nền tảng: đúng đề, đúng đáp án, đúng nhãn. Câu giáo viên giữ ở bank cá nhân hoặc trung tâm để ra đề nội bộ thì không cần duyệt hệ thống.
