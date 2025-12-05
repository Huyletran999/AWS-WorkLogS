---
title: "Nhật ký công việc Tuần 9"
date: "2025-09-09"
weight: 9
chapter: false
pre: " <b> 1.9. </b> "
---
### Mục tiêu Tuần 9:

* Tiếp tục làm việc với workshop

### Các nhiệm vụ thực hiện trong tuần này:

| Ngày | Nhiệm vụ | Ngày bắt đầu | Ngày hoàn thành | Tài liệu tham khảo |
| :--- | :--- | :---: | :---: | :--- |
| T2 | - Chỉnh sửa Kiến trúc AWS:<br>&emsp; + Loại bỏ AWS Detective <br>&emsp; + Cập nhật Step Function Workflow thay cho một AWS Lambda Function duy nhất <br>&emsp; + Thêm Custom Dashboard: Một trang web dashboard tĩnh tùy chỉnh được host trên S3 và dùng Athena để truy vấn từ data lake <br> | 03/11/2025 | 03/11/2025 | |
| T3 | - Bắt đầu viết và xem xét các inline policy cho Lambda và User Role. | 04/11/2025 | 04/11/2025 | |
| T4 | - Họp nhóm: Báo cáo tiến độ:<br>&emsp; + IR Workflow: Hoàn thành một nửa, function cô lập EC2 đã xong, chưa kiểm thử với các finding thực tế. | 05/11/2025 | 05/11/2025 | |
| T5 | - Họp nhóm<br> - Nghiên cứu phương pháp ETL Pipeline: <br>&emsp; + Thay vì dùng Glue ELT Job, sử dụng custom Lambda ELT pipeline cho CloudTrail và CloudWatch logs <br>&emsp; + Lưu log thô vào một Raw Log S3 Bucket sau đó dùng ETL Lambda để xử lý dữ liệu và ghi vào Processed Data S3 để Crawl <br> - Chỉnh sửa Kiến trúc AWS: Thêm nhóm mới: nhóm DATA PREP chứa Raw Log S3 Bucket và ETL Lambda <br>- Môn học ở trường: <br> | 06/11/2025 | 06/11/2025 | [Advanced Writing](https://www.coursera.org/account/accomplishments/verify/EDQ1NY2UG063) |
| T6 | - Nghiên cứu Kinesis Data Firehose để thu thập log: Tốt cho việc sử dụng trong tương lai, không phù hợp với dự án hiện tại vì dữ liệu streaming thời gian thực là không cần thiết, sử dụng xử lý theo lô (batch processing) tốt hơn<br> - Xây dựng thành công ETL Pipeline cho CloudTrail log: Được kích hoạt bởi việc tạo object trong CloudTrail Raw Log Bucket và định dạng lại log thô thành JSONL rồi lưu vào Processed S3 <br> - Crawl và truy vấn thành công log đã xử lý để hiển thị các sự kiện CloudTrail | 07/11/2025 | 07/11/2025 | |

### Thành tựu Tuần 9:

* **Tinh chỉnh Kiến trúc & Ra quyết định:**
    * Cập nhật cơ chế Ứng phó sự cố (IR) để sử dụng **Step Functions Workflow** thay vì một Lambda function duy nhất nhằm cải thiện khả năng điều phối.
    * Giới thiệu chiến lược **Custom Dashboard** (trang web tĩnh host trên S3) sử dụng Athena để truy vấn data lake.
    * Thực hiện phân tích so sánh giữa **AWS Kinesis Data Firehose** và xử lý theo lô; chọn phương pháp xử lý theo lô để tiết kiệm chi phí vì không yêu cầu streaming thời gian thực.

* **Triển khai Data Pipeline:**
    * Tạo nhóm kiến trúc **DATA PREP** mới, bao gồm Raw Log S3 Bucket và custom ETL Lambda.
    * Xây dựng và triển khai **serverless ETL Lambda pipeline** để xử lý CloudTrail log, tự động kích hoạt khi có object mới được tạo trong Raw Log S3 Bucket.
    * Crawl và truy vấn thành công CloudTrail log đã xử lý (định dạng JSONL) sử dụng **AWS Glue và Athena**.
    

* **Cấu hình Bảo mật & IAM:**
    * Bắt đầu quy trình thắt chặt bảo mật bằng cách viết và xem xét các **inline policy** cho Lambda function và User Role để đảm bảo quyền truy cập tối thiểu (least-privilege).

* **Tiến độ Dự án:**
    * Đạt 50% tiến độ hoàn thành IR Step Functions Workflow, với **EC2 quarantine function** đã được code xong (chờ kiểm thử finding).