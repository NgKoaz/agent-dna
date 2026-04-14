# Skill: Link Agent DNA to Project

Dùng skill này khi cần liên kết dự án hiện tại với bộ tiêu chuẩn (DNA) của hệ thống.

## Context
Trên môi trường Windows, việc tạo Symbolic Link cho thư mục thường yêu cầu quyền Administrator. Để đơn giản hóa và cho phép AI tự thực hiện, chúng ta sử dụng `Junction`.

## Instructions for AI

1. **Verify Source**: Đảm bảo thư mục nguồn `D:\agent-dna` tồn tại.
2. **Clean-up**: Nếu dự án hiện tại đã có thư mục `.github` hoặc `.gemini` cục bộ (không phải link), hãy yêu cầu người dùng xác nhận xóa hoặc tự động xóa nếu chúng trống.
3. **Execute Link**: Chạy các lệnh PowerShell sau để tạo liên kết:
   ```powershell
   # Tạo link cho .github
   New-Item -ItemType Junction -Path ".github" -Target "D:\agent-dna\.github"

   # Tạo link cho .gemini
   New-Item -ItemType Junction -Path ".gemini" -Target "D:\agent-dna\.gemini"
   ```
4. **Git Ignore**: Đảm bảo đã cập nhật `.gitignore` để tránh commit các thư mục link này vào repo riêng của dự án:
   ```text
   .github
   .gemini
   .agents
   .claude
   ```

## Best Practices
- Ưu tiên dùng `Junction` thay cho `SymbolicLink` để tránh lỗi quyền hạn (Elevation Required).
- Luôn kiểm tra xem link đã tồn tại chưa (`Test-Path`) trước khi tạo mới để tránh lỗi `ResourceExists`.
