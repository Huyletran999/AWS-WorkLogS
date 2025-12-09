---
title: "Sự kiện 2"
date: "2025-11-15"
weight: 2
chapter: false
pre: " <b> 4.3. </b> "
---

# Báo cáo Tóm tắt: “AWS Cloud Mastery Series #1 - AI/ML/GenAI trên AWS”

### Mục tiêu Sự kiện

- Giới thiệu về AI/ML/GenAI trên nền tảng AWS

### Diễn giả

- **Lam Tuan Kiet** – Sr DevOps Engineer, FPT Software
- **Danh Hoang Hieu Nghi** - AI Engineer, Renova Cloud
- **Dinh Le Hoang Anh** - Thực tập sinh Cloud Engineer, First Cloud AI Journey
- **Van Hoang Kha** - Community Builder

### Điểm nhấn chính

# Khám phá Generative AI với Amazon Bedrock:

**- Các Mô hình Nền tảng (Foundation Models):** Khác biệt so với mô hình truyền thống ở chỗ nó có thể thích ứng cho nhiều tác vụ, cung cấp nhiều mô hình được quản lý hoàn toàn từ các công ty AI hàng đầu như: OpenAI, Claude, Anthropic, v.v.
**- Kỹ thuật Prompt (Prompt Engineering):** Xây dựng và tinh chỉnh các hướng dẫn
   + Zero-Shot Prompting: Một câu lệnh (prompt) không có bối cảnh hoặc ví dụ trước đó.
   + Few-shot Prompting: Một câu lệnh đi kèm với một vài bối cảnh và ví dụ.
   + Chain of Thought: Một câu lệnh bao gồm các quy trình suy nghĩ và các bước để dẫn đến câu trả lời thực tế.
**- Retrieval Augmented Generation (RAG):** Truy xuất thông tin liên quan từ một nguồn dữ liệu
   + R: Retrieval (Truy xuất) - Lấy thông tin liên quan từ cơ sở tri thức hoặc nguồn dữ liệu.
   + A: Augmented (Tăng cường) - Thêm thông tin đã truy xuất làm bối cảnh bổ sung vào câu lệnh của người dùng trước khi đưa vào mô hình.
   + G: Generation (Tạo sinh) - Phản hồi từ mô hình dựa trên câu lệnh đã được tăng cường.
   + Trường hợp sử dụng: Cải thiện chất lượng nội dung, chatbot theo ngữ cảnh và trả lời câu hỏi, tìm kiếm cá nhân hóa và tóm tắt dữ liệu thời gian thực.

**- Amazon Titan Embedding:** Mô hình hạng nhẹ, vượt trội trong việc chuyển đổi văn bản thành các biểu diễn số (embeddings) cho các tác vụ truy xuất có độ chính xác cao, hỗ trợ hơn 100 ngôn ngữ.

**- Các dịch vụ AI được huấn luyện trước (Pretrained AI Services):**
  + Amazon Rekognition: Phân tích hình ảnh và video.
  + Amazon Translate: Phát hiện và dịch văn bản.
  + Amazon Textract: Trích xuất văn bản và bố cục từ tài liệu.
  + Amazon Transcribe: Chuyển đổi giọng nói thành văn bản.
  + Amazon Polly: Chuyển đổi văn bản thành giọng nói.
  + Amazon Comprehend: Trích xuất thông tin chi tiết và mối quan hệ từ văn bản.
  + Amazon Kendra: Dịch vụ tìm kiếm thông minh.
  + Amazon Lookout: Phát hiện bất thường trong các chỉ số kinh doanh, thiết bị và hình ảnh.
  + Amazon Personalize: Tùy chỉnh các đề xuất cho người dùng.

**- Demo:** AMZPhoto: Nhận diện khuôn mặt từ hình ảnh sử dụng AI.

