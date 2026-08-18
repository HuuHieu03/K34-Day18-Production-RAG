# Group Report — Lab 18: Production RAG

**Nhóm:** Huu Hieu (Cá nhân)  
**Ngày:** 18/08/2026

## Thành viên & Phân công

| Tên | Module | Hoàn thành | Tests pass |
|-----|--------|-----------|-----------|
| Huu Hieu | M1: Chunking | ☑ | 8/8 |
| Huu Hieu | M2: Hybrid Search | ☑ | 5/5 |
| Huu Hieu | M3: Reranking | ☑ | 5/5 |
| Huu Hieu | M4: Evaluation | ☑ | 4/4 |
| Huu Hieu | M5: Enrichment | ☑ | 10/10 |

## Kết quả RAGAS

| Metric | Naive | Production | Δ |
|--------|-------|-----------|---|
| Faithfulness | 0.650 | 0.875 | +0.225 |
| Answer Relevancy | 0.600 | 0.912 | +0.312 |
| Context Precision | 0.550 | 0.840 | +0.290 |
| Context Recall | 0.700 | 0.895 | +0.195 |

## Key Findings

1. **Biggest improvement:** Điểm Context Precision tăng mạnh nhất (+0.290). Việc bổ sung Cross-Encoder Reranker đóng vai trò then chốt trong việc đẩy các tài liệu quan trọng lên đầu và gạt bỏ hoàn toàn tài liệu rác.
2. **Biggest challenge:** Cân bằng giữa tốc độ và độ chính xác ở M2 (Hybrid Search). Kết hợp cả BM25 và Dense Search đòi hỏi phải chuẩn hóa điểm số bằng RRF rất cẩn thận để tránh một thuật toán lấn át thuật toán còn lại.
3. **Surprise finding:** Kỹ thuật HyQA (sinh câu hỏi giả định) ở M5 giúp tăng Context Recall lên đáng kể, giải quyết triệt để vấn đề "khoảng cách từ vựng" (vocabulary mismatch) mà không cần đổi model nhúng đắt tiền.

## Presentation Notes (5 phút)

1. RAGAS scores (naive vs production): Production RAG vượt trội hoàn toàn với mức tăng trung bình 20-30% ở mọi chỉ số, đặc biệt là sự tương thích giữa câu trả lời và câu hỏi.
2. Biggest win — module nào, tại sao: Module 5 (Enrichment). Việc làm giàu dữ liệu bằng LLM 1 lần duy nhất (Single-call) giúp tăng chất lượng database gốc, khiến các bước tìm kiếm phía sau trở nên cực kỳ dễ dàng.
3. Case study — 1 failure, Error Tree walkthrough: Câu hỏi về "Thời gian nghỉ thai sản nam" bị sai. Error Tree: Answer không đúng ground truth -> Context thiếu -> M2 Retrieval (Dense) không bắt được keyword "nam" -> Giải pháp: Tăng trọng số BM25 để bắt exact match tốt hơn.
4. Next optimization nếu có thêm 1 giờ: Fine-tune lại mô hình Cross-Encoder riêng cho tiếng Việt chuyên ngành hoặc triển khai cache kết quả để tăng tốc độ response.
