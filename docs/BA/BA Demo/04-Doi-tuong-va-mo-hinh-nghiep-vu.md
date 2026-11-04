# 04 — Đối tượng người dùng & mô hình nghiệp vụ

---

## 1. Actors (vai trò)

| Role | Mục tiêu | Quyền chính (MVP) |
|------|----------|-------------------|
| **Student** | Luyện / thi thử, xem điểm, (sau) xếp hạng | Làm bài, xem lịch sử, xem giải (nếu gói cho phép) |
| **Teacher** | Nhập câu, tạo ma trận, sinh đề, mở kỳ thi cho lớp/trung tâm | CRUD câu (tenant), blueprint, exam, xem báo cáo lớp |
| **CenterAdmin** | Quản lý giáo viên, học sinh, gói dịch vụ trung tâm | User, phân quyền, cấu hình kỳ thi |
| **ContentAdmin** (team mình) | Duyệt câu “bank chung” của nền tảng | Approve/reject, taxonomy hệ thống |
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
- **Topic** — cây chủ đề theo Subject (+ Grade tùy chọn)  
- **CognitiveLevel** — NB, TH, VD, VDC  
- **ItemFormat** — MCQ_SINGLE, TRUE_FALSE_IDEA, TRUE_FALSE_GROUP, SHORT_ANSWER, ESSAY…  
- **Competency** (optional) — TD, GQ, MH  

### 3.2. Ngân hàng

- **Stimulus** — ngữ liệu chung (đoạn văn, hình, bảng số liệu)  
- **Question** — đơn vị gán vào đề (có thể là group)  
- **QuestionItem** — ý/lệnh hỏi chấm điểm được (MCQ 1 item; Đ/S group có 4 item)  
- **Choice** — phương án A/B/C/D hoặc Đ/S  
- **Solution** — lời giải (ẩn theo gói)  
- **QuestionTag** — tag phụ (dạng “cực trị”, “thực tế kinh tế”…)  
- **QuestionOwnership** — bank chung / bank tenant trung tâm  

### 3.3. Ma trận & đề

- **BlueprintTemplate** — mẫu (TN_THPT_TOAN_2025…)  
- **Blueprint** — instance ma trận (các ô + rule điểm)  
- **BlueprintCell** — filters + count + section + score_policy_ref  
- **Exam** — metadata đề (tên, môn, thời gian mặc định)  
- **ExamVersion** — bản đã sinh / đã khóa danh sách câu + snapshot  
- **ExamVersionItem** — vị trí hiển thị, điểm tối đa, reference/snapshot câu  

### 3.4. Tổ chức thi & luyện

- **Organization** — trung tâm / cá nhân giáo viên  
- **Classroom / Cohort** — lớp học sinh  
- **ExamCampaign** — đợt thi (giống “đợt thi” trên demo Bộ)  
- **ExamSession** — ca/phòng (optional MVP)  
- **Attempt** — một lần làm bài của 1 user trên 1 ExamVersion  
- **AttemptAnswer** — đáp án từng item  
- **AttemptScore** — điểm chi tiết theo phần  

### 3.5. Tài khoản & gói

- **User**, **Enrollment**, **SubscriptionPlan**, **Entitlement**

---

## 4. Quan hệ then chốt (chữ, không ERD formal)

- 1 Subject có nhiều Topic.  
- 1 Question thuộc 1 Subject, gắn ≥1 Topic, 1 CognitiveLevel (hoặc per-item), 1 ItemFormat.  
- 1 Stimulus có nhiều Question.  
- 1 Blueprint có nhiều BlueprintCell.  
- 1 Blueprint sinh ra nhiều ExamVersion.  
- 1 ExamVersion dùng cho nhiều Attempt.  
- 1 Attempt có nhiều AttemptAnswer → chấm ra AttemptScore.

---

## 5. Luồng nghiệp vụ chính

### Luồng A — Giáo viên dựng bank & ma trận

1. Tạo/import câu hỏi + gắn metadata.  
2. ContentAdmin duyệt (nếu bank chung).  
3. Tạo Blueprint từ template hoặc bảng trống.  
4. Hệ thống báo tồn kho theo ô.  
5. Sinh ExamVersion → preview → xuất bản.

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

## 7. Multi-tenant (nhẹ, để mở bán trung tâm)

- Mỗi Organization có bank riêng + (optional) được dùng bank chung platform.  
- Blueprint/Exam của org A không lộ sang org B.  
- Học sinh thuộc org hoặc mua gói B2C độc lập.

MVP có thể **single tenant** (chỉ bank của team) nhưng schema để `organization_id` nullable từ đầu — tránh rewrite.

---

## 8. Những gì chưa cần entity riêng lúc đầu

- Proctoring event (tab blur) — log đơn giản trên Attempt nếu làm.  
- Ranking season, badge, meme asset.  
- AI import job (làm sau dạng ImportJob).
