# Tóm tắt điều hành (1 trang)

## Sản phẩm là gì?

Nền tảng **[ngân hàng câu hỏi](./11-Chu-thich.md#ngan-hang-cau-hoi) + [ma trận](./11-Chu-thich.md#ma-tran) [sinh đề](./11-Chu-thich.md#sinh-de) + thi/luyện trên máy** — **đa môn ngay từ đầu**, UI thi học theo demo [CBT](./11-Chu-thich.md#cbt) của Bộ (không đóng vai phần mềm thi quốc gia). Toán là môn seed sâu nhất; chưa làm riêng Văn / Tin / Công nghệ.

## Core phải làm trước

1. Câu hỏi có metadata: **môn × [chủ đề](./11-Chu-thich.md#chu-de) (L1/L2) × [cấp độ tư duy](./11-Chu-thich.md#cap-do-tu-duy) × [dạng thức](./11-Chu-thich.md#dang-thuc)**.  
2. **[Khung bài thi](./11-Chu-thich.md#khung-bai-thi)** / template theo kỳ (TN theo môn, kiểm tra, **đề trộn môn ĐGNL-style**) → [ma trận](./11-Chu-thich.md#ma-tran) bốc câu; GV chọn phần cần thi.  
3. **Thi + chấm máy** MCQ, Đúng/Sai (4 ý), Trả lời ngắn (khi môn có).  
4. Xáo thứ tự câu (theo khối [stimulus](./11-Chu-thich.md#stimulus)) + xáo A–D.  
5. Luyện tập = cùng engine (UI vui để sau).

## Logic cần nhớ

| Kỳ | Hình thức nổi bật | Hệ quả phần mềm |
|----|-------------------|-----------------|
| TN THPT (hầu hết môn) | 2–3 dạng thức; Văn tự luận | Template scoring theo môn; chưa làm Văn |
| Kiểm tra 10–12 | Ma trận theo chương | Chọn phần / chủ đề linh hoạt |
| ĐGNL / thi thử liên môn | Trắc nghiệm trộn môn | Blueprint multi-subject |
| Vào lớp 10 | Thường tự luận theo Sở | P2 |

**Cấp độ:** NB → TH → VD → **VDC**.  
**Dạng thức ≠ mức độ ≠ chủ đề.** Một môn ↔ nhiều template kỳ; L1/L2 chỉ là cây chủ đề trong môn.  
**Sau bốc câu:** [đặc tả](./11-Chu-thich.md#dac-ta-de) → GV chỉnh → [khóa đề](./11-Chu-thich.md#khoa-de).

## Đối tượng hệ thống

Student, Teacher, (CenterAdmin), [ContentAdmin](./11-Chu-thich.md#content-admin).  
Thực thể chính: Subject, Topic, [Question](./11-Chu-thich.md#question-item), [Blueprint](./11-Chu-thich.md#ma-tran), [ExamVersion](./11-Chu-thich.md#exam-version), [Attempt](./11-Chu-thich.md#attempt).

## Nhiều môn?

**Làm ngay** với engine chung + content pack. Đợt đầu: môn TN phổ biến. **Để ngỏ:** Văn, Tin, Công nghệ, audio. Chi tiết: [06](./06-MVP-uu-tien-va-pham-vi.md), [07](./07-Mo-rong-nhieu-mon.md).

## Không làm ở MVP (tiết kiệm vốn)

AI bắt điện thoại, gamification nặng, parse PDF hoàn hảo, microservices, tự host LLM, pipeline riêng Văn/Tin/CN.  
Import đề: form + template text trước; AI bằng **API key user** sau.

## Việc team cần làm tiếp

1. GV review **09** + tinh chỉnh [taxonomy](./11-Chu-thich.md#taxonomy) **10** (Toán); seed mỏng môn demo thứ 2.  
2. Segment đã chốt: **10–11–12**; đề khóa = 1 link chung cho cả lớp.  
3. Seed câu mẫu → code P0 theo **06** (đa môn + đặc tả + xáo đề).  
4. Đọc [12 — Pháp lý](./12-Phap-ly-va-rui-ro.md) trước khi public / thu tiền (không scrap đề, không gắn Bộ, consent phụ huynh).  
5. Bản thống nhất → `docs/BA/BA chốt/`.
