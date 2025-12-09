---
title: "Worklog Tuần 10"
date: 2025-09-10
weight: 10
chapter: false
pre: " <b> 1.10. </b> "
---



### Mục tiêu tuần 10:

* Nghiên cứu kỹ lưỡng và kiểm thử tất cả các thành phần để chuẩn bị tích hợp vào bản dựng cuối cùng của workshop.


### Các công việc cần triển khai trong tuần này---
title: "Nhật ký công việc Tuần 10"
date: "2025-11-10"
weight: 2
chapter: false
pre: " <b> 1.10. </b> "
---
### Mục tiêu Tuần 10:

* Nghiên cứu và kiểm thử toàn diện tất cả các thành phần để chuẩn bị tích hợp vào bản build cuối cùng của workshop.

### Các nhiệm vụ thực hiện trong tuần này:

| Ngày | Nhiệm vụ | Ngày bắt đầu | Ngày hoàn thành | Tài liệu tham khảo |
| :---: | :--- | :--------: | :-------------: | :----------------- |
| T2 | - Kiểm thử cô lập EC2 với sự kiện giả lập (mock events) và phát hiện thực tế từ GuardDuty (đã debug và sửa các hàm xử lý dữ liệu để phù hợp với cấu trúc JSON của phát hiện thực tế).<br> - Cập nhật đề xuất:<br>&emsp; + Bao gồm Kiến trúc AWS và các Dịch vụ đã cập nhật.<br>&emsp; + Tính toán lại ước tính chi phí. | 10/11/2025 | 10/11/2025 | |
| T3 | - Kiểm thử cô lập IAM (quarantine) và hiện đang giải quyết các vấn đề xử lý dữ liệu tương tự.<br> - Xây dựng thành công tất cả các policy và role với quyền truy cập tối thiểu (least-privilege). | 11/11/2025 | 11/11/2025 | |
| T4 | - Xây dựng thành công thiết kế Step Functions bao gồm các trạng thái: Kiểm tra loại phát hiện (Check Finding Types), Cô lập EC2, Cách ly người dùng (Quarantine Users), và Không cần hành động (No Action Needed). | 12/11/2025 | 12/11/2025 | |
| T5 | - Kiểm thử thành công các Lambda function với cả sự kiện giả lập và một số phát hiện thực tế sử dụng các script mới.<br> - Hiện đang hướng tới việc xây dựng các script có khả năng phân tích mọi loại phát hiện.<br> - Nghiên cứu cách tối ưu hóa cấu trúc Lambda -> EventBridge -> Step Functions. | 13/11/2025 | 13/11/2025 | |

### Thành tựu Tuần 10:

* **Điều phối Ứng phó sự cố:**
  * Thiết kế và triển khai thành công quy trình AWS Step Functions, với các trạng thái logic riêng biệt cho "Check Finding Types," "Isolate EC2," "Quarantine IAM User," và "No Action Needed."
  

* **Kiểm thử & Debug thực tế:**
  * Chuyển từ kiểm thử với sự kiện giả lập sang xử lý các phát hiện thực tế từ Amazon GuardDuty.
  * Debug và tinh chỉnh thành công logic phân tích dữ liệu của Lambda để diễn giải chính xác cấu trúc JSON phức tạp của các cảnh báo GuardDuty thực tế cho cả kịch bản EC2 và IAM.

* **Triển khai Bảo mật & IAM:**
  * Kiến trúc và triển khai thành công tất cả các IAM role và inline policy cần thiết cho các function cách ly, tuân thủ nghiêm ngặt nguyên tắc **quyền truy cập tối thiểu (least-privilege)** để đảm bảo an toàn.

* **Tài liệu Dự án & Tối ưu hóa:**
  * Cập nhật đề xuất dự án để phản ánh việc chuyển đổi sang kiến trúc Step Functions và cung cấp các tính toán lại cho chi phí đám mây dự kiến.
  * Bắt đầu nghiên cứu tối ưu hóa mô hình tích hợp giữa AWS EventBridge và Step Functions để đảm bảo kích hoạt tự động nhanh hơn và tin cậy hơn.
| Thứ | Công việc                                                                                                                                                                                   | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu                            |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------ | --------------- | ----------------------------------------- |
| 2   | - Làm quen với các thành viên FCJ <br> - Đọc và lưu ý các nội quy, quy định tại đơn vị thực tập                                                                                             | 11/08/2025   | 11/08/2025      |
| 3   | - Tìm hiểu AWS và các loại dịch vụ <br>&emsp; + Compute <br>&emsp; + Storage <br>&emsp; + Networking <br>&emsp; + Database <br>&emsp; + ... <br>                                            | 12/08/2025   | 12/08/2025      | <https://cloudjourney.awsstudygroup.com/> |
| 4   | - Tạo AWS Free Tier account <br> - Tìm hiểu AWS Console & AWS CLI <br> - **Thực hành:** <br>&emsp; + Tạo AWS account <br>&emsp; + Cài AWS CLI & cấu hình <br> &emsp; + Cách sử dụng AWS CLI | 13/08/2025   | 13/08/2025      | <https://cloudjourney.awsstudygroup.com/> |
| 5   | - Tìm hiểu EC2 cơ bản: <br>&emsp; + Instance types <br>&emsp; + AMI <br>&emsp; + EBS <br>&emsp; + ... <br> - Các cách remote SSH vào EC2 <br> - Tìm hiểu Elastic IP   <br>                  | 14/08/2025   | 15/08/2025      | <https://cloudjourney.awsstudygroup.com/> |
| 6   | - **Thực hành:** <br>&emsp; + Tạo EC2 instance <br>&emsp; + Kết nối SSH <br>&emsp; + Gắn EBS volume                                                                                         | 15/08/2025   | 15/08/2025      | <https://cloudjourney.awsstudygroup.com/> |


### Kết quả đạt được tuần 10:

* Hiểu AWS là gì và nắm được các nhóm dịch vụ cơ bản: 
  * Compute
  * Storage
  * Networking 
  * Database
  * ...

* Đã tạo và cấu hình AWS Free Tier account thành công.

* Làm quen với AWS Management Console và biết cách tìm, truy cập, sử dụng dịch vụ từ giao diện web.

* Cài đặt và cấu hình AWS CLI trên máy tính bao gồm:
  * Access Key
  * Secret Key
  * Region mặc định
  * ...

* Sử dụng AWS CLI để thực hiện các thao tác cơ bản như:

  * Kiểm tra thông tin tài khoản & cấu hình
  * Lấy danh sách region
  * Xem dịch vụ EC2
  * Tạo và quản lý key pair
  * Kiểm tra thông tin dịch vụ đang chạy
  * ...

* Có khả năng kết nối giữa giao diện web và CLI để quản lý tài nguyên AWS song song.
* ...



