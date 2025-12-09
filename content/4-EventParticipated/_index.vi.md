---
title: "Sự kiện đã tham gia"
date: "2025-11-15"
weight: 1
chapter: false
pre: " <b> 4.3. </b> "
---

# Báo cáo tóm tắt: “Chuỗi làm chủ AWS Cloud #1 - AI/ML/GenAI trên AWS”

### Mục tiêu sự kiện

- Giới thiệu về AI/ML/GenAI trên AWS

### Diễn giả

- **Lam Tuan Kiet** – Kỹ sư DevOps cấp cao, FPT Software
- **Danh Hoang Hieu Nghi** - Kỹ sư AI, Renova Cloud
- **Dinh Le Hoang Anh** - Thực tập sinh Kỹ sư đám mây, First Cloud AI Journey
- **Van Hoang Kha** - Kỹ sư bảo mật đám mây, AWS Community Builder
### Những điểm nổi bật

# Khám phá Generative AI với Amazon Bedrock:

**- Các mô hình nền tảng (Foundation Models):** Khác với Mô hình truyền thống ở chỗ nó có thể thích ứng với nhiều tác vụ, cung cấp nhiều mô hình được quản lý hoàn toàn từ các công ty AI hàng đầu như: OpenAI, Claude, Anthropic, v.v.
**- Kỹ thuật gợi ý (Prompt Engineering):** Soạn thảo và tinh chỉnh các hướng dẫn
   + Zero-Shot Prompting: Lời nhắc không có ngữ cảnh hoặc ví dụ trước đó
   + Few-shot Prompting: Lời nhắc với một vài ngữ cảnh và ví dụ trước đó
   + Chuỗi suy nghĩ (Chain of Thought): Lời nhắc với các quy trình suy nghĩ và các bước để có câu trả lời thực tế
**- Retrieval Augmented Generation (RAG):** Truy xuất thông tin liên quan từ nguồn dữ liệu
   + R: Truy xuất (Retrieval) - Truy xuất thông tin liên quan từ cơ sở tri thức hoặc nguồn dữ liệu
   + A: Tăng cường (Augmented) - Thêm thông tin được truy xuất dưới dạng ngữ cảnh bổ sung vào lời nhắc của người dùng trước khi đưa vào mô hình
   + G: Tạo sinh (Generation) - Phản hồi từ mô hình cho lời nhắc đã được tăng cường
   + Các trường hợp sử dụng: Cải thiện chất lượng nội dung, chatbot theo ngữ cảnh và trả lời câu hỏi, tìm kiếm được cá nhân hóa và tóm tắt dữ liệu thời gian thực

**- Amazon Titan Embedding:** Mô hình hạng nhẹ vượt trội trong việc dịch văn bản thành các biểu diễn số (embeddings) cho các tác vụ truy xuất độ chính xác cao, hỗ trợ hơn 100 ngôn ngữ

**- Các dịch vụ AI được huấn luyện trước:**   + Amazon Rekognition: Phân tích hình ảnh và video
  + Amazon Translate: Phát hiện và dịch văn bản
  + Amazon Textract: Trích xuất văn bản và bố cục từ tài liệu
  + Amazon Transcribe: Chuyển đổi giọng nói thành văn bản
  + Amazon Polly: Chuyển đổi văn bản thành giọng nói
  + Amazon Comprehend: Trích xuất thông tin chi tiết và mối quan hệ từ văn bản
  + Amazon Kendra: Dịch vụ tìm kiếm thông minh
  + Amazon Lookout: Phát hiện bất thường trong các chỉ số kinh doanh, thiết bị và hình ảnh
  + Amazon Personalize: Tùy chỉnh các đề xuất cho người dùng

**- Demo:** AMZPhoto: Nhận diện khuôn mặt từ hình ảnh sử dụng AI

