---
title: "Nhật ký công việc Tuần 1"
date: "2025-09-09"
weight: 1
chapter: false
pre: " <b> 1.1. </b> "
---
### Mục tiêu Tuần 1:

* Kết nối với các thành viên và mentor của FCJ.
* Tìm hiểu môi trường làm việc văn phòng.
* Cài đặt Linux, học cách sử dụng Linux đúng cách.
* Học các kiến thức cơ bản về AWS, Console và CLI.
* Hoàn thành module 1 và 2.

### Các nhiệm vụ thực hiện trong tuần này:


| Ngày | Nhiệm vụ | Ngày bắt đầu | Ngày hoàn thành | Tài liệu tham khảo |
| :--- | :--- | :---: | :---: | :--- |
| T2 | - Đọc nội quy thực tập<br> - Tạo tài khoản AWS <br> - Tìm hiểu AWS là gì <br>- Hoàn thành Module 1 Lab 1 (Học cách tạo tài khoản AWS và quản lý nhóm người dùng) <br>- Hoàn thành Module 1 Lab 7 (Học cách tạo ngân sách sử dụng dịch vụ) <br>- Lab 7-3 (Usage Budget) không thực hiện được, lỗi ở dropdown usage type, không hiển thị gì <br>- Hoàn thành Module 1 Lab 9 (Học về Dịch vụ hỗ trợ AWS, các loại hình, lợi ích và cách yêu cầu hỗ trợ) | 08/09/2025 | 08/09/2025 | [Tạo tài khoản AWS mới](https://000001.awsstudygroup.com/1-create-new-aws-account/) <br><br> [MFA cho tài khoản AWS](https://000001.awsstudygroup.com/2-mfa-setup-for-aws-user-root/) <br><br> [Tạo nhóm Admin và người dùng Admin](https://000001.awsstudygroup.com/3-create-admin-user-and-group/) <br><br> [Hỗ trợ xác thực tài khoản](https://000001.awsstudygroup.com/4-verify-new-account/) <br><br> [Khám phá và cấu hình AWS Management Console](https://000001.awsstudygroup.com/5-explore-and-configure-the-aws-management-console/) <br><br> [Tạo Support Case và quản lý case trong AWS](https://000001.awsstudygroup.com/6-support-cases/) |
| T3 | - Bắt đầu học lý thuyết Module 2:<br>&emsp; + Học về VPC (Amazon Virtual Private Cloud)<br>&emsp; + Học về Subnet, Route table, Security Group<br>&emsp; + Học về ENI và EIP<br>&emsp; + Học về VPC Peering và Transit Gateway <br>&emsp; + Học về Elastic Load Balancing<br>&emsp; + Học về EC2<br> - Thiết lập trang web cho báo cáo workshop <br> - Cài đặt Hugo <br> - Viết thành công nhật ký công việc bằng markdown và Hugo | 09/09/2025 | 09/09/2025 | [https://cloudjourney.awsstudygroup.com/](https://cloudjourney.awsstudygroup.com/) |
| T4 - CN | - Hoàn thành các bài lab của Module 2<br> - Lab 3: <br>&emsp; + Học về các tài nguyên cần thiết để tạo và chạy EC2 instance <br>&emsp; + Cấu hình và chạy thành công các EC2 instance <br>&emsp; + Kết nối và ping thành công đến các EC2 instance <br>&emsp; + Tạo NAT Gateway để cho phép kết nối EC2 private <br> - Lab 10: <br>&emsp; + Học cách tạo và sử dụng keypair để bảo mật <br>&emsp; + Học cách cấu hình security group để quản lý kết nối <br>&emsp; + Kết nối và sử dụng thành công RDP qua EC2 <br>&emsp; + Thiết lập hybrid DNS với Route 53 Resolver (Đang thực hiện, template CloudFormation không tạo security group để tiếp tục bài lab) <br> - Lab 19: <br>&emsp; + Tạo thành công kết nối VPC Peering <br> &emsp; + Học cách cấu hình Network ACL <br> &emsp; + Bật Cross-Peer DNS để phân giải tên miền private <br> - Tải và sử dụng MobaXTerm để kết nối đến EC2 instance <br> - Tải và sử dụng Putty để cấu hình keypair | 10/09/2025 | 12/09/2025 | [Lab 3](https://000003.awsstudygroup.com/) <br><br> [Lab 10](https://000010.awsstudygroup.com/) <br><br> [Lab 19](https://000019.awsstudygroup.com/) |

### Thành tựu Tuần 1:

* Đã tạo và bảo mật tài khoản AWS, bao gồm thiết lập ngân sách và tìm hiểu các dịch vụ hỗ trợ.
* Hoàn thành lý thuyết và các bài lab thực hành về VPC, Subnet, Security Group và Route Table.
* Triển khai và kết nối thành công các EC2 instance, cấu hình NAT Gateway, và quản lý các kết nối chính sử dụng VPC Peering và AWS Transit Gateway.
* Có kinh nghiệm thực tế với S3 Bucket (hosting website tĩnh, versioning, replication), AWS Backup, và Storage Gateway.
* Thiết lập tài liệu: Đã cài đặt Hugo và cấu hình trang web để viết nhật ký công việc bằng markdown.
* Thành thạo công cụ: Học cách sử dụng MobaXTerm và PuTTY để kết nối và quản lý EC2 instance.
* Sửa thành công template CloudFormation bị lỗi thời trong bài lab Transit Gateway và học cách quản lý chi phí qua cảnh báo ngân sách.
* Hoàn thành Module 1 và Module 2, và đã bắt đầu tốt Module 3.