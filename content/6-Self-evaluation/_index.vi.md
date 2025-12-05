---
title: "Tự đánh giá"
date: 2025-09-10
weight: 6
chapter: false
pre: " <b> 6. </b> "
---



Trong suốt thời gian thực tập tại **Amazon Web Services** từ **9/2025** đến **12/2025**, tôi đã có cơ hội học hỏi, rèn luyện và áp dụng kiến thức đã được trang bị tại trường vào môi trường làm việc thực tế.  
Tôi đã tham gia **Phát triển Autonomous Incident Response** với các tasks EventBridge (Trigger), AWS Lambda Functions, AWS Step Functions (Core Logic). 
### Báo cáo Tổng kết Kỹ năng & Hạng mục đã thực hiện

Trong quá trình triển khai dự án, tôi đã thực hiện các nội dung sau:

1.  **Orchestration với AWS Step Functions:**
    * Thiết lập tích hợp trực tiếp **AWS SDK** (Service Integration) để gọi API EC2 và Auto Scaling, loại bỏ sự phụ thuộc vào Lambda trung gian.
    * Xử lý luồng dữ liệu (Data Flow) giữa các state: sử dụng `ResultPath: null` để bảo toàn dữ liệu và `States.Array` để xử lý mảng động.
    * Cấu hình các logic điều hướng phức tạp: rẽ nhánh (Choice), vòng lặp (Map) và cơ chế tự động thử lại (Retry).

2.  **Vận hành Auto Scaling Group (ASG):**
    * Thực hiện quy trình tách (Detach) instance khỏi ASG sử dụng tham số `ShouldDecrementDesiredCapacity` để duy trì hoạt động ứng dụng.
    * Xử lý các ràng buộc về dung lượng (Capacity Constraints), cụ thể là khắc phục lỗi logic MinSize bằng cách thêm bước `UpdateASGConfiguration`.

3.  **Debugging & Troubleshooting:**
    * Phân tích nguyên nhân gốc (Root Cause Analysis) thông qua việc kiểm tra Input/Output của từng Step.
    * Thực hiện kiểm thử cô lập (Isolation Testing) cho từng nhánh logic (ASG và Non-ASG) và sử dụng dữ liệu giả lập (Mock events).
    * Xác định và xử lý các lỗi logic không báo lỗi hệ thống (Silent Failure) và các lỗi môi trường (sai Region, định dạng ID).

4.  **Bảo mật & Quản lý Quyền hạn (IAM):**
    * Áp dụng nguyên tắc **Least Privilege**: Cấp quyền hạn chế qua Inline Policy cho từng hành động cụ thể (như DetachInstances, CreateSnapshot).
    * Triển khai quy trình kỹ thuật Ứng phó sự cố theo trình tự: Phát hiện $\rightarrow$ Cô lập (Security Group) $\rightarrow$ Bảo vệ (Termination Protection) $\rightarrow$ Thu thập bằng chứng (Snapshot).

5.  **Tự động hóa (Automation):**
    * Xây dựng hệ thống tự động hóa thay thế thao tác thủ công.
    * Thiết kế workflow đảm bảo tính **Idempotent** (cho phép chạy lại nhiều lần mà không gây lỗi trùng lặp) và khả năng xử lý linh hoạt cho cả instance thuộc ASG và không thuộc ASG. 

Về tác phong, tôi luôn cố gắng hoàn thành tốt nhiệm vụ, tuân thủ nội quy, và tích cực trao đổi với đồng nghiệp để nâng cao hiệu quả công việc.

Để phản ánh một cách khách quan quá trình thực tập, tôi xin tự đánh giá bản thân dựa trên các tiêu chí dưới đây:


| STT | Tiêu chí                            | Mô tả                                                                                            | Tốt | Khá | Trung bình |
| --- | ----------------------------------- | ------------------------------------------------------------------------------------------------ | --- | --- | ---------- |
| 1   | **Kiến thức và kỹ năng chuyên môn** | Hiểu biết về ngành, áp dụng kiến thức vào thực tế, kỹ năng sử dụng công cụ, chất lượng công việc | ✅   | ☐   | ☐          |
| 2   | **Khả năng học hỏi**                | Tiếp thu kiến thức mới, học hỏi nhanh                                                            | ☐   | ✅   | ☐          |
| 3   | **Chủ động**                        | Tự tìm hiểu, nhận nhiệm vụ mà không chờ chỉ dẫn                                                  | ☐  | ✅   | ☐          |
| 4   | **Tinh thần trách nhiệm**           | Hoàn thành công việc đúng hạn, đảm bảo chất lượng                                                | ✅   | ☐   | ☐          |
| 5   | **Kỷ luật**                         | Tuân thủ giờ giấc, nội quy, quy trình làm việc                                                   | ✅  | ☐   |  ☐         |
| 6   | **Tính cầu tiến**                   | Sẵn sàng nhận feedback và cải thiện bản thân                                                     | ✅   |☐    | ☐          |
| 7   | **Giao tiếp**                       | Trình bày ý tưởng, báo cáo công việc rõ ràng                                                     | ✅  | ☐   | ☐          |
| 8   | **Hợp tác nhóm**                    | Làm việc hiệu quả với đồng nghiệp, tham gia nhóm                                                 | ✅   | ☐   | ☐          |
| 9   | **Ứng xử chuyên nghiệp**            | Tôn trọng đồng nghiệp, đối tác, môi trường làm việc                                              | ✅   | ☐   | ☐          |
| 10  | **Tư duy giải quyết vấn đề**        | Nhận diện vấn đề, đề xuất giải pháp, sáng tạo                                                    | ✅   | ☐    | ☐          |
| 11  | **Đóng góp vào dự án/tổ chức**      | Hiệu quả công việc, sáng kiến cải tiến, ghi nhận từ team                                         | ✅   | ☐   | ☐          |
| 12  | **Tổng thể**                        | Đánh giá chung về toàn bộ quá trình thực tập                                                     | ✅   | ☐   | ☐          |

### Cần cải thiện

* Nâng cao tính kỹ luật, chấp hành nghiêm chỉnh nội quy của công ty hoặc bất kỳ trong một tổ chức nào
* Cải thiện trong cách tư duy giải quyết vấn đề
* Học cách giao tiếp tốt hơn trong giao tiếp hằng ngày và trong công việc, xử lý tình huống

