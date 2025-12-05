---
title: "Nhật ký công việc Tuần 3"
date: "2025-09-22"
weight: 3
chapter: false
pre: " <b> 1.3. </b> "
---
### Mục tiêu Tuần 3:

* Hoàn thành Module 5.
* Hỗ trợ đồng đội với các bài lab trước đó.
* Làm lại các bài lab trước đây bị chặn do giới hạn Free Tier.
* Thảo luận ý tưởng dự án.

### Các nhiệm vụ thực hiện trong tuần này:


| Ngày | Nhiệm vụ | Ngày bắt đầu | Ngày hoàn thành | Tài liệu tham khảo |
| :--- | :--- | :---: | :---: | :--- |
| T2 | - Lab 25 không thể hoàn thành vì tài khoản vẫn ở gói Free Tier.<br>- Đã nâng cấp tài khoản lên gói trả phí.<br>- Thử lại Lab 25:<br>&emsp;+ Template được cung cấp sử dụng Lambda runtime nodejs12.x đã cũ, nên đã cập nhật lên nodejs20.x.<br>&emsp;+ Thiết lập hệ thống file FSx.<br>&emsp;+ Endpoint mặc định của S3 để kiểm thử chỉ truy cập được ở vùng US, nên câu lệnh cần đổi thành: Read-S3Object -BucketName nasanex -KeyPrefix /AVHRR -Folder Z:/nasanex/AVHRR -Region us-west-2.<br>&emsp;+ Tạo file share.<br>&emsp;+ Cấu hình cả HDD và SSD FSx.<br>&emsp;+ Cập nhật phiên bản công cụ đã cũ ở phần 25.4.<br>&emsp;+ Thực hiện benchmark ổ đĩa thành công với các tham số khác nhau.<br>&emsp;+ Sử dụng CloudWatch để giám sát hiệu năng — thông lượng (throughput) đạt tối đa 400 MB, kích hoạt cảnh báo.<br>&emsp;+ Tìm hiểu về tính năng deduplication (chống trùng lặp) của FSx:<br>&emsp;&emsp;• Lịch mặc định chạy vào thứ Bảy hàng tuần.<br>&emsp;&emsp;• Lần chạy dedup đầu tiên không tối ưu được gì do cài đặt fileAge mặc định -> chỉnh fileAge về 0 -> ~50% file được tối ưu.<br>&emsp;+ Tạo shadow copy để backup.<br>&emsp;+ Học cách quản lý và buộc đóng (force-close) các file đang mở.<br>&emsp;+ Cấu hình hạn mức người dùng (user quotas) để giới hạn dung lượng lưu trữ.<br>&emsp;+ Bật tính năng Continuously Available (CA) file shares để nhiều người dùng có thể truy cập cùng lúc.<br>&emsp;+ Mở rộng throughput và dung lượng lưu trữ từ AWS Console.<br>- Ôn tập Mô hình Trách nhiệm Chia sẻ: cả AWS và khách hàng đều chia sẻ trách nhiệm bảo mật.<br>- Module 5-2: Best practice là tạo một IAM user quản trị thay vì dựa vào tài khoản root.<br>- IAM Principal: Một thực thể được phép truy cập tài nguyên AWS.<br>- IAM Policy: Có thể dựa trên danh tính hoặc tài nguyên.<br>- IAM Role: Tập hợp các quyền hạn cho user/service, và có thể dùng cho truy cập xuyên tài khoản (cross-account).<br>- Môn học ở trường:<br>&emsp;+ ENW493c: Hoàn thành khóa học Understanding Research Methods. | 22/09/2025 | 22/09/2025 | [Lab25](https://000025.awsstudygroup.com/1-introduce/) <br><br> |
| T3 | - Module 5:<br>- Amazon Cognito: Dịch vụ xác thực và quản lý người dùng với hai thành phần chính:<br>&emsp;+ User Pools: Lưu thông tin người dùng và hỗ trợ các nhà cung cấp danh tính bên thứ ba.<br>&emsp;+ Identity Pools: Ánh xạ người dùng tới các quyền hạn và thông tin xác thực tạm thời.<br>- AWS Organizations: Quản lý tập trung nhiều tài khoản AWS sử dụng OU và Service Control Policies (SCP).<br>- AWS Identity Center (SSO): Quản lý truy cập ứng dụng và tài khoản AWS thông qua các bộ quyền (permission sets).<br>- AWS KMS: Tạo và quản lý khóa mã hóa (CMK), dùng để tạo và mã hóa/giải mã các data key.<br>- AWS Security Hub: Đánh giá tình trạng bảo mật dựa trên các best practice của AWS.<br>- Tiếp tục Lab 14:<br>&emsp;+ Thiết lập IAM role và S3 bucket.<br>&emsp;+ Ubuntu 25.04 thất bại do kernel không hỗ trợ -> thử Ubuntu 24.04 -> vẫn không hỗ trợ -> cài đặt thành công Ubuntu 22.04.<br>&emsp;+ Import máy ảo (VM) vào AWS.<br>&emsp;+ Kết nối tới EC2 instance được tạo từ AMI bằng username/password của VM. | 23/09/2025 | 23/09/2025 | [Lab 14](https://000014.awsstudygroup.com/) |
| T4 | Tiếp tục với lab 14:<br>&emsp; + Tạo export bucket, cấu hình quyền hạn <br>&emsp; + Export thành công instance sang định dạng .OVA để sử dụng <br>- Lab 18: Bật Security Hub và cấu hình AWS Config để ghi lại dữ liệu phân tích (Có thể mất nhiều thời gian để tính điểm) | 24/09/2025 | 24/09/2025 | [Lab 14](https://000014.awsstudygroup.com/) |
| T5 | - Lab 22:<br>&emsp;+ Xây dựng Lambda function để tự động start/stop EC2 instance sử dụng lịch trình và tag.<br>&emsp;+ Gửi thông báo đến Slack.<br>- Lab 28:<br>&emsp;+ Tạo IAM policy và role để chỉ cho phép truy cập từ vùng Singapore.<br>&emsp;+ Chặn truy cập EC2 từ bên ngoài vùng được cho phép.<br>&emsp;+ Chặn tạo EC2 instance nếu không có tag hợp lệ.<br>- Lab 30: Hạn chế IAM user để họ chỉ có thể truy cập EC2 ở một vùng cụ thể.<br>- Cập nhật Lab 18: Quét Security Hub hoàn tất — điểm số: 85%, có 1 lỗi nghiêm trọng (một IAM user vẫn có quyền admin).<br>- Lab 33:<br>&emsp;+ Thiết lập KMS.<br>&emsp;+ Cấu hình CloudTrail để gửi log đến S3.<br>&emsp;+ Truy vấn log bằng Athena.<br>&emsp;+ Xác minh rằng KMS từ chối truy cập đối với người dùng không được phép một cách chính xác. | 25/09/2025 | 25/09/2025 | [Lab 22](https://000022.awsstudygroup.com/) <br><br> [Lab 28](https://000028.awsstudygroup.com/) <br><br> [Lab 30](https://000030.awsstudygroup.com/) <br><br> [Lab 18](https://000018.awsstudygroup.com/) <br><br> [Lab 33](https://000033.awsstudygroup.com/) |
| T6 | - Lab 44: Cấu hình điều kiện cho role, hạn chế truy cập theo IP, Thời gian và các yếu tố khác<br> - Lab 48:<br>&emsp; + Sử dụng IAM access key để upload file lên S3 qua EC2 Instance <br>&emsp; + Upload file lên S3 qua EC2 Instance không dùng access key mà sử dụng IAM Roles <br> - Lab 12: <br>&emsp; + Tạo AWS Organization <br>&emsp; + Tạo tài khoản và di chuyển chúng vào các unit (OU) <br>&emsp; + Mời các tài khoản vào tổ chức <br>&emsp; + Chuyển đổi role cho các tài khoản trong tổ chức <br>&emsp; + Thiết lập policy cho các tài khoản trong tổ chức <br>&emsp; + Cài đặt Python để tiếp tục bài lab <br> | 26/09/2025 | 26/09/2025 | [Lab 44](https://000044.awsstudygroup.com/) <br><br> [Lab 48](https://000048.awsstudygroup.com/) <br><br> [Lab 12](https://000012.awsstudygroup.com/) <br><br> |


## **Thành tựu Tuần 3**

* Đã nâng cấp tài khoản AWS và hoàn thành các bài lab trước đây bị chặn do giới hạn Free Tier.
* Giải quyết nhiều vấn đề tương thích (ví dụ: Lambda runtime cũ, kernel không hỗ trợ).
* Hoàn thành thiết lập **Amazon FSx** nâng cao trong Lab 25:
  * Deduplication, shadow copy, user quota, mở rộng, giám sát CloudWatch.
* Hoàn thành lý thuyết Module 5: IAM, Cognito, Organizations, Identity Center, KMS.
* Áp dụng bảo mật IAM thực tế:
  * Hạn chế vùng (Lab 28 & 30)
  * Điều kiện IAM theo IP/thời gian (Lab 44)
  * Upload S3 an toàn dùng IAM Role (Lab 48)
* Bật Security Hub & AWS Config (Lab 18) → Đạt điểm đánh giá bảo mật **85%**.
* Xây dựng tự động hóa Lambda để lập lịch cho EC2 tích hợp với Slack (Lab 22).
* Import thành công VM, tạo AMI, và export EC2 ra file .OVA (Lab 14).
* Thiết lập AWS Organization với các OU, SCP, chuyển đổi role, và quản lý user/group (Lab 12).
* Hoàn thành các bài lab Microsoft Workloads:
  * Quản lý AD
  * Khắc phục sự cố EC2 qua sửa chữa volume
  * Gán license với Microsoft AD
* Cấu hình CloudTrail, lưu log vào S3, và dùng Athena để phân tích log (Lab 33), với KMS thực thi kiểm soát truy cập.