# Tóm tắt điều hành (1 trang)

## Sản phẩm là gì?

Nền tảng **ngân hàng câu hỏi + ma trận sinh đề + thi/luyện trên máy**, bắt đầu môn **Toán**, UI thi học theo demo CBT của Bộ (không đóng vai phần mềm thi quốc gia).

## Core phải làm trước

1. Câu hỏi có metadata: **chủ đề (dạng bài) × cấp độ tư duy × dạng thức (loại câu hỏi)**.  
2. **Ma trận** quy định số câu mỗi ô → hệ thống **bốc** từ bank.  
3. **Thi + chấm máy** 3 dạng: MCQ, Đúng/Sai (4 ý), Trả lời ngắn.  
4. Luyện tập = tái sử dụng cùng engine (UI vui để sau).

## Logic Toán cần nhớ

| Kỳ | Hình thức nổi bật | Hệ quả phần mềm |
|----|-------------------|-----------------|
| TN THPT Toán từ 2025 | 22 câu / 34 ý; 90 phút; 3 phần | Template scoring đặc biệt Phần II |
| Kiểm tra 10–11–12 | Ma trận NB/TH/VD/VDC theo chương | Ma trận tự do + tồn kho |
| Vào lớp 10 | Thường tự luận theo Sở | P2; đừng thiết kế chỉ MCQ |

**Cấp độ:** NB → TH → VD → **VDC** (báo cáo 3 mức: VDC gộp VD).  
**Dạng thức ≠ mức độ ≠ chủ đề** — ba trục tách riêng; Đ/S gắn mức **cả câu** (4 ý cố định).  
**Sau bốc câu:** bắt buộc **đặc tả** → GV chỉnh → khóa đề. Short: làm tròn trong stem, chấm khớp đúng. Ma trận COARSE hoặc FINE do user chọn.

## Đối tượng hệ thống

Student, Teacher, (CenterAdmin), ContentAdmin.  
Thực thể chính: Topic, Question(/Item), Blueprint, ExamVersion, Attempt.

## Mở nhiều môn sau?

**Được** nếu không hard-code Toán: subject + topic data + score policy config. Nhượng quyền = content pack + người phụ trách môn.

## Không làm ở MVP (tiết kiệm vốn)

AI bắt điện thoại, gamification nặng, parse PDF hoàn hảo, microservices, tự host LLM.  
Import đề: form + template text trước; AI bằng **API key user** sau.

## Việc team cần làm tiếp

1. GV review **09** (đã chốt) + tinh chỉnh taxonomy **10**.  
2. Segment đã chốt: **10–11–12**; ownership layer động; đề khóa = 1 link chung cho cả lớp.  
3. Seed ~50 câu mẫu (Đ/S: 1 mức/câu + 4 ý) → code P0 theo **06** (có đặc tả).  
4. Bản thống nhất → `docs/BA/BA chốt/`.
