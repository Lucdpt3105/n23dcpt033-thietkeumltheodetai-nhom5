# Phân Tích Sơ Đồ Lớp (Class Diagram) - Hệ Thống Thi Trực Tuyến

Sơ đồ này mô tả cấu trúc tĩnh của hệ thống, bao gồm các lớp đối tượng chính, các thuộc tính (attributes), phương thức (methods) của chúng, và mối quan hệ giữa các lớp đó.

---

##  Danh sách các lớp và mô tả

### 1. User
Lớp cơ sở (base class) đại diện cho một người dùng chung của hệ thống.
- **Thuộc tính:**
  - `userID`: Định danh duy nhất.
  - `name`: Tên người dùng.
  - `email`: Email đăng nhập.
  - `role`: Vai trò (ví dụ: 'student', 'teacher').
- **Phương thức:**
  - `LoginWithZalo()`: Đăng nhập bằng tài khoản Zalo.
  - `updateProfileDate()`: Cập nhật thông tin cá nhân.

### 2. Teacher
Lớp kế thừa từ `User`, đại diện cho giáo viên. Giáo viên có quyền tạo và quản lý các kỳ thi.
- **Thuộc tính:**
  - `department`: Khoa/Bộ môn.
  - `teacherId`: Mã số giáo viên.
- **Phương thức:**
  - `createExam()`: Tạo một kỳ thi mới.
  - `editExam()`: Chỉnh sửa thông tin kỳ thi.
  - `addQuestion()`: Thêm câu hỏi vào kỳ thi.
  - `importFromExcel()`: Nhập danh sách câu hỏi từ file Excel.

### 3. Student
Lớp kế thừa từ `User`, đại diện cho học sinh/sinh viên. Sinh viên có quyền tham gia làm bài thi.
- **Thuộc tính:**
  - `classId`: Mã lớp học.
  - `studentId`: Mã số sinh viên.
- **Phương thức:**
  - `viewExamList()`: Xem danh sách các kỳ thi có thể tham gia.
  - `startExam()`: Bắt đầu làm bài thi.
  - `submitExam()`: Nộp bài thi.
  - `viewResult()`: Xem kết quả bài thi đã làm.

### 4. Exam
Đại diện cho một kỳ thi hoặc bài kiểm tra.
- **Thuộc tính:**
  - `examId`: ID của kỳ thi.
  - `title`: Tiêu đề kỳ thi.
  - `subject`: Môn học.
  - `type`: Loại kỳ thi (trắc nghiệm, tự luận).
  - `durationMinutes`: Thời gian làm bài (phút).
  - `startAt`, `endAt`: Thời gian bắt đầu và kết thúc kỳ thi.
  - `status`: Trạng thái (đang mở, đã đóng).
- **Phương thức:**
  - `addQuestion()`: Thêm câu hỏi vào đề thi.
  - `validate()`: Kiểm tra tính hợp lệ của kỳ thi.

### 5. QuestionBank
Đại diện cho ngân hàng câu hỏi, nơi lưu trữ các câu hỏi.
- **Thuộc tính:**
  - `bankId`: ID ngân hàng.
  - `ownerId`: ID của người sở hữu (giáo viên).
  - `name`: Tên ngân hàng câu hỏi.
- **Phương thức:**
  - `search()`: Tìm kiếm câu hỏi theo tiêu chí.
  - `addQuestion()`: Thêm câu hỏi mới vào ngân hàng.

### 6. Choices
Đại diện cho các lựa chọn đáp án của một câu hỏi trắc nghiệm.
- **Thuộc tính:**
  - `choiceId`: ID của lựa chọn.
  - `questionId`: ID của câu hỏi chứa lựa chọn này.
  - `text`: Nội dung của lựa chọn.
  - `isCorrect`: Đánh dấu đây có phải là đáp án đúng không.
- **Phương thức:**
  - `method()`: (Phương thức mẫu, cần định nghĩa rõ hơn).

