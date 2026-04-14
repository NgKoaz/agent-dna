# Cẩm Nang Viết Commit Message (Conventional Commits)

Để tự động hóa quá trình quản lý lịch sử code, dự án tuân thủ theo chuẩn **Conventional Commits**. Một tiêu đề commit chuẩn cần được viết theo định dạng sau:

```text
<type>(<scope>): <short description>
```

---

## 1. Phân Loại Commit (`<type>`)

### 🔴 Nhóm Thay Đổi Chính (Core Changes)
Ảnh hưởng trực tiếp đến chức năng ứng dụng dành cho người dùng.
- **`feat` (feature)**: Thêm một tính năng mới.
- **`fix` (bug fix)**: Vá lỗi/bug.
- **`perf` (performance)**: Cải thiện hiệu suất tính toán xử lý (nhanh hơn, tối ưu bộ nhớ hơn).

### 🛠 Nhóm Bảo Trì & Cấu Trúc (Maintenance)
Không làm thay đổi tính năng người dùng nhìn thấy, nhưng giúp mã nguồn sạch hơn.
- **`refactor`**: Cải thiện, tái cấu trúc lại mã nguồn mà không sửa lỗi hay thêm tính năng (VD: đổi tên biến, chia tách logic hàm).
- **`style`**: Các vấn đề thuần túy về mặt hình thức định dạng code (khoảng trắng, dấu chấm phẩy...).
- **`test`**: Bổ sung hoặc chỉnh sửa các bài kiểm thử tự động (Unit Test, Integration Test).
- **`build`**: Cập nhật hệ thống Build tool/Package Manager hoặc cập nhật thư viện phụ thuộc.
- **`ci`**: Cấu hình quy trình Continuous Integration (GitHub Actions, Gitlab CI, Jenkins).

### 📋 Nhóm Thông Tin & Khác (Utility)
- **`docs` (documentation)**: Bổ sung/Cập nhật các tài liệu văn bản (hướng dẫn README, comments trong code).
- **`chore`**: Các tác vụ lặt vặt không xếp vào nhóm trên (VD: Sửa lỗi syntax nhỏ, cập nhật `.gitignore`...).
- **`revert`**: Commit lùi lại (Hoàn tác) một commit đã push trước đó.

---

## 2. Các Ví Dụ Thực Tế
- `feat(auth): add Google login support` (Thêm tính năng đăng nhập Google)
- `fix(ui): resolve overlapping button on mobile` (Sửa lỗi nút bị đè)
- `docs: update installation instructions` (Cập nhật file HDSD cài đặt)

---

## 3. Hướng Dẫn Push "Khối Dữ Liệu Lớn"
*Mặc dù cực kỳ khuyến khích chia nhỏ commit (Atom commits), nhưng nếu bạn thiết kế / code nhanh và gom toàn bộ khối lượng vào đẩy lên 1 lượt, vui lòng tuân thủ:*

- **`feat: initial commit`** hoặc **`feat: complete microservice structure`**: Sử dụng cho lần khởi tạo đẩy trọn vẹn bộ khung thư mục ban đầu.
- **`feat: implement core MVP for [tên-dịch-vụ]`**: Đẩy code nguyên một cụm tính năng thô đầu tiên đủ để chạy được (MVP).
- **`feat: squash all features into one`**: Đẩy dồn nhiều thay đổi vào 1 pack không phân chia.
- **`wip` (Work In Progress)**: Đẩy nháp lên môi trường server để lưu trữ an toàn (hành trang trước khi làm tiếp ở máy khác).

> [!TIP]
> **LỜI KHUYÊN KHI CODE TỰ KHẢO (VIBE CODE)**
> Dù tốc độ code của bạn siêu nhanh thì ít nhất cũng nên cố gắng tách nhỏ theo chu kỳ cơ bản (3 nhịp):
> 1. `feat: init project and boilerplate` (Dựng lại cấu trúc rỗng)
> 2. `feat: core logic and database` (Xử lý toàn bộ DB và tính toán)
> 3. `feat: final touch and docs` (Thoát code, fix bug cuối và ghi chú)
> 
> Nhờ 3 nhịp dứt điểm này, mai sau nếu có điểm gãy (crash) hệ thống, bạn sẽ khoanh vùng được chính xác lỗi đang thuộc "cục" nào.
