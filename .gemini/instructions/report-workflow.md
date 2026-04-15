# Workflow: Quy trình báo cáo tiến độ (Reporting)

Quy trình này đảm bảo tính minh bạch, trung thực và chuyên nghiệp trong việc quản lý tiến độ dự án.

## Các bước thực hiện sau mỗi giai đoạn (Stage)

### 1. Cập nhật Danh sách công việc (Tasks)
- Mở file `docs/tasks.md`.
- Đánh dấu `[x]` vào các đầu việc đã hoàn thành trong giai đoạn vừa thực hiện.

### 2. Viết báo cáo tiến độ chi tiết (Progress Report)
- Sử dụng Skill: **`report-digitech-company-work-progress` ở `.gemini\skills\report-digitech-company-work-progress\SKILL.md`**.
- Ghi đè hoặc cập nhật vào file `docs/report.md`.
- Nội dung phải bao gồm 6 phần bắt buộc (Phần nào không có thì có thể để trống, thường thì 5, 6 có thể trống nhiều):
    1. **MÔ TẢ CÔNG VIỆC (WHAT)**: Mục tiêu của giai đoạn.
    2. **NỘI DUNG CẦN THỰC HIỆN (HOW)**: Cách tiếp cận kỹ thuật.
    3. **QUÁ TRÌNH THỰC HIỆN**: Các bước chia nhỏ và thời gian ước tính (Thực tế).
    4. **FILE CHANGES**: Danh sách tệp tin thay đổi/tạo mới.
    5. **PR**: Nhánh làm việc (Branch).
    6. **SELFTEST + KẾT QUẢ**: Chứng minh code đã chạy đúng.

### 3. Đồng bộ hóa Tổng quan (Overview - Tùy chọn)
- Nếu giai đoạn vừa xong mang lại thay đổi lớn về lộ trình hoặc kiến trúc, hãy cập nhật lại file `docs/overview.md` để đảm bảo cái nhìn tổng thể luôn đúng.

### 4. Tạo Git Commit Message
- Sau khi báo cáo, hãy xem xét các tệp tin thay đổi (Tách biệt các tệp logic/code với các tệp tài liệu/docs).
- Cung cấp sẵn một câu lệnh `git commit` chuẩn (Conventional Commits) cho các thay đổi code để người dùng có thể copy và thực thi nhanh chóng.
- Tuân thủ chuẩn **Conventional Commits** trong `.github/COMMIT_CONVENTION.md`.
- Sử dụng nhiều flag `-m` để tách biệt Tiêu đề và Nội dung chi tiết nếu commit gom nhiều thay đổi lớn.

## Nguyên tắc báo cáo
- **Trung thực**: Ghi rõ cả các bước giả lập (Mock) hoặc các lỗi phát sinh.
- **Scannable**: Sử dụng Bold và Bullet points để người quản lý dễ dàng lướt nhanh nội dung.
- **Tiêu chuẩn**: Luôn tham chiếu đến các file Skill và Convention trong thư mục `.gemini` và `.github`.
