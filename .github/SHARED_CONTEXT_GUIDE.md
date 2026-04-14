# Shared AI Context: Integration & Workflow

Hướng dẫn này tập trung vào hai khía cạnh quan trọng nhất để vận hành hệ thống Kỹ năng AI dùng chung: **Tích hợp** và **Đồng bộ**.

---

## 1. Phương Pháp Tích Hợp (Integration)

Để không phải copy-paste thủ công và giữ cho dự án sạch sẽ, chúng ta sử dụng kỹ thuật **Git Submodule**. Cách này coi Repo Kỹ năng AI là một "phụ tùng" gắn vào dự án chính.

- **Lệnh thực hiện:** 
  ```bash
  git submodule add <URL_REPO_SKILLS> .shared-skills
  ```
- **Kết quả:** Thư mục `.shared-skills` sẽ xuất hiện trong dự án. Đây thực chất là một "cửa sổ" tham chiếu thẳng tới Repo Skills của bạn.
- **Lợi ích:** Tách biệt hoàn toàn mã nguồn nghiệp vụ và mã nguồn kỹ năng AI. Bạn có thể nâng cấp Agent mà không cần chạm vào logic của ứng dụng.

---

## 2. Quy Trình Vận Hành (Workflow)

Để hệ thống luôn "thông minh" một cách đồng bộ trên tất cả các dự án (iCa, Logistics, Orchestrator...), hãy tuân thủ quy trình 3 bước:

1.  **Cập nhật tại gốc:** Khi phát hiện một Prompt hay hoặc một quy tắc mới, hãy thực hiện chỉnh sửa duy nhất một lần tại Repo Skills gốc.
2.  **Đồng bộ tức thì:** Tại thư mục gốc của các dự án đang sử dụng, chạy lệnh:
    ```bash
    git submodule update --remote
    ```
3.  **Hưởng thụ thành quả:** Mọi dự án sẽ ngay lập tức áp dụng bộ kỹ năng mới nhất. Bạn không còn phải lo lắng về việc "quên" cập nhật quy tắc ở dự án này hay dự án nọ.

> [!IMPORTANT]
> Việc tách biệt Kỹ năng AI thành một thực thể độc lập giúp bạn quản lý "tri thức" của các Agent theo cách chuyên nghiệp và có hệ thống hơn.
