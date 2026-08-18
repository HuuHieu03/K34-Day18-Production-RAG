# 📜 Nguyên Tắc Hành Vi Cốt Lõi Cho AI Agent (Agent Rules)

Tài liệu này định nghĩa các nguyên tắc hành vi bắt buộc cho AI Agent khi tham gia vào quá trình phát triển, phân tích mã nguồn và bảo trì dự án.

---

## 🚫 1. Không Bịa Đặt Thông Tin (Zero Hallucination Policy)

- **Cơ sở thực tế (Fact-based only)**: AI Agent chỉ được phép đưa ra câu trả lời, nhận định hoặc giải pháp dựa trên dữ liệu thực tế đọc được trực tiếp từ kho mã nguồn (repository), file mã lệnh, tệp cấu hình hoặc tài liệu chính thức của dự án.
- **Không tự suy đoán vô căn cứ**: Khi thông tin bị thiếu, cấu hình không rõ ràng hoặc xuất hiện điểm mơ hồ, AI Agent **bắt buộc phải đặt câu hỏi làm rõ với người dùng** thay vì tự tiện suy diễn.
- **Trích dẫn nguồn cụ thể**: Khi giải thích logic hoặc nguyên nhân lỗi, phải chỉ rõ đường dẫn tệp tin và vị trí dòng lệnh tương ứng.

---

## ⚙️ 2. Quy Tắc Làm Việc & Kỹ Thuật (Working Standards)

1. **Tuân thủ cấu trúc `my_workspace/`**:
   - Mọi kế hoạch, tiến độ, lịch sử và nhật ký phải được lưu đúng thư mục tương ứng (`plans/`, `progress/`, `history/`, `logs/`).
   - Luôn sử dụng đúng chuẩn YAML Frontmatter và tuân thủ quy tắc đặt tên phiên bản.

2. **Minh bạch trước khi sửa đổi mã nguồn (Pre-action Transparency)**:
   - Trước khi thực hiện thay đổi mã nguồn, Agent phải giải thích rõ ràng lý do, phạm vi ảnh hưởng và giải pháp kỹ thuật dự kiến áp dụng.
   - Không thực hiện các thao tác phá vỡ cấu trúc có sẵn mà không có sự đồng thuận.

3. **Báo cáo trung thực & Minh bạch sau mỗi lần thử nghiệm (Post-action Transparency)**:
   - Sau khi chạy các lệnh kiểm thử (tests), benchmark hoặc đo lường hiệu năng, phải ghi nhận đầy đủ kết quả thực tế (thành công, thất bại, metric cụ thể) vào nhật ký `logs/`.
   - Tuyệt đối không che giấu lỗi hoặc báo cáo sai lệch kết quả đo đạc.

4. **Bảo toàn tính toàn vẹn của mã nguồn**:
   - Giữ nguyên các comment, docstring và quy ước phong cách code hiện có trừ khi có yêu cầu tái cấu trúc rõ ràng từ người dùng.
   - Viết mã nguồn sạch, có xử lý ngoại lệ cẩn thận và kèm theo kiểm thử đơn vị (unit tests) hoặc kiểm thử tích hợp phù hợp.

---

## 🧪 3. Quy Tắc Chuyên Biệt Cho Lab 18 (Production RAG)

1. **Nguyên tắc triển khai từng bước (Step-by-step Execution)**:
   - Tuyệt đối **KHÔNG** implement toàn bộ các module cùng một lúc.
   - Bắt buộc phải thực hiện và hoàn thành dứt điểm theo thứ tự tuần tự: `M1 (Chunking) → M2 (Search) → M3 (Rerank) → M4 (Eval) → M5 (Enrichment)`.

2. **Lý giải kỹ thuật & Thiết kế (Technical Reasoning)**:
   - Trước khi bắt tay vào code bất kỳ module nào, AI Agent phải phân tích yêu cầu, giải thích rõ logic, công thức hoặc thuật toán sẽ sử dụng (ví dụ: thuật toán phân mảnh Semantic, công thức tính điểm RRF, lý do chọn Cross-Encoder v.v.).
   - Chỉ tiến hành chỉnh sửa mã nguồn sau khi đã lý giải cặn kẽ và nhận được sự xác nhận.

3. **Tuân thủ quy trình kiểm thử của Lab (Lab Workflow Compliance)**:
   - **Baseline Test**: Bắt buộc phải chạy khởi tạo Docker (Qdrant) và `naive_baseline.py` ngay từ đầu để lấy điểm baseline, làm cơ sở đối chiếu sau này.
   - **Unit Testing**: Sau khi hoàn thành *MỖI* module, phải chạy command test tương ứng (ví dụ: `pytest tests/test_m1.py -v`). **Chỉ chuyển sang làm module tiếp theo khi test đạt Pass 100%**.
   - **Zero TODOs**: Quá trình implement phải giải quyết triệt để và xóa sạch mọi thẻ `# TODO` trong code.
   - **End-to-End Test & Analysis**: Bước cuối cùng là chạy toàn bộ luồng pipeline (`python src/pipeline.py`), trích xuất báo cáo RAGAS và **bắt buộc** phải thực hiện phân tích lỗi (Failure Analysis) chi tiết.

4. **Môi Trường Thực Thi & Quản Lý Gói (`uv` & `.venv`)**:
   - **Quản lý package bằng `uv`**: Sử dụng `uv` cho mọi tác vụ cài đặt thư viện và môi trường (`uv venv`, `uv pip install -r requirements.txt`, `uv pip install ...`).
   - **Thực thi trên môi trường ảo `.venv`**: Mọi lệnh chạy Python, kiểm thử tự động (`pytest`), benchmark hay pipeline bắt buộc phải được kích hoạt và thực thi trên môi trường ảo `.venv` của dự án (thông qua `uv run ...` hoặc đường dẫn python của `.venv`).
   - Không cài đặt dependencies ra môi trường Python global để tránh xung đột phiên bản.
