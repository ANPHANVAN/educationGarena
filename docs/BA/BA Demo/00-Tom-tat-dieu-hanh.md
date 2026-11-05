# Tóm tắt điều hành (1 trang)

## Sản phẩm là gì?

Nền tảng **[ngân hàng câu hỏi](./11-Chu-thich.md#ngan-hang-cau-hoi) + [ma trận](./11-Chu-thich.md#ma-tran) [sinh đề](./11-Chu-thich.md#sinh-de) + thi/luyện trên máy**, bắt đầu môn **Toán**, UI thi học theo demo [CBT](./11-Chu-thich.md#cbt) của Bộ (không đóng vai phần mềm thi quốc gia).

## Core phải làm trước

1. Câu hỏi có metadata: **[chủ đề](./11-Chu-thich.md#chu-de) (dạng bài) × [cấp độ tư duy](./11-Chu-thich.md#cap-do-tu-duy) × [dạng thức](./11-Chu-thich.md#dang-thuc) (loại câu hỏi)**.  
2. **Ma trận** quy định số câu mỗi [ô](./11-Chu-thich.md#o-ma-tran) → hệ thống **bốc** từ bank.  
3. **Thi + chấm máy** 3 dạng: [MCQ](./11-Chu-thich.md#mcq), [Đúng/Sai](./11-Chu-thich.md#dung-sai) (4 ý), [Trả lời ngắn](./11-Chu-thich.md#tra-loi-ngan).  
4. Luyện tập = tái sử dụng cùng engine (UI vui để sau).

## Logic Toán cần nhớ

| Kỳ | Hình thức nổi bật | Hệ quả phần mềm |
|----|-------------------|-----------------|
| TN THPT Toán từ 2025 | 22 câu / 34 ý; 90 phút; 3 phần | Template [scoring](./11-Chu-thich.md#score-policy) đặc biệt Phần II |
| Kiểm tra 10–11–12 | Ma trận [NB](./11-Chu-thich.md#nb)/[TH](./11-Chu-thich.md#th)/[VD](./11-Chu-thich.md#vd)/[VDC](./11-Chu-thich.md#vdc) theo chương | Ma trận tự do + [tồn kho](./11-Chu-thich.md#ton-kho) |
| Vào lớp 10 | Thường tự luận theo Sở | P2; đừng thiết kế chỉ MCQ |

**Cấp độ:** NB → TH → VD → **VDC** (báo cáo 3 mức: VDC gộp VD).  
**Dạng thức ≠ mức độ ≠ chủ đề** — ba trục tách riêng; Đ/S gắn mức **cả câu** (4 ý cố định).  
**Sau bốc câu:** bắt buộc **[đặc tả](./11-Chu-thich.md#dac-ta-de)** → GV chỉnh → [khóa đề](./11-Chu-thich.md#khoa-de). Short: làm tròn trong [stem](./11-Chu-thich.md#stem), chấm [khớp đúng](./11-Chu-thich.md#exact-match). Ma trận [COARSE](./11-Chu-thich.md#coarse) hoặc [FINE](./11-Chu-thich.md#fine) do user chọn.

## Đối tượng hệ thống

Student, Teacher, (CenterAdmin), [ContentAdmin](./11-Chu-thich.md#content-admin).  
Thực thể chính: Topic, [Question(/Item)](./11-Chu-thich.md#question-item), [Blueprint](./11-Chu-thich.md#ma-tran), [ExamVersion](./11-Chu-thich.md#exam-version), [Attempt](./11-Chu-thich.md#attempt).

## Mở nhiều môn sau?

**Được** nếu không hard-code Toán: subject + topic data + score policy config. Nhượng quyền = content pack + người phụ trách môn.

## Không làm ở MVP (tiết kiệm vốn)

AI bắt điện thoại, gamification nặng, parse PDF hoàn hảo, microservices, tự host LLM.  
Import đề: form + template text trước; AI bằng **API key user** sau.

## Việc team cần làm tiếp

1. GV review **09** (đã chốt) + tinh chỉnh [taxonomy](./11-Chu-thich.md#taxonomy) **10**.  
2. Segment đã chốt: **10–11–12**; [ownership layer](./11-Chu-thich.md#ownership-layer) động; đề khóa = 1 link chung cho cả lớp.  
3. Seed ~50 câu mẫu (Đ/S: 1 mức/câu + 4 ý) → code P0 theo **06** (có đặc tả).  
4. Bản thống nhất → `docs/BA/BA chốt/`.
