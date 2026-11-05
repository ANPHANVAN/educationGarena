# 04 — Đối tượng người dùng & mô hình nghiệp vụ

---

## 1. Actors (vai trò)

| Role | Mục tiêu | Quyền chính (MVP) |
|------|----------|-------------------|
| **Student** | Luyện / thi thử, xem điểm, (sau) xếp hạng | Làm bài, xem lịch sử, xem giải (nếu gói cho phép) |
| **Teacher** | Nhập câu, tạo [ma trận](./11-Chu-thich.md#ma-tran), [sinh đề](./11-Chu-thich.md#sinh-de), mở kỳ thi cho lớp/trung tâm | CRUD câu (tenant), blueprint, exam, xem báo cáo lớp |
| **CenterAdmin** | Quản lý giáo viên, học sinh, gói dịch vụ trung tâm | User, phân quyền, cấu hình kỳ thi |
| **[ContentAdmin](./11-Chu-thich.md#content-admin)** (team mình) | Duyệt câu “bank chung” của nền tảng | Approve/reject, [taxonomy](./11-Chu-thich.md#taxonomy) hệ thống |
| **System** | Chấm điểm, hết giờ auto-submit, billing | Job |

Giai đoạn 2 người: Teacher ≈ ContentAdmin; CenterAdmin có thể gộp Teacher.

---

## 2. Phân hệ nghiệp vụ

```
[Taxonomy]     Môn, lớp, chủ đề, mức tư duy, dạng thức
     │
[Question Bank] Câu hỏi + metadata + trạng thái duyệt
     │
[Blueprint]     Ma trận / template sinh đề
     │
[Exam]          ExamVersion (đề cụ thể đã khóa)
     │
[Delivery]      Kỳ thi / Phiên làm bài / Luyện tập
     │
[Result]        Bài làm, điểm, thống kê
```

---

## 3. Thực thể nghiệp vụ (logical model)

### 3.1. Taxonomy

- **Subject** — Toán, (sau) Lý…  
- **GradeLevel** — 10, 11, 12, (sau) 9…  
- **CurriculumVersion** — GDPT2018, …  
- **[Topic](./11-Chu-thich.md#chu-de)** — cây chủ đề theo Subject (+ Grade tùy chọn)  
- **[CognitiveLevel](./11-Chu-thich.md#cap-do-tu-duy)** — [NB](./11-Chu-thich.md#nb), [TH](./11-Chu-thich.md#th), [VD](./11-Chu-thich.md#vd), [VDC](./11-Chu-thich.md#vdc)  
- **[ItemFormat](./11-Chu-thich.md#dang-thuc)** — [MCQ_SINGLE](./11-Chu-thich.md#mcq), TRUE_FALSE_IDEA, [TRUE_FALSE_GROUP](./11-Chu-thich.md#dung-sai), [SHORT_ANSWER](./11-Chu-thich.md#tra-loi-ngan), ESSAY…  
- **[Competency](./11-Chu-thich.md#nang-luc)** (optional) — TD, GQ, MH  

### 3.2. [Ngân hàng](./11-Chu-thich.md#ngan-hang-cau-hoi)

- **[Stimulus](./11-Chu-thich.md#stimulus)** — ngữ liệu chung (đoạn văn, hình, bảng số liệu)  
- **[Question](./11-Chu-thich.md#question-item)** — đơn vị gán vào đề (có thể là group)  
- **QuestionItem** — ý/lệnh hỏi chấm điểm được (MCQ 1 item; Đ/S group có 4 item)  
- **Choice** — phương án A/B/C/D hoặc Đ/S  
- **Solution** — lời giải (ẩn theo gói)  
- **QuestionTag** — tag phụ (dạng “cực trị”, “thực tế kinh tế”…)  
- **[OwnershipLayer](./11-Chu-thich.md#ownership-layer)** — bảng động (`personal` / `center` / `system` / `secret` / …) gắn câu & đề  
- **Question.created_by** (+ org) — nguồn gốc bắt buộc để audit  

### 3.3. Ma trận, [đặc tả](./11-Chu-thich.md#dac-ta-de) & đề

- **[BlueprintTemplate](./11-Chu-thich.md#blueprint-template)** — mẫu (TN_THPT_TOAN_2025…)  
- **Blueprint** — instance ma trận; có [`granularity`](./11-Chu-thich.md#granularity): [COARSE](./11-Chu-thich.md#coarse) | [FINE](./11-Chu-thich.md#fine)  
- **[BlueprintCell](./11-Chu-thich.md#o-ma-tran)** — filters (topic [L1](./11-Chu-thich.md#l1)/[L2](./11-Chu-thich.md#l2), level, format, section) + count + [score_policy_ref](./11-Chu-thich.md#score-policy)  
- **Exam** — metadata đề (tên, môn, thời gian mặc định)  
- **[ExamVersion](./11-Chu-thich.md#exam-version)** — draft | locked; danh sách câu + [snapshot](./11-Chu-thich.md#snapshot) khi locked  
- **ExamVersionItem** — vị trí hiển thị, điểm tối đa, reference/snapshot **câu** (Đ/S = 1 câu kèm 4 ý)  
- **ExamSpec** — đặc tả đề (draft | locked) gắn ExamVersion  
- **ExamSpecRow** — dòng đặc tả: vị trí, [YCCĐ](./11-Chu-thich.md#yccd), topic, level, format, trỏ câu  

### 3.4. Tổ chức thi & luyện

- **Organization** — trung tâm / cá nhân giáo viên  
- **Classroom / Cohort** — lớp học sinh  
- **[ExamCampaign](./11-Chu-thich.md#exam-campaign)** — đợt thi (giống “đợt thi” trên demo Bộ)  
- **ExamSession** — ca/phòng (optional MVP)  
- **[Attempt](./11-Chu-thich.md#attempt)** — một lần làm bài của 1 user trên 1 ExamVersion  
- **AttemptAnswer** — đáp án từng item  
- **AttemptScore** — điểm chi tiết theo phần  

### 3.5. Tài khoản & gói

- **User**, **Enrollment**, **SubscriptionPlan**, **Entitlement**

---

## 4. Quan hệ then chốt (chữ, không ERD formal)

- 1 Subject có nhiều Topic.  
- 1 Question thuộc 1 Subject; gắn ≥1 Topic + **1 CognitiveLevel bắt buộc trên câu** (Đ/S không tách mức theo ý).  
- Câu Đ/S có đúng 4 ý (đáp án + [stem](./11-Chu-thich.md#stem) ý); mức/topic nằm ở câu.  
- 1 Blueprint có nhiều BlueprintCell; granularity COARSE|FINE.  
- 1 Blueprint sinh ra nhiều ExamVersion (kèm ExamSpec).  
- 1 ExamVersion (locked) dùng cho nhiều Attempt.  
- 1 Attempt lưu đáp án từng ý Đ/S → chấm theo policy số ý đúng trong câu.

---

## 5. Luồng nghiệp vụ chính

### Luồng A — Giáo viên dựng bank & ma trận → đặc tả

1. Tạo/import câu hỏi; Đ/S gắn **1 mức cho cả câu** + đủ 4 ý.  
2. ContentAdmin duyệt (nếu bank chung).  
3. Tạo Blueprint (template / tự do) + chọn COARSE hoặc FINE.  
4. Hệ thống báo [tồn kho](./11-Chu-thich.md#ton-kho) theo ô (Đ/S đếm theo câu).  
5. Sinh ExamVersion **DRAFT** + **Đặc tả DRAFT**.  
6. GV chỉnh câu/thứ tự/YCCĐ → Validate → **[LOCK](./11-Chu-thich.md#khoa-de)** → xuất bản.

### Luồng B — Học sinh thi thử “chuẩn Bộ”

1. Vào đợt thi / chọn đề thi thử.  
2. Bắt đầu Attempt (server clock).  
3. Làm bài, autosave.  
4. Nộp / hết giờ.  
5. Chấm theo score policy template.  
6. Hiện kết quả (điểm; chi tiết đúng/sai tùy cấu hình).

### Luồng C — Luyện theo ma trận tự chọn

1. Học sinh (hoặc GV giao) chọn chủ đề + số câu/mức.  
2. Sinh đề on-the-fly (ExamVersion tạm).  
3. Làm bài → xem giải ngay (mode luyện).

---

## 6. Mapping sang demo Bộ (để đồng bộ ngôn ngữ UI)

| Demo Bộ | Entity của mình |
|---------|-----------------|
| Đợt thi | ExamCampaign |
| Ca thi / phòng | ExamSession (P1) |
| Môn thi → Vào thi | Subject + ExamVersion assigned |
| Palette câu | ExamVersionItem list + AttemptAnswer state |
| Kết quả | AttemptScore |

---

## 7. Ownership & phạm vi nhìn thấy (đã chốt hướng)

- Layer sở hữu là **danh mục động** (xem `01` §6.3), không hard-code vĩnh viễn.  
- Seed tối thiểu: `personal`, `center`, `system`, `secret`.  
- Câu vào **system** bắt buộc qua duyệt (đúng stem + đáp án).  
- GV luôn tạo được đề / câu **personal** (và `center` nếu thuộc org) để dùng nội bộ.  
- `organization_id` nullable từ đầu; đề/câu `secret` chỉ user được cấp quyền trong đợt thi.

---

## 8. Những gì chưa cần entity riêng lúc đầu

- Proctoring event (tab blur) — log đơn giản trên Attempt nếu làm.  
- Ranking season, badge, meme asset.  
- AI import job (làm sau dạng ImportJob).
