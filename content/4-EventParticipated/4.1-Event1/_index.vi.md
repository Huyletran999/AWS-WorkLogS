---
title: "Sự kiện 1"
date: "2025-10-03"
weight: 1
chapter: false
pre: " <b> 4.1. </b> "
---

# Báo cáo tóm tắt: “Vòng đời phát triển định hướng AI: Tái định hình Kỹ thuật phần mềm”

### Mục tiêu sự kiện

- Khám phá sự chuyển đổi mang tính cách mạng trong phát triển phần mềm được thúc đẩy bởi AI tạo sinh.
- Giới thiệu Vòng đời phát triển định hướng AI (AI-DLC) và các khái niệm cốt lõi của nó.
- Demo Kiro và Amazon Q Developer

### Diễn giả

- **Toan Huynh** – Specialist SA, PACE
- **My Nguyen** - Sr. Prototyping Architect, Amazon Web Services - ASEAN


### Những điểm nổi bật

- Tập trung vào khái niệm AI-DLC, một khuôn khổ nơi AI điều phối quy trình phát triển, bao gồm lập kế hoạch, phân rã tác vụ và đề xuất kiến trúc, trong khi các nhà phát triển giữ trách nhiệm cuối cùng về việc xác nhận, ra quyết định và giám sát.

**- Khái niệm cốt lõi của AI-DLC:** Cách tiếp cận này lấy Con người làm trung tâm, với AI đóng vai trò là Cộng tác viên để nâng cao năng lực của nhà phát triển, dẫn đến Tăng tốc độ phân phối (chu kỳ được tính bằng giờ/ngày thay vì tuần/tháng).

**- Quy trình làm việc AI-DLC:** Đây là một vòng lặp lặp lại bao gồm các Tác vụ AI (Tạo kế hoạch, Thực hiện kế hoạch, Tìm kiếm sự làm rõ) và Tác vụ con người (Cung cấp sự làm rõ, Thực hiện kế hoạch), trong đó AI liên tục đặt câu hỏi làm rõ và chỉ thực hiện các giải pháp sau khi con người xác nhận.

**- Các giai đoạn AI-DLC:** Vòng đời được chia thành Khởi tạo, Xây dựng và Vận hành. Mỗi giai đoạn xây dựng ngữ cảnh phong phú hơn cho giai đoạn tiếp theo:

+ Khởi tạo (Inception): Bao gồm xây dựng ngữ cảnh, mô tả chi tiết ý định với User Stories và lập kế hoạch với các Đơn vị công việc (Units of Work).

+ Xây dựng (Construction): Liên quan đến Mô hình hóa miền (Domain Modeling), tạo mã và kiểm thử, thêm các thành phần kiến trúc và triển khai với IaC & kiểm thử.

+ Vận hành (Operation): Tập trung vào triển khai trong môi trường production và quản lý sự cố.

**- Những thách thức mà AI-DLC hướng tới giải quyết:**

+ Mở rộng phát triển AI: Các công cụ lập trình AI có thể thất bại với các dự án phức tạp.

+ Kiểm soát hạn chế: Các công cụ hiện có gây khó khăn trong việc cộng tác và quản lý các tác nhân AI.

+ Chất lượng mã: Việc duy trì kiểm soát chất lượng khi chuyển từ bằng chứng khái niệm (PoC) sang môi trường production trở nên khó khăn.

# Đi sâu chi tiết: Kiro - IDE AI cho Nguyên mẫu đến Production

- Kiro, một Môi trường phát triển tích hợp (IDE) ưu tiên AI hỗ trợ AI-DLC, tập trung vào phát triển dựa trên đặc tả (Spec-driven development).

**- Phát triển dựa trên đặc tả:** Kiro chuyển đổi một câu lệnh cấp cao (ví dụ: "Tôi muốn tạo một ứng dụng trò chuyện giống Slack") thành các yêu cầu rõ ràng (requirements.md), thiết kế hệ thống (design.md) và các tác vụ riêng biệt (tasks.md), thay đổi căn bản việc phát triển từ "viết code theo cảm tính" (vibe coding) sang một quy trình có cấu trúc, có thể truy xuất nguồn gốc. Các nhà phát triển cộng tác với Kiro trên các thông số kỹ thuật này, đóng vai trò là nguồn sự thật.

