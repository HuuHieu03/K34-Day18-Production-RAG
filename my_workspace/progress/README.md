# 📊 Theo Dõi Tiến Độ Triển Khai (Progress Directory)

Thư mục `progress/` dùng để quản lý trạng thái thực thi thực tế của các công việc theo từng kế hoạch hoặc phiên bản, giúp người dùng và AI Agent kiểm soát tiến độ minh bạch.

---

## 🏷️ Quy Chuẩn Đặt Tên File

Mọi file theo dõi tiến độ phải tuân theo cấu trúc đặt tên:

```text
vX.Y.Z_<YYYY-MM-DD>_<topic>_progress.md
```

- `vX.Y.Z`: Phiên bản mục tiêu đồng bộ với file kế hoạch (ví dụ `v1.0.0`).
- `<YYYY-MM-DD>`: Ngày khởi tạo theo dõi tiến độ (ví dụ `2026-08-18`).
- `<topic>`: Chủ đề tương ứng với kế hoạch (ví dụ `hybrid_search`).
- `_progress.md`: Hậu tố cố định phân loại tài liệu tiến độ.

> **Ví dụ**: `v1.0.0_2026-08-18_hybrid_search_progress.md`

---

## 📋 Hướng Dẫn Sử Dụng

1. Tạo file mới từ [TEMPLATE_progress.md](file:///d:/tai%20lieu%20hoc%20tap/VinAI/Day18/Lap/K34-Day18-Production-RAG/my_workspace/progress/TEMPLATE_progress.md) khi bắt đầu thực hiện một kế hoạch mới.
2. Cập nhật YAML Frontmatter (đặc biệt là trường `status` chuyển dần từ `PLANNED` -> `IN_PROGRESS` -> `COMPLETED`).
3. Đánh dấu trạng thái các công việc bằng checklist markdown: `[x]` (hoàn thành) hoặc `[ ]` (chưa hoàn thành).
4. Ghi nhận ngay các trở ngại (blockers), vấn đề phát sinh và ghi chú quan trọng trong suốt quá trình triển khai.
