---
title: "Nhật ký công việc Tuần 7"
date: "2025-10-20"
weight: 7
chapter: false
pre: " <b> 1.7. </b> "
---

### Mục tiêu Tuần 7:

* Kết nối và làm quen với các thành viên của First Cloud Journey.
* Hiểu các dịch vụ AWS cơ bản, cách sử dụng console & CLI.
* Thiết kế và tạo mẫu quy trình phản ứng sự cố tự động, tinh chỉnh kiến trúc dự án dựa trên phản hồi của mentor.

### Các nhiệm vụ thực hiện trong tuần này:

| Ngày | Nhiệm vụ | Ngày bắt đầu | Ngày hoàn thành | Tài liệu tham khảo |
| :---: | :--- | :--------: | :-------------: | :----------------- |
| T2 | - Nghiên cứu và thử nghiệm thuật toán cô lập EC2 bằng cách sử dụng Security Group (SG) không có quy tắc outbound/inbound nào | 20/10/2025 | 21/10/2025 | |
| T4 | - Họp nhóm:<br> &emsp; + Ôn tập nhanh kiến thức dịch vụ AWS <br> &emsp; + Thảo luận về các thay đổi trong đề xuất <br> - Cập nhật Kiến trúc AWS: Thêm AWS Detective <br> - Chỉnh sửa đề xuất: <br> &emsp; + Thêm việc sử dụng AWS Detective <br> &emsp; + Thêm kế hoạch dùng CDK sau khi hoàn thành workshop <br> - Khuyến nghị của Mentor: <br> &emsp; + Trực quan hóa dữ liệu nhưng không dùng QuickSight, thay vào đó làm dashboard tự code (Đang nghiên cứu) <br> &emsp; + Lưu các phát hiện của GuardDuty vào S3 bucket để phân tích (Đang nghiên cứu) <br> - Cấu hình thành công EventBridge để kích hoạt khi có các phát hiện cụ thể từ GuardDuty và: <br> &emsp; + Gửi email SNS đến tất cả thành viên nhóm <br> &emsp; + Kích hoạt một script Lambda đơn giản <br> - Hình thành ý tưởng thêm vào workshop: Làm một trang biểu đồ dữ liệu đơn giản host trên S3, dùng API Gateway và Lambda để lấy dữ liệu điều tra từ Amazon Athena (Đang nghiên cứu) | 22/10/2025 | 22/10/2025 | |
| T5 | - Thử chơi AWS Card Clash cùng thành viên nhóm: Khá bất ngờ vì hiệu quả tốt để học về các dịch vụ, chức năng và vị trí của chúng trong Kiến trúc<br> - Ôn tập kiến thức dịch vụ AWS cho kỳ thi giữa kỳ: Sử dụng Google Gemini để tạo câu hỏi trắc nghiệm dựa trên yêu cầu | 23/10/2025 | 23/10/2025 | [AWS Card Clash](https://aws.amazon.com/training/digital/aws-card-clash/) |
| T6 | - Cấu hình thành công GuardDuty threat list để kích hoạt phát hiện từ các hoạt động của EC2 Instance | 08/15/2025 | 08/15/2025 | [Pháp luật và đạo đức trong công nghệ số](https://www.coursera.org/account/accomplishments/verify/7JELDK2MGGKL) |

### Thành tựu Tuần 7:

* **Thực hành GuardDuty:**
  * Hoàn thành "Getting Hands on with Amazon GuardDuty - AWS Virtual Workshop" và bài lab chuyên sâu tạo bởi Amazon Q.
  * Tạo, kiểm thử và kích hoạt thành công nhiều loại phát hiện GuardDuty thông qua cài đặt console, hoạt động EC2 và truy cập CloudTrail API.
  * Thiết lập môi trường kiểm thử dễ dàng hơn bằng cách kích hoạt thành công các cảnh báo mẫu với mức độ nghiêm trọng và loại khác nhau qua CloudShell CLI.
  * Cấu hình thành công GuardDuty threat list để kích hoạt phát hiện từ hoạt động của EC2 Instance.

* **Đề xuất Workshop và Cải tiến Kiến trúc:**
  * Cập nhật đề xuất và Kiến trúc AWS để tích hợp AWS Detective cho khả năng điều tra sâu hơn.
  * Thêm kế hoạch triển khai CDK sau khi hoàn thành workshop.
  * Bắt đầu nghiên cứu các khuyến nghị của mentor, bao gồm trực quan hóa dữ liệu tự code và lưu phát hiện GuardDuty vào S3 để phân tích.
  * Hình thành ý tưởng workshop mới về trang biểu đồ dữ liệu đơn giản host trên S3 sử dụng API Gateway và Lambda.

* **Tích hợp Dịch vụ và Tự động hóa:**
  * Cấu hình thành công EventBridge để xử lý các phát hiện cụ thể của GuardDuty.
  * Tự động hóa thông báo bằng cách gửi email SNS cho thành viên nhóm và kích hoạt script Lambda dựa trên cảnh báo GuardDuty.

* **Nghiên cứu An ninh Mạng & Cô lập:**
  * Nghiên cứu và kiểm chứng thuật toán cô lập EC2 bằng cách thử nghiệm Security Group (SG) với các quy tắc chặn inbound/outbound để ngăn chặn hiệu quả các instance bị xâm nhập.