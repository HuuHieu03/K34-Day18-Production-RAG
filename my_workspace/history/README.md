# 📜 Lưu Trữ Lịch Sử Phiên & Bàn Giao Ngữ Cảnh (History Directory)

Thư mục `history/` đóng vai trò là "bộ nhớ dài hạn" của dự án, lưu trữ các báo cáo tóm tắt sau mỗi phiên làm việc nhằm đảm bảo việc chuyển giao và khôi phục ngữ cảnh (context handover) cho AI Agent và con người diễn ra liền mạch.

---

## 🏷️ Quy Chuẩn Đặt Tên File

Tùy theo tính chất của phiên làm việc, có thể lựa chọn 1 trong 2 định dạng đặt tên:

1. **Theo ngày làm việc (Session Summary)**:
   ```text
   YYYY-MM-DD_session_summary.md
   ```
   *Ví dụ*: `2026-08-18_session_summary.md`

2. **Theo phiên bản và tính năng (Feature History)**:
   ```text
   vX.Y.Z_<YYYY-MM-DD>_<topic>_history.md
   ```
   *Ví dụ*: `v1.0.0_2026-08-18_production_rag_history.md`

---

## 📋 Hướng Dẫn Sử Dụng

1. Cuối mỗi phiên làm việc, sao chép mẫu từ [TEMPLATE_history.md](file:///d:/tai%20lieu%20hoc%20tap/VinAI/Day18/Lap/K34-Day18-Production-RAG/my_workspace/history/TEMPLATE_history.md).
2. Điền đầy đủ thông tin vào khối YAML Frontmatter (`type: "history"`, `status: "COMPLETED"`).
3. Ghi lại cô đọng những gì đã làm, các quyết định quan trọng vừa thống nhất và hiện trạng chính xác của hệ thống.
4. Nêu rõ kế hoạch và các đầu mối công việc cần tiếp tục cho phiên làm việc tiếp theo.