**- Quy trình làm việc tác nhân (Agentic Workflows):** Các tác nhân AI của Kiro thực hiện đặc tả trong khi vẫn giữ nhà phát triển con người nắm quyền kiểm soát, với các tính năng chính là:

**+ Kế hoạch thực hiện:** Kiro tạo ra một Kế hoạch thực hiện chi tiết với các tác vụ bắt đầu, tác vụ phụ (ví dụ: "Triển khai đăng ký người dùng và endpoint đăng nhập", "Triển khai phần mềm trung gian JWT") và liên kết chúng lại với các yêu cầu cụ thể để xác nhận.

**+ Agent Hooks:** Các hook này ủy quyền các tác vụ cho các tác nhân AI kích hoạt dựa trên các sự kiện như "lưu tệp". Chúng tự động thực thi trong nền dựa trên các lời nhắc được xác định trước, giúp mở rộng công việc bằng cách tạo tài liệu, kiểm thử đơn vị hoặc tối ưu hóa hiệu suất mã.
### Những điểm chính cần ghi nhớ
**- AI đảm bảo sự sẵn sàng cho Production:** Việc Kiro tạo ra các tài liệu thiết kế chi tiết (như sơ đồ luồng dữ liệu và hợp đồng API) và tạo các bài kiểm tra đơn vị trước khi mã được viết, đảm bảo rằng mã do AI tạo ra đã sẵn sàng cho production và có thể bảo trì, không chỉ là một nguyên mẫu nhanh chóng.

**- Kiểm soát của con người thông qua các tạo tác:** Các nhà phát triển duy trì quyền kiểm soát không phải bằng cách viết phần lớn mã, mà bằng cách xác nhận và tinh chỉnh các tạo tác—các yêu cầu, thiết kế và kế hoạch tác vụ—trước khi các tác nhân AI thực hiện việc triển khai.

### Ứng dụng vào công việc

**- Tích hợp Amazon Q Developer/Các công cụ tương tự:** Tích hợp các trợ lý lập trình AI vào các dự án học thuật của tôi để tự động hóa mã mẫu và các tác vụ chung nhằm tăng năng suất.

**- Tập trung vào các tác vụ giá trị cao:** Bằng cách để AI tự động hóa những công việc nặng nhọc không phân biệt, tôi có thể tập trung thời gian vào việc làm chủ các tác vụ sáng tạo, có giá trị cao hơn như Mô hình hóa miền và Thiết kế kiến trúc, vốn là những hoạt động lấy con người làm trung tâm rất quan trọng trong giai đoạn Xây dựng.

### Trải nghiệm sự kiện

Việc tham dự sự kiện **Vòng đời phát triển định hướng AI: Tái định hình Kỹ thuật phần mềm** đã mang lại cái nhìn hấp dẫn về tương lai của phát triển phần mềm. Rõ ràng là AI tạo sinh không chỉ là một trợ lý lập trình; nó đang ở vị thế trở thành người điều phối cốt lõi của toàn bộ quy trình phát triển. Phiên làm việc được cấu trúc tốt, đi từ khái niệm bao quát của AI-DLC đến các bản demo cụ thể của Amazon Q Developer và Kiro. Bản demo của Kiro đặc biệt ấn tượng, cho thấy cách một lời nhắc văn bản đơn lẻ có thể được chuyển đổi thành một kế hoạch phát triển đầy đủ, có thể thực thi và có thể truy xuất nguồn gốc ngay bên trong IDE.

#### Bài học rút ra
- Ba thách thức chính với sự phát triển AI hiện tại (mở rộng quy mô, kiểm soát hạn chế và chất lượng mã) làm cho cách tiếp cận có cấu trúc, được con người xác nhận của AI-DLC trở nên vô cùng cần thiết và được cân nhắc kỹ lưỡng.


#### Một số hình ảnh sự kiện
![Ảnh nhóm trong sự kiện](/images/Events/TheBois-AIDLC.jpg)