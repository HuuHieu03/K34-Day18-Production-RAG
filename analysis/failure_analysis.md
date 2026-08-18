# Báo Cáo Phân Tích Lỗi (Failure Analysis) - Lab 18

Trong quá trình đánh giá bằng RAGAS, chúng ta đã phát hiện một số câu hỏi có kết quả trả lời không tốt. Dựa trên 4 metrics cốt lõi, dưới đây là phân tích nguyên nhân và đề xuất hướng khắc phục (dựa trên Diagnostic Tree).

## 1. Vấn đề liên quan đến `Context Recall` thấp
- **Biểu hiện**: Hệ thống không tìm thấy đủ các chunks chứa thông tin cần thiết.
- **Chẩn đoán**: Lỗi nằm ở bước Retrieval. Thuật toán tìm kiếm (Dense Search) có thể không bắt được các keyword chính xác.
- **Khắc phục**: Áp dụng Hybrid Search (kết hợp BM25) để bắt chính xác các keyword/tên riêng, và/hoặc cải thiện chiến lược Chunking (Semantic/Hierarchical).

## 2. Vấn đề liên quan đến `Context Precision` thấp
- **Biểu hiện**: Các chunks đúng bị xếp hạng thấp, trong khi chunks rác bị đẩy lên trên.
- **Chẩn đoán**: Quá nhiều thông tin nhiễu lọt vào kết quả tìm kiếm sơ bộ (Top 20).
- **Khắc phục**: Đưa vào mô hình Reranker (Cross-Encoder) chấm điểm chéo lại giữa query và từng chunk để đẩy chunk liên quan lên Top-K (Ví dụ: dùng `BAAI/bge-reranker-v2-m3`).

## 3. Vấn đề liên quan đến `Faithfulness` thấp
- **Biểu hiện**: LLM tự bịa ra thông tin (hallucination) không có trong Context.
- **Chẩn đoán**: LLM bỏ qua chỉ thị "Chỉ trả lời dựa trên context".
- **Khắc phục**: Cần siết chặt lại Prompt Template, dặn dò gắt gao hơn ("NẾU KHÔNG CÓ TRONG CONTEXT THÌ NÓI TÔI KHÔNG BIẾT"), đồng thời hạ tham số `temperature` của LLM xuống 0.

## 4. Vấn đề liên quan đến `Answer Relevancy` thấp
- **Biểu hiện**: Câu trả lời không khớp với câu hỏi (hỏi gà đáp vịt).
- **Chẩn đoán**: Câu hỏi từ user quá mơ hồ hoặc hệ thống RAG không có đủ context phù hợp nên LLM trả lời chung chung.
- **Khắc phục**: Áp dụng Data Enrichment (HyQA - sinh câu hỏi giả định trước khi embed) hoặc dùng Query Reformulation để làm rõ ý của user trước khi Search.
