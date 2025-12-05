---
title: "Nhật ký công việc Tuần 2"
date: "2025-09-15"
weight: 2
chapter: false
pre: " <b> 1.2. </b> "
----------------------

### Mục tiêu Tuần 2:

* Hiểu và cấu hình AWS Transit Gateway.
* Tìm hiểu về các dịch vụ lưu trữ AWS (EBS, EFS, S3).
* Thảo luận về ý tưởng workshop.
* Thực hành các chiến lược sao lưu và khôi phục dữ liệu.
* Lưu trữ website tĩnh sử dụng S3 và cấu hình CloudFront.
* Hoàn thành Module 3.

### Các nhiệm vụ thực hiện trong tuần này:


| Ngày | Nhiệm vụ | Ngày bắt đầu | Ngày hoàn thành | Tài liệu tham khảo |
| :--- | :--- | :---: | :---: | :--- |
| T2 | - Lab 20:<br> - Tạo thành công AWS Transit Gateway để cho phép kết nối giữa các VPC thông qua một hub chung <br> - Sửa file template, thay đổi loại EC2 instance thành t3.micro vì tài khoản vẫn đang sử dụng gói miễn phí (free tier) | 15/09/2025 | 15/09/2025 | |
| T3 | - Đã xác minh các kế hoạch chi phí và ngân sách hoạt động đúng dự kiến, nhận thông báo qua email.<br> Bắt đầu học lý thuyết Module 3 <br>&emsp; Học về EBS, tính năng Instance store và kiểm tra User Data/Meta Data <br> - Tìm hiểu về Amazon Lightsail <br> Tìm hiểu về Elastic File System (EFS) và FSx <br> - Tìm hiểu về MGN <br>&emsp; - Hoàn thành các bài lab của Module 3 (Phần 1) - Lab 13: Tạo thành công Backup Plan và Vault cho dữ liệu trong S3 Bucket &emsp; + Thiết lập thành công thông báo cho các sự kiện Backup &emsp; + Khôi phục bản backup thành công<br> - Hoàn thành các bài lab của Module 3 (Phần 2) - Lab 24: &emsp; + Đã tạo Storage Gateway &emsp; + Hoàn thành việc chia sẻ file thành công <br> - Hoàn thành các bài lab của Module 3 (Phần 3) - Lab 57: &emsp; + Lưu trữ thành công website tĩnh bằng S3 Bucket &emsp; + Cấu hình thành công các access modifier &emsp; + Cấu hình tăng tốc Website tĩnh với CloudFront không hoạt động, bỏ qua bước này &emsp; + Tạo thành công các phiên bản (version) cho bucket &emsp; + Di chuyển các object giữa các bucket &emsp; + Sao chép (Replicate) bucket sang các region khác. <br>| 16/09/2025 | 20/09/2025 | [Lab 13](https://000013.awsstudygroup.com/) <br><br> [Lab 24](https://000024.awsstudygroup.com/) <br><br> [Lab 57](https://000057.awsstudygroup.com/) |

### Thành tựu Tuần 2:

* Sửa thành công template CloudFormation bị lỗi thời trong bài lab Transit Gateway.
* Tạo thành công AWS Transit Gateway để kết nối giữa các VPC thông qua một hub chung.
* Rút ra bài học về việc dọn dẹp tài nguyên và xác minh cảnh báo chi phí/ngân sách (bị trừ $12 credit).
* Có kinh nghiệm thực tế với S3 Bucket (hosting website tĩnh, versioning, replication).
* Tạo thành công Backup Plan và Vault sử dụng AWS Backup, bao gồm cả kiểm thử khôi phục.
* Cấu hình Storage Gateway và hoàn thành nhiệm vụ chia sẻ file.
* Hoàn thành lý thuyết và bài lab của Module 3.