### 7. Attempt
Lưu lại một lượt làm bài của sinh viên cho một kỳ thi cụ thể.
- **Thuộc tính:**
  - `attemptId`: ID của lượt làm bài.
  - `examId`, `studentId`: Khóa ngoại đến Kỳ thi và Sinh viên.
  - `startedAt`, `lastSavedAt`, `finishedAt`: Các mốc thời gian làm bài.
  - `status`: Trạng thái (đang làm, đã nộp).
  - `score`: Điểm số cuối cùng.
- **Phương thức:**
  - `saveTempAnswer()`: Lưu câu trả lời tạm thời.
  - `finalizeAndScore()`: Hoàn tất và chấm điểm.

### 8. Answer
Lưu câu trả lời cụ thể của sinh viên cho một câu hỏi trong một lượt làm bài.
- **Thuộc tính:**
  - `answerId`: ID câu trả lời.
  - `attemptId`, `questionId`, `choiceId`: Các khóa ngoại liên quan.
  - `answerText`: Nội dung câu trả lời (cho câu hỏi tự luận).
  - `isMarked`, `isAutoMarked`: Trạng thái chấm điểm.
  - `score`, `autoMarkScore`: Điểm số.
  - `feedback`: Nhận xét của giáo viên.

### 9. Result
Lưu kết quả tổng hợp của một lượt làm bài sau khi đã chấm xong.
- **Thuộc tính:**
  - `resultId`: ID kết quả.
  - `attemptId`: Khóa ngoại đến lượt làm bài.
  - `totalScore`: Tổng điểm.
  - `rank`: Xếp hạng.
  - `generatedAt`: Thời điểm tạo kết quả.

### 10. Notification
Đại diện cho một thông báo gửi đến người dùng.
- **Thuộc tính:**
  - `notificationId`: ID thông báo.
  - `userId`: ID người nhận.
  - `type`: Loại thông báo.
  - `status`: Trạng thái (đã đọc, chưa đọc).
  - `sendAt`: Thời gian gửi.
- **Phương thức:**
  - `send()`: Gửi thông báo.

---

## Phân Tích Mối Quan Hệ

1.  **Kế thừa (Inheritance):**
    - `Teacher` và `Student` là các lớp con, kế thừa từ lớp cha `User`. Điều này thể hiện cả hai đều là người dùng nhưng có thêm các thuộc tính và hành vi riêng.

2.  **Association (Quan hệ kết hợp):**
    - **Teacher ↔ Exam:** Một `Teacher` có thể tạo và quản lý nhiều `Exam`. Một `Exam` được tạo bởi một `Teacher`.
    - **Student ↔ Attempt:** Một `Student` có thể có nhiều `Attempt` (lượt làm bài). Mỗi `Attempt` thuộc về duy nhất một `Student`.
    - **Exam ↔ Attempt:** Một `Exam` có thể có nhiều `Attempt` từ các sinh viên khác nhau.
    - **Attempt ↔ Answer:** Một `Attempt` bao gồm nhiều `Answer` (câu trả lời).
    - **Attempt → Result:** Mỗi `Attempt` sau khi hoàn tất sẽ có một `Result` tương ứng.
    - **Teacher ↔ QuestionBank:** Một `Teacher` sở hữu và quản lý một `QuestionBank`.

3.  **Aggregation (Quan hệ tập hợp - "has-a"):**
    - **Exam <> Choices:** Một `Exam` chứa một tập hợp các `Choices` (lựa chọn cho các câu hỏi). Các `Choices` có thể tồn tại độc lập với `Exam`.

4.  **Dependency (Quan hệ phụ thuộc):**
    - **Teacher --- > Notification:** Lớp `Teacher` sử dụng lớp `Notification` (thể hiện qua đường nét đứt). Ví dụ, hệ thống có thể gửi thông báo khi giáo viên tạo xong bài thi.
