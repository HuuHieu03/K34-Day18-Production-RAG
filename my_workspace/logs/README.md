# 🪵 Nhật Ký Thực Thi & Xử Lý Sự Cố (Logs Directory)

Thư mục `logs/` dùng để ghi lại toàn bộ chi tiết kỹ thuật trong quá trình thực thi, bao gồm lệnh chạy, log output, nhật ký gỡ lỗi (troubleshooting) và kết quả đo lường benchmark/nghiệm thu.

---

## 🏷️ Quy Chuẩn Đặt Tên File

Mọi file nhật ký thực thi phải tuân theo cấu trúc đặt tên:

```text
vX.Y.Z_<YYYY-MM-DD>_<topic>_log.md
```

- `vX.Y.Z`: Phiên bản tương ứng (ví dụ `v1.0.0`).
- `<YYYY-MM-DD>`: Ngày thực thi ghi log (ví dụ `2026-08-18`).
- `<topic>`: Chủ đề của phiên chạy (ví dụ `production_rag`, `milvus_indexing`, `rerank_benchmark`).
- `_log.md`: Hậu tố cố định phân loại tài liệu nhật ký.

> **Ví dụ**: `v1.0.0_2026-08-18_production_rag_log.md`

---

## 📋 Hướng Dẫn Sử Dụng

1. Tạo file nhật ký mới từ [TEMPLATE_log.md](file:///d:/tai%20lieu%20hoc%20tap/VinAI/Day18/Lap/K34-Day18-Production-RAG/my_workspace/logs/TEMPLATE_log.md) khi tiến hành chạy thử nghiệm hoặc gỡ lỗi kỹ thuật.
2. Cập nhật khối YAML Frontmatter (`type: "log"`, `status: "COMPLETED"` hoặc `IN_PROGRESS`).
3. Ghi lại các bước thực hiện tuần tự kèm lệnh terminal và output quan trọng.
4. Khi gặp lỗi, ghi chi tiết theo cấu trúc chuẩn: **Triệu chứng (Symptom)**, **Nguyên nhân gốc rễ (Root Cause)**, và **Giải pháp khắc phục (Fix / Solution)**.
5. Tổng hợp các số liệu đo lường, kết quả benchmark hoặc nghiệm thu vào phần cuối.
