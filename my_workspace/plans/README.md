# 🗺️ Quản Lý Kế Hoạch Kỹ Thuật (Plans Directory)

Thư mục `plans/` chịu trách nhiệm lưu trữ các bản thiết kế kiến trúc, đề xuất kỹ thuật và kế hoạch triển khai chi tiết theo từng phiên bản của dự án.

---

## 🏷️ Quy Chuẩn Đặt Tên File

Mọi kế hoạch mới phải được đặt tên theo mẫu:

```text
vX.Y.Z_<YYYY-MM-DD>_<topic>_plan.md
```

- `vX.Y.Z`: Phiên bản mục tiêu (Semantic Versioning, ví dụ `v1.0.0`, `v1.1.0`).
- `<YYYY-MM-DD>`: Ngày lập kế hoạch theo định dạng chuẩn (ví dụ `2026-08-18`).
- `<topic>`: Chủ đề ngắn gọn mô tả tính năng/module (ví dụ `hybrid_search`, `reranking_pipeline`, `cache_layer`).
- `_plan.md`: Hậu tố cố định phân loại tài liệu.

> **Ví dụ**: `v1.0.0_2026-08-18_hybrid_search_plan.md`

---

## 📋 Hướng Dẫn Sử Dụng

1. Sao chép nội dung từ [TEMPLATE_plan.md](file:///d:/tai%20lieu%20hoc%20tap/VinAI/Day18/Lap/K34-Day18-Production-RAG/my_workspace/plans/TEMPLATE_plan.md) khi bắt đầu một kế hoạch mới.
2. Điền đầy đủ thông tin vào khối YAML Frontmatter ở đầu file.
3. Phân tích chi tiết kiến trúc, các quyết định kỹ thuật và lộ trình thực thi theo các giai đoạn (Phases).
4. Xác định rõ ràng kế hoạch kiểm thử (Verification Plan) trước khi chuyển sang giai đoạn thực thi mã nguồn.
