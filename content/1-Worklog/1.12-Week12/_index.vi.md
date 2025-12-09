---
title: "Nhật ký công việc Tuần 12"
date: "2025-11-24"
weight: 2
chapter: false
pre: " <b> 1.12. </b> "
---
### Mục tiêu Tuần 12:

* Khởi tạo và xác thực môi trường Infrastructure as Code (CDK).
* Nâng cao quy trình Phản ứng sự cố với khả năng thu thập chứng cứ pháp y tự động (SSM).
* Debug và tinh chỉnh Lambda function và IAM role để đảm bảo hoạt động tin cậy.

### Các nhiệm vụ thực hiện trong tuần này:

| Ngày | Nhiệm vụ | Ngày bắt đầu | Ngày hoàn thành | Tài liệu tham khảo |
| :---: | :--- | :--------: | :-------------: | :----------------- |
 |
| T3 | - **Cập nhật IR Step Functions:** Thêm **Map State** để lặp qua các Instance bị cô lập và kích hoạt SSM Lambda cho các Instance đó để thu thập log phục vụ điều tra số (forensics).<br> - **CDK:** Chuyển môi trường kiểm thử CDK sang một tài khoản chuyên biệt mới. | 26/11/2025 | 26/11/2025 | |
| T6 | - **Họp nhóm:**<br>&emsp; + Phân công nhiệm vụ CDK cho các thành viên <br>&emsp; + Bắt đầu cập nhật đề xuất và sơ đồ kiến trúc <br> - **Sửa lỗi và cải tiến IR Step Functions:** <br>&emsp; + Sửa lỗi `EC2Isolate` Lambda: Chỉnh lại phương thức parse dữ liệu <br>&emsp; + Cải thiện trạng thái: Thêm Parsing Lambda và sắp xếp lại các function <br>&emsp; + SSM bị lỗi do thiếu IAM: Đã thêm các role cần thiết vào SSM Forensics Function. | 28/11/2025 | 30/11/2025 | |

### Thành tựu Tuần 12:
* **Logic Phản ứng sự cố & Điều tra số:**
  * Nâng cấp quy trình Step Functions bằng cách triển khai **Map State**, cho phép hệ thống lặp và xử lý đồng thời nhiều EC2 instance bị cô lập.
  
  * Tích hợp **SSM (Systems Manager) Lambda** để tự động kích hoạt thu thập log chứng cứ pháp y trên các instance bị xâm nhập.

* **Debug & Tối ưu hóa:**
  * Tinh chỉnh logic xử lý dữ liệu bằng cách sửa các lỗi parse JSON trong `EC2Isolate` Lambda.
  * Giải quyết các vấn đề về quyền hạn bằng cách gán đúng **IAM Role** cho SSM Forensics function, đảm bảo function có quyền thực thi lệnh trên EC2 instance.
  * Tối ưu hóa cấu trúc quy trình bằng cách sắp xếp lại các trạng thái và thêm một Parsing Lambda chuyên biệt để luồng dữ liệu tốt hơn.