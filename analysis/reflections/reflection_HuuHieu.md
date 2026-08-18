# Individual Reflection — Lab 18

**Tên:** Huu Hieu  
**Module phụ trách:** M1, M2, M3, M4, M5 (Làm cá nhân)

---

## 1. Đóng góp kỹ thuật

- Module đã implement: M1 (Chunking), M2 (Search), M3 (Rerank), M4 (Eval), M5 (Enrichment).
- Các hàm/class chính đã viết: 
  - `chunk_hierarchical`, `chunk_semantic` (M1)
  - `HybridSearch` tích hợp `BM25Search`, `DenseSearch`, và `reciprocal_rank_fusion` (M2)
  - `CrossEncoderReranker.rerank` (M3)
  - `evaluate_ragas`, `failure_analysis` (M4)
  - `enrich_chunks` với chế độ `_enrich_single_call` (M5)
- Số tests pass: 32/32

## 2. Kiến thức học được

- Khái niệm mới nhất: Thuật toán RRF (Reciprocal Rank Fusion) để gộp kết quả tìm kiếm mà không cần chuẩn hóa scale của từng hệ thống phân tán độc lập.
- Điều bất ngờ nhất: Sự hiệu quả của Cross-Encoder Reranker. Chỉ cần thêm 1 bước chấm điểm lại, các tài liệu rác bay sạch khỏi top-k dù trước đó Dense Search chấm điểm rất cao.
- Kết nối với bài giảng (slide nào): Phần Architecture của RAG Sản Xuất (Bài 18). Ánh xạ chính xác từ lý thuyết Pipeline vào 5 module độc lập trong code.

## 3. Khó khăn & Cách giải quyết

- Khó khăn lớn nhất: Cấu hình môi trường và cài đặt các package (đặc biệt là tải các mô hình vài GB như BAAI/bge-reranker-v2-m3) dẫn đến timeout/đứng máy khi test.
- Cách giải quyết: Hủy tiến trình test bị kẹt, chủ động tải mô hình (pre-download) ở chế độ hiển thị tiến trình (progress bar) trong terminal. Viết mock data/fallback cho các hàm gọi LLM để test đi qua mượt mà.
- Thời gian debug: 2-3 giờ.

## 4. Nếu làm lại

- Sẽ làm khác điều gì: Sẽ tối ưu hóa hàm đánh giá RAGAS để chạy đa luồng (async) nhằm tiết kiệm thời gian eval cho các dataset lớn.
- Module nào muốn thử tiếp: Module 5 (Enrichment). Muốn tích hợp thêm Agent tự trị để sinh metadata tự động theo ontology sâu của doanh nghiệp.

## 5. Tự đánh giá

| Tiêu chí | Tự chấm (1-5) |
|----------|---------------|
| Hiểu bài giảng | 5 |
| Code quality | 5 |
| Teamwork | 5 |
| Problem solving | 5 |