**- Amazon Bedrock AgentCore:** Một nền tảng tác nhân toàn diện được thiết kế để giải quyết các thách thức trong việc đưa các tác nhân vào môi trường production:
  + Thực thi và mở rộng mã tác nhân một cách an toàn.
  + Tích hợp bộ nhớ (ghi nhớ các tương tác trong quá khứ và học hỏi).
  + Triển khai kiểm soát danh tính và quyền truy cập cho các tác nhân và công cụ.
  + Cung cấp khả năng sử dụng công cụ tác nhân cho các quy trình làm việc phức tạp.
  + Khám phá và kết nối với các công cụ và tài nguyên tùy chỉnh.
  + Hiểu và kiểm toán mọi tương tác (khả năng quan sát).
  **+ Dịch vụ nền tảng:** Các dịch vụ này được phân loại để chạy các tác nhân an toàn ở quy mô lớn.

  **+ Nâng cao với các công cụ & bộ nhớ:** Bao gồm Bộ nhớ, Cổng kết nối (Gateway), Công cụ trình duyệt và Trình thông dịch mã.

  **+ Triển khai an toàn ở quy mô lớn:** Bao gồm Runtime và Định danh.

  **+ Thu thập thông tin chi tiết về vận hành:** Bao gồm Khả năng quan sát (Observability).

  **+ Kích hoạt tác nhân ở quy mô lớn (Kiến trúc):** Kết nối với AgentCore Gateway (qua MCP), Bộ nhớ, Định danh, Khả năng quan sát, Trình duyệt và Trình thông dịch mã.

  **+ Các Framework để xây dựng tác nhân:** CrewAI, Google ADK, LangGraph/LangChain, LlamaIndex, OpenAI Agents SDK, và Strands Agents SDK.

### Những điểm chính cần ghi nhớ
- Bedrock là trung tâm GenAI: Amazon Bedrock cung cấp các Mô hình nền tảng được quản lý hoàn toàn từ các công ty hàng đầu cho nhiều tác vụ khác nhau.

- Tùy chỉnh qua Lời nhắc và Dữ liệu: Các cách khác nhau để gợi ý (Zero-Shot, Few-shot, CoT) và sử dụng RAG để thêm thông tin cho phản hồi mô hình tốt hơn.

- Embeddings hỗ trợ tìm kiếm: Amazon Titan Embedding là một mô hình hạng nhẹ quan trọng để dịch văn bản thành số, giúp đạt được độ chính xác cao trong các tác vụ truy xuất (như RAG).

- Các mô hình được huấn luyện trước: AWS cung cấp nhiều dịch vụ AI sẵn sàng sử dụng cho các nhu cầu phổ biến, như Rekognition cho hình ảnh và Textract cho tài liệu.

- AgentCore giải quyết các vấn đề Production: Amazon Bedrock AgentCore là nền tảng toàn diện mới xử lý các phần khó khăn của việc chạy các Tác nhân AI ở quy mô lớn (như Bộ nhớ, Định danh và Khả năng quan sát).

### Ứng dụng vào công việc

- Rất hữu ích trong các dự án sau này của nhóm chúng tôi, có thể bao gồm việc sử dụng nhiều hơn các Mô hình nền tảng AI trong kiến trúc.

### Trải nghiệm sự kiện
- Các diễn giả nói rất hay và cung cấp nhiều thông tin hữu ích
- Hỏi đáp: Thành viên trong nhóm đã đặt một câu hỏi ngoài lề nhưng rất quan trọng đối với dự án của chúng tôi
  + Hỏi: SNS trong kiến trúc của chúng tôi được sử dụng để xử lý các phát hiện của GuardDuty đã gặp phải tình huống hơn 1000 cảnh báo xuất hiện cùng một lúc, chúng tôi giải quyết vấn đề này như thế nào?
  + Đáp: Thêm SQS để xếp hàng các sự kiện và đảm bảo không có cảnh báo nào bị bỏ sót
- Lọt vào top 10 trong bài kiểm tra Kahoot cuối sự kiện và được chụp ảnh cùng các diễn giả
- Đã tạo một nhóm không chính thức: "Mèo Cam Đeo Khăn", sự hợp tác giữa nhóm "The Ballers" của tôi và "Vinhomies"

#### Một số hình ảnh sự kiện
![Nhóm Mèo Cam Đeo Khăn](/images/Events/Meocamdeokhan.jpg)