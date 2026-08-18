# Báo Cáo Phân Tích Lỗi (Failure Analysis) - Lab 18

Phân tích bottom-5 câu hỏi có điểm RAGAS thấp nhất dựa trên Error Tree.

## 1. Câu hỏi: Quy định về thời gian nghỉ thai sản cho nam giới là bao nhiêu?
- **Answer có đúng ground truth không?**: Không. LLM trả lời thời gian của nữ.
- **Context có chứa bằng chứng cần thiết không?**: Không (Thiếu thông tin).
- **Lỗi ở đâu (Chunk/Retrieval)?**: M2 Retrieval (Dense Search) tìm ra các chunk về "nghỉ thai sản" nhưng bỏ sót keyword "nam giới". 
- **Đề xuất (Suggested fix)**: Tăng trọng số của thuật toán BM25 trong Hybrid Search để ưu tiên exact match từ khóa "nam". Có thể viết test kiểm tra điểm BM25 cho từ "nam".

## 2. Câu hỏi: Ai là người phê duyệt ngân sách phòng ban Marketing?
- **Answer có đúng ground truth không?**: Không. LLM bịa ra "Giám đốc Marketing".
- **Context có chứa bằng chứng cần thiết không?**: Có.
- **Lỗi ở đâu (Generation)?**: Context đúng nhưng Answer sai (Faithfulness thấp). LLM bỏ qua chỉ thị "chỉ dựa trên context".
- **Đề xuất (Suggested fix)**: Sửa lại Prompt Template mạnh tay hơn (Ví dụ: "NẾU KHÔNG THẤY TRONG CONTEXT, HÃY TRẢ LỜI KHÔNG BIẾT"). Hạ `temperature` của LLM xuống 0. Kiểm tra lại bằng RAGAS Eval ở lần tiếp theo.

## 3. Câu hỏi: Form đăng ký nghỉ phép nằm ở thư mục nào?
- **Answer có đúng ground truth không?**: Không.
- **Context có chứa bằng chứng cần thiết không?**: Không.
- **Lỗi ở đâu (Chunk/Retrieval)?**: M1 Chunking cắt ngang bảng biểu (table) đường dẫn thư mục khiến thông tin bị nát.
- **Đề xuất (Suggested fix)**: Chuyển sang Structure-Aware Chunking (Markdown/HTML) thay vì cắt theo ký tự để giữ nguyên bảng biểu đường dẫn.

## 4. Câu hỏi: Chi phí tối đa cho một chuyến công tác nội địa là bao nhiêu?
- **Answer có đúng ground truth không?**: Không. LLM trả lời chung chung "tuỳ thuộc vào cấp bậc".
- **Context có chứa bằng chứng cần thiết không?**: Có chứa nhiều chunks liên quan nhưng bị loãng.
- **Lỗi ở đâu (Retrieval/Reranking)?**: M3 Reranking không đẩy chunk chứa con số cụ thể lên Top 1 (Context Precision thấp).
- **Đề xuất (Suggested fix)**: Thêm Contextual Prepend ở M5 (Enrichment) để ghi rõ "Quy định công tác nội địa năm 2024" vào đầu chunk, giúp Reranker nhận diện chính xác hơn.

## 5. Câu hỏi: Sự khác biệt giữa bảo hiểm PVI và bảo hiểm y tế cơ bản là gì?
- **Answer có đúng ground truth không?**: Một nửa.
- **Context có chứa bằng chứng cần thiết không?**: Thiếu thông tin về bảo hiểm PVI.
- **Lỗi ở đâu (Chunk/Retrieval)?**: Do câu hỏi mang tính so sánh, M2 Search không tìm được chunk nào có cả 2 keyword cùng lúc (Context Recall thấp).
- **Đề xuất (Suggested fix)**: Áp dụng HyQA (Module 5) sinh các câu hỏi so sánh giả định trước khi embed. Lần eval tiếp theo sẽ đo lại điểm Recall.
