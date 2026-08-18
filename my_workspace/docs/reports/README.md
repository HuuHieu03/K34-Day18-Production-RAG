# 📑 Quản Lý Báo Cáo Dự Án (Reports Directory)

Thư mục `docs/reports/` chịu trách nhiệm lưu trữ các báo cáo kỹ thuật, báo cáo tổng quan dự án (project overview), báo cáo phân tích kiến trúc, benchmark và các báo cáo chuyên đề theo yêu cầu.

---

## 🏷️ Quy Chuẩn Đặt Tên File

Mọi file báo cáo mới phải được đặt tên theo một trong hai quy chuẩn:

1. **Báo cáo theo phiên bản & tính năng**:
   ```text
   vX.Y.Z_<YYYY-MM-DD>_<topic>_report.md
   ```
   *Ví dụ*: `v1.0.0_2026-08-18_project_overview_report.md`

2. **Báo cáo theo ngày thực hiện**:
   ```text
   YYYY-MM-DD_<topic>_report.md
   ```
   *Ví dụ*: `2026-08-18_retrieval_performance_report.md`

- `vX.Y.Z`: Phiên bản mục tiêu (nếu gắn liền với release/milestone).
- `<YYYY-MM-DD>`: Ngày lập báo cáo theo định dạng chuẩn ISO.
- `<topic>`: Chủ đề báo cáo (ví dụ: `project_overview`, `rag_pipeline_audit`, `latency_analysis`).
- `_report.md`: Hậu tố cố định phân loại tài liệu báo cáo.

---

## 📋 Hướng Dẫn Sử Dụng

1. Sao chép nội dung từ [TEMPLATE_report.md](file:///d:/tai%20lieu%20hoc%20tap/VinAI/Day18/Lap/K34-Day18-Production-RAG/my_workspace/docs/reports/TEMPLATE_report.md) khi tạo báo cáo mới.
2. Điền đầy đủ thông tin vào khối YAML Frontmatter ở đầu file (`type: "report"`, `status: "COMPLETED"` hoặc `DRAFT`).
3. Trình bày nội dung trực quan, có biểu đồ / bảng số liệu minh họa và trích dẫn rõ ràng từ mã nguồn hoặc dữ liệu thực tế.
4. Đưa ra các đánh giá khách quan và đề xuất cải tiến cụ thể.
