# Bài Thu Hoạch (Reflection) - Lab 18: Production RAG

**Học viên:** Huu Hieu

## 1. So sánh Naive RAG và Production RAG
Thông qua quá trình triển khai thực tế, tôi nhận thấy Naive RAG tồn tại rất nhiều điểm yếu so với kiến trúc RAG Sản xuất (Production RAG):
- **Chunking**: Naive RAG chia văn bản một cách cơ bản theo độ dài ký tự cố định, dễ dẫn đến tình trạng cắt ngang câu hoặc làm mất hoàn toàn ngữ cảnh. Trong khi đó, Production RAG dùng các chiến lược Hierarchical, Semantic và Structure-aware Chunking giúp bảo toàn trọn vẹn ngữ nghĩa của văn bản.
- **Tìm kiếm (Retrieval)**: Naive RAG chỉ sử dụng Vector Search (Dense), dễ bị thiếu nhạy bén với các từ khóa cụ thể (như mã nhân viên, số điện thoại, tên riêng). Production RAG áp dụng Hybrid Search (kết hợp BM25 + Dense) và dùng thuật toán RRF để gom ưu điểm của cả hai, giúp tìm kiếm bao quát hơn.
- **Xếp hạng lại (Reranking)**: Bằng cách thêm mô hình Cross-Encoder ở bước cuối cùng, Production RAG có khả năng loại bỏ hiệu quả các nhiễu loạn trong kết quả tìm kiếm, đưa thông tin liên quan nhất lên vị trí top đầu để trao cho LLM.

## 2. Bài học về Data Enrichment
Thay vì nhét trực tiếp các "raw chunk" vào Vector Database, việc "làm giàu" dữ liệu bằng LLM trước khi lưu trữ tạo ra sự khác biệt cực kỳ lớn:
- **Tóm tắt (Summarize)**: Giúp embed các vector gọn gàng và đánh trọng tâm vào nội dung chính, ít nhiễu.
- **HyQA (Hypothetical QA)**: Là một kỹ thuật vô cùng thông minh giúp nối liền "khoảng cách từ vựng" giữa câu hỏi tự nhiên của người dùng và văn bản cứng nhắc trong tài liệu.
- **Contextual Prepend**: Giải quyết triệt để vấn đề "mất bối cảnh" của các đoạn chunk ngắn, đặc biệt hữu ích khi xử lý tài liệu lớn.

## 3. Đánh giá chất lượng với RAGAS
Việc "cảm nhận bằng mắt" xem RAG trả lời đúng hay sai là cách làm thủ công và không thể nhân rộng. Sử dụng RAGAS với 4 thang đo độc lập (Faithfulness, Answer Relevancy, Context Precision, Context Recall) giúp định lượng bằng những con số rõ ràng để phân biệt lỗi do khâu nào (do Search kém hay do LLM trả lời kém). Từ đó, tôi có thể dễ dàng tra cứu Diagnostic Tree để tinh chỉnh lại.

## 4. Kế hoạch ứng dụng
Tôi dự định sẽ áp dụng ngay kỹ thuật Hybrid Search + Reranker vào các ứng dụng RAG trong tương lai để tối ưu độ chính xác. Ngoài ra, việc học được cách áp dụng "Combined Single-Call" ở bước Data Enrichment cũng giúp tôi nhận ra tầm quan trọng của việc tối ưu hóa chi phí API (chỉ gọi 1 lần để sinh nhiều trường dữ liệu) trước khi triển khai hệ thống vào thực tế.