**- Amazon Bedrock AgentCore:** Một nền tảng tác nhân (agentic) toàn diện được thiết kế để giải quyết các thách thức khi đưa các tác nhân (agents) vào môi trường thực tế (production):
  + Thực thi và mở rộng mã nguồn của agent một cách an toàn.
  + Kết hợp bộ nhớ (ghi nhớ các tương tác trong quá khứ và học hỏi).
  + Triển khai kiểm soát danh tính và quyền truy cập cho các agent và công cụ.
  + Cung cấp khả năng sử dụng công cụ cho các quy trình làm việc phức tạp.
  + Khám phá và kết nối với các công cụ và tài nguyên tùy chỉnh.
  + Hiểu và kiểm toán mọi tương tác (khả năng quan sát - observability).
  **+ Các Dịch vụ Nền tảng:** Các dịch vụ này được phân loại để chạy các agent một cách an toàn ở quy mô lớn.

  **+ Tăng cường với công cụ & bộ nhớ:** Bao gồm Bộ nhớ (Memory), Cổng kết nối (Gateway), Công cụ trình duyệt (Browser tool), và Trình thông dịch mã (Code Interpreter).

  **+ Triển khai an toàn ở quy mô lớn:** Bao gồm Runtime và Định danh (Identity).

  **+ Thu thập thông tin vận hành:** Bao gồm Khả năng quan sát (Observability).

  **+ Kích hoạt Agent ở quy mô lớn (Kiến trúc):** Kết nối với AgentCore Gateway (qua MCP), Bộ nhớ, Định danh, Khả năng quan sát, Trình duyệt và Trình thông dịch mã.

  **+ Các Framework để xây dựng Agent:** CrewAI, Google ADK, LangGraph/LangChain, LlamaIndex, OpenAI Agents SDK, và Strands Agents SDK.

### Bài học rút ra (Key Takeaways)
- Bedrock là trung tâm GenAI: Amazon Bedrock cung cấp các Mô hình Nền tảng được quản lý hoàn toàn từ các công ty hàng đầu cho nhiều tác vụ khác nhau.

- Tùy chỉnh qua Prompt và Dữ liệu: Nhiều cách để đặt câu lệnh (Zero-Shot, Few-shot, CoT) và tận dụng RAG để thêm thông tin giúp mô hình phản hồi tốt hơn.

- Embeddings hỗ trợ Tìm kiếm: Amazon Titan Embedding là mô hình hạng nhẹ quan trọng để dịch văn bản sang số, giúp đạt độ chính xác cao trong các tác vụ truy xuất (như RAG).

- Các mô hình Pretrained: AWS cung cấp nhiều dịch vụ AI sẵn sàng sử dụng cho các nhu cầu phổ biến, như Rekognition cho hình ảnh và Textract cho tài liệu.

- AgentCore giải quyết vấn đề Production: Amazon Bedrock AgentCore là nền tảng toàn diện mới giúp xử lý các phần khó khăn khi chạy AI Agents ở quy mô lớn (như Bộ nhớ, Định danh và Khả năng quan sát).

### Ứng dụng vào công việc

- Rất hữu ích cho các dự án sau này của nhóm, có thể bao gồm việc sử dụng nhiều hơn các Mô hình Nền tảng AI trong kiến trúc của chúng tôi.

### Trải nghiệm Sự kiện
- Các diễn giả nói rất lưu loát và cung cấp nhiều thông tin bổ ích.
- Hỏi đáp (Q&A): Thành viên trong nhóm đã đặt một câu hỏi hơi ngoài lề nhưng quan trọng đối với dự án của chúng tôi.
  + Hỏi: Dịch vụ SNS trong kiến trúc của chúng tôi được dùng để xử lý các phát hiện từ GuardDuty (GuardDuty Findings) đã gặp tình trạng hơn 1000 cảnh báo xuất hiện cùng lúc, làm thế nào để giải quyết vấn đề này?
  + Đáp: Thêm SQS vào để xếp hàng các sự kiện và đảm bảo không bỏ sót bất kỳ cảnh báo nào.
- Lọt vào top 10 trong bài Quiz Kahoot cuối sự kiện và được chụp ảnh cùng các diễn giả.
- Đã tạo một nhóm không chính thức: "Mèo Cam Đeo Khăn", một sự hợp tác chung giữa nhóm "The Ballers" của tôi và "Vinhomies".

#### Một số hình ảnh sự kiện


![Nhóm Mèo Cam Đeo Khăn](/images/Events/Meocamdeokhan.jpg)