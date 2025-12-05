---
title: "Nhật ký công việc Tuần 11"
date: "2025-11-17"
weight: 2
chapter: false
pre: " <b> 1.11. </b> "
---
### Mục tiêu Tuần 11:

* Tối ưu hóa kiến trúc về chi phí và độ tin cậy (tích hợp SQS & phân tích API S3).
* Nâng cao kiến thức về Bảo mật biên (WAF/CloudFront) và Cơ sở hạ tầng dưới dạng mã (IaC - CDK).
* Hoàn tất kiểm thử cô lập EC2 và tinh chỉnh dashboard tùy chỉnh.

### Các nhiệm vụ thực hiện trong tuần này:

| Ngày | Nhiệm vụ | Ngày bắt đầu | Ngày hoàn thành | Tài liệu tham khảo |
| :---: | :--- | :--------: | :-------------: | :----------------- |
| T2 | - Tham gia **AWS Cloud Mastery Series #2**: Có được cái nhìn sâu sắc về CDK và CloudFormation cho dự án và nhận được khuyến nghị từ mentor về chiến lược demo.<br> - Viết bài tổng kết trải nghiệm sự kiện. | 17/11/2025 | 17/11/2025 | |
| T3 | - **Tổng quan Dashboard:** Cập nhật giao diện frontend để hiển thị các trường thông tin quan trọng hơn.<br> - **Chỉnh sửa Kiến trúc:** <br>&emsp; + Loại bỏ Glue Crawler để giảm độ phức tạp.<br>&emsp; + Thêm **Amazon SQS** vào giữa EventBridge và Step Functions để làm bộ đệm.<br> - **Phân tích Chi phí:** Phát hiện các lệnh gọi API S3 GET quá mức từ Lambda xử lý CloudTrail; lên kế hoạch cập nhật giá.<br> - **Triển khai:**<br>&emsp; + Cô lập thành công EC2 trong môi trường kiểm thử.<br>&emsp; + Nâng cấp CloudWatch ETL Lambda để xử lý log thông qua trigger mà không cần Crawler.<br> - Sao lưu mã nguồn của tất cả các Lambda function. | 18/11/2025 | 18/11/2025 | |
| T4 | - Tham gia **Workshop Bảo vệ Ứng dụng: AWS Perimeter Protection**.<br>&emsp; + Tìm hiểu sâu về cấu hình CloudFront và WAF.<br>&emsp; + Xem xét gói giá (pricing tier) mới của CloudFront.<br> - Học cách thiết lập **API Gateway REST APIs** để chuẩn bị tích hợp dashboard. | 19/11/2025 | 19/11/2025 | [AWS Perimeter Protection](https://catalog.us-east-1.prod.workshops.aws/workshops/32e6bc9a-5c03-416d-be50-34358a8a5f64/en-US) |
| T6 | - Nghiên cứu **AWS CDK**: Cài đặt, sử dụng và cấu hình stack để chuẩn bị cho việc di chuyển sang IaC vào tuần tới. | 21/11/2025 | 21/11/2025 | [AWS CDK Github](https://github.com/aws/aws-cdk) <br><br> [AWS CDK Document](https://docs.aws.amazon.com/cdk/v2/guide/home.html) |

### Thành tựu Tuần 11:

* **Tối ưu hóa Kiến trúc & Quản lý Chi phí:**
  * Tinh chỉnh kiến trúc hướng sự kiện (event-driven) bằng cách tách biệt EventBridge và Step Functions sử dụng **Amazon SQS** để đảm bảo độ bền và tin cậy của tin nhắn.
  
  * Thực hiện **phân tích chi phí** quan trọng cho pipeline log, xác định cấu hình Lambda hiện tại đang tạo ra quá nhiều yêu cầu S3 GET và lập kế hoạch tối ưu hóa chi phí API.
  * Tinh gọn **ETL Pipeline** bằng cách loại bỏ AWS Glue Crawler và nâng cấp CloudWatch Lambda để hoạt động hoàn toàn dựa trên sự kiện kích hoạt từ S3 (S3 event triggers).

* **Học tập về Bảo mật & Mạng:**
  * Có kinh nghiệm thực tế về bảo vệ biên (perimeter protection) thông qua việc hoàn thành **AWS Perimeter Protection Workshop**, tập trung vào cấu hình **AWS WAF** (Web Application Firewall) và **Amazon CloudFront**.
  

[Image of AWS CloudFront and WAF architecture]

  * Nghiên cứu **API Gateway REST APIs** để hỗ trợ việc tích hợp dashboard bảo mật tùy chỉnh trong tương lai.

* **Chuẩn bị cho Infrastructure as Code (IaC):**
  * Tận dụng kiến thức từ **AWS Cloud Mastery Series #2** để lên kế hoạch chuyển đổi dự án sang Infrastructure as Code.
  * Hoàn thành nghiên cứu nền tảng về **AWS CDK**, bao gồm cài đặt, cấu hình stack và sử dụng construct để chuẩn bị cho giai đoạn triển khai.

* **Triển khai Dự án:**
  * Thực thi và xác minh thành công logic **Cô lập EC2** trong môi trường kiểm thử thực tế.
  * Cập nhật frontend của dashboard tùy chỉnh để hiển thị các trường thông tin bảo mật liên quan hơn.