---
title: "Nhật ký công việc Tuần 4"
date: "2025-09-29"
weight: 4
chapter: false
pre: " <b> 1.4. </b> "
---
### Mục tiêu Tuần 4:

- Hoàn thành Module 6
- Bắt đầu làm đề xuất (proposal)

### Các nhiệm vụ thực hiện trong tuần này:


| Ngày | Nhiệm vụ | Ngày bắt đầu | Ngày hoàn thành | Tài liệu tham khảo |
| :--- | :--- | :---: | :---: | :--- |
| T2 | - Module 6: Ôn tập khái niệm Cơ sở dữ liệu:<br> &emsp; + Database (Cơ sở dữ liệu) <br> &emsp; + Session (Phiên) <br> &emsp; + Primary/Foreign Key (Khóa chính/Khóa ngoại) <br> &emsp; + Index (Chỉ mục) <br> &emsp; + Partitions (Phân vùng) <br> &emsp; + Execution/Query Plan (Kế hoạch thực thi/truy vấn) <br> &emsp; + Log & Buffer <br> &emsp; + RDBMS (Hệ quản trị cơ sở dữ liệu quan hệ) <br> &emsp; + NoSQL <br> ![Database](/images/1-Worklog/Database.png) <br> &emsp; + OLTP (Xử lý giao dịch trực tuyến): Dùng cho thanh toán, giao dịch <br> &emsp; + OLAP (Xử lý phân tích trực tuyến): Phân tích dữ liệu, dự đoán xu hướng và mô hình <br> - AWS RDS (Dịch vụ cơ sở dữ liệu quan hệ): Bao gồm Aurora, MySQL, Postgres SQL, MSSQL, Oracle, Maria <br> &emsp; + Sao lưu tự động <br> &emsp; + Tạo Read Replica <br> &emsp; + Read Replica có thể chuyển thành node chính (primary) <br> &emsp; + Tự động chuyển đổi dự phòng (Fail Over)/Multi AZ (Sao lưu trên nhiều AZ) <br> &emsp; + Thường được dùng cho OLTP <br> &emsp; + Mã hóa dữ liệu khi lưu trữ/khi truyền tải <br> &emsp; + Được bảo vệ bởi Security Group và NACL <br> &emsp; + Có thể thay đổi kích thước instance <br> &emsp; + Tự động mở rộng dung lượng lưu trữ <br> - Amazon Aurora: Tối ưu hóa hạ tầng lưu trữ bên dưới, sử dụng MySQL và PostgreSQL <br> &emsp; + Backtrack: quay lại trạng thái trước đó <br> &emsp; + Clone (Tạo bản sao) <br> &emsp; + Global Database (Đa vùng) <br> &emsp; + Multi Master: Nhiều Master Database <br> - Amazon Redshift: Dịch vụ kho dữ liệu (Data warehouse): Lõi PostgreSQL, tối ưu cho OLAP <br> &emsp; + Sử dụng kiến trúc MPP (Massively Parallel Processing): dữ liệu được phân vùng và lưu tại các compute node, một Leader node dùng để điều phối và biên dịch truy vấn <br> &emsp; + Lưu trữ dữ liệu dạng cột (columnar), hữu ích cho ứng dụng OLAP <br> <br> &emsp; + Sử dụng SQL và các driver như JDBC và ODBC <br> &emsp; + Cung cấp các dịch vụ tối ưu chi phí (Transient Cluster/ Redshift spectrum) <br> - Amazon ElastiCache: Tạo các Cluster Caching Engine (Redis/Memcached) <br> &emsp; + Phát hiện và thay thế các node bị lỗi <br> &emsp; + Đặt trước lớp CSDL để cache dữ liệu <br> &emsp; + Khuyến nghị dùng Redis cho các workload mới <br> &emsp; + Sử dụng ElastiCache yêu cầu logic caching trên ứng dụng, không khuyến khích dùng system caching mặc định <br> - Xây dựng đề xuất cho workshop cùng đồng đội <br> - Môn học ở trường: <br> &emsp; + KS57: Hoàn thành môn Quản trị dữ liệu và an toàn thông tin | 29/09/2025 | 29/09/2025 | [Quản trị dữ liệu và an toàn thông tin](https://www.coursera.org/account/accomplishments/verify/JA236L8TZGD7) |
| T3 | - Lab 43: Hướng dẫn bị lỗi, link không hoạt động, làm theo video<br> &emsp; + Tải xuống Schema Conversion Tool <br> &emsp; + Tải MSSQL trên EC2 Instance <br> &emsp; + Không có script SQL, thử với Database MSSQL cơ bản tự tạo <br> &emsp; + Không có CloudFormation Stack, bỏ qua kết nối Oracle Database <br> &emsp; + Cài đặt MySQL trên EC2 Instance <br> &emsp; + Di chuyển Database MSSQL tự tạo sang MySQL Database sử dụng AWS Schema Conversion Tool <br> &emsp; + Tạo RDS tùy chỉnh để kiểm thử tác vụ di chuyển <br> &emsp; + Thử di chuyển từ máy local lên RDS <br> &emsp; + Thử dùng AWS Replication Agent: Không thành công do chỉ hỗ trợ Window/Linux server, không hỗ trợ OS cá nhân <br> &emsp; + Thử port forward PC để dùng làm endpoint <br> &emsp; + Port forwarding thất bại, không được ISP cho phép | 30/09/2025 | 30/09/2025 | [Lab 43](https://000043.awsstudygroup.com/) <br><br> [Application Mirgation Service Guide](https://docs.aws.amazon.com/mgn/latest/ug/what-is-application-migration-service.html) |
| T4 | - Phát hiện credit của tài khoản AWS đã hết hạn khi làm lab 12<br> - Viết support case (yêu cầu hỗ trợ) <br> - Tạm dừng làm lab <br> - Tập trung nghiên cứu về đề xuất của nhóm | 01/10/2025 | 01/10/2025<br> - Môn học ở trường: <br> &emsp; + ENW439c: Hoàn thành môn Research Methodologies | [Research Methodologies](https://www.coursera.org/account/accomplishments/verify/M3368Q4AAMNB) |
| T5 | - Tiếp tục làm lab nhờ sự trợ giúp của thành viên nhóm: Tạo IAM User với quyền admin để tôi đăng nhập và sử dụng tài khoản của họ<br> - Dịch bài blog đầu tiên | 02/10/2025 | 02/10/2025 | [Blog 1](content/3-BlogsTranslated/3.1-Blog1/_index.md) |
| T6 | - Tham gia sự kiện AI-Driven Development Life Cycle: Reimagining Software Engineering<br> - Dịch bài blog thứ hai và thứ ba | 03/10/2025 | 04/10/2025 | [Blog 2](content/3-BlogsTranslated/3.2-Blog2/_index.md) <br><br> [Blog 3](content/3-BlogsTranslated/3.3-Blog3/_index.md) |

### Thành tựu Tuần 4:

* Hoàn thành việc ôn tập toàn diện các khái niệm cốt lõi về cơ sở dữ liệu bao gồm RDBMS, khóa, chỉ mục, phân vùng, OLTP/OLAP và các dịch vụ cơ sở dữ liệu đặc thù của AWS.
* Nắm được kiến thức lý thuyết về các tính năng và trường hợp sử dụng cho AWS RDS, Amazon Aurora (ví dụ: Backtrack, Global Database), Amazon Redshift (Kho dữ liệu cho OLAP), và Amazon ElastiCache (caching với Redis/Memcached).
* Di chuyển Cơ sở dữ liệu: Đã thử nghiệm một bài lab di chuyển cơ sở dữ liệu phức tạp, thể hiện sự tháo vát thông qua việc:
  * Tự tạo một Database MSSQL và cài đặt các dịch vụ cần thiết trên EC2 instance do hướng dẫn lab bị lỗi.
  * Di chuyển thành công database MSSQL tự tạo sang MySQL sử dụng AWS Schema Conversion Tool (SCT).
* Phát hiện và xử lý vấn đề hết hạn credit AWS bằng cách tạo support case.
* Đảm bảo tiến độ làm lab bằng cách thiết lập IAM User với quyền admin trên tài khoản của thành viên trong nhóm.
* Xây dựng đề xuất cho workshop sắp tới cùng với các thành viên trong nhóm.
* Hoàn thành việc dịch 3 bài blog.
* Tham dự sự kiện AI-Driven Development Life Cycle: Reimagining Software Engineering.