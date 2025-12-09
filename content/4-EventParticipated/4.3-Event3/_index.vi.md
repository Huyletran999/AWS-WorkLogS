
---
title: "Sự kiện 3"
date: "2025-11-17"
weight: 3
chapter: false
pre: " <b> 4.3. </b> "
---

# Báo cáo Tóm tắt: “AWS Cloud Mastery Series #2 - DevOps trên AWS”

### Mục tiêu Sự kiện

- Giới thiệu các dịch vụ AWS DevOps – Quy trình CI/CD
- Giới thiệu Cơ sở hạ tầng dưới dạng mã (IaC) và các công cụ liên quan
- Giới thiệu các Dịch vụ Container trên AWS
- Đảm bảo khả năng Giám sát (Monitoring) và Quan sát (Observability) sử dụng các dịch vụ AWS

### Diễn giả

- **Truong Quang Tinh** – AWS Community Builder, Kỹ sư Nền tảng (Platform Engineer) - TymeX
- **Bao Huynh** – AWS Community Builder
- **Nguyen Khanh Phuc Thinh** – AWS Community Builder
- **Tran Dai Vi** – AWS Community Builder
- **Huynh Hoang Long** – AWS Community Builder
- **Pham Hoang Quy** – AWS Community Builder
- **Nghiem Le** – AWS Community Builder
- **Dinh Le Hoang Anh** - Thực tập sinh Cloud Engineer, First Cloud AI Journey

### Điểm nhấn Chính

## Tư duy DevOps (DevOps Mindset)

**- Văn hóa:** Hợp tác, Tự động hóa, Học tập liên tục và Đo lường
**- Các vai trò DevOps:** Kỹ sư DevOps, Kỹ sư Cloud, Kỹ sư Nền tảng, Kỹ sư độ tin cậy trang web (SRE)
**- Chỉ số thành công:**
    + Đảm bảo sức khỏe của việc triển khai (deployment health)
    + Cải thiện sự linh hoạt (agility)
    + Tính ổn định của hệ thống
    + Tối ưu hóa trải nghiệm khách hàng
    + Chứng minh hiệu quả đầu tư công nghệ

| NÊN (DO) | KHÔNG NÊN (DON'T) |
| :--- | :--- |
| Bắt đầu từ những điều cơ bản | Kẹt trong vòng lặp hướng dẫn (Tutorial Hell) |
| Học bằng cách xây dựng dự án thực tế | Sao chép và dán một cách mù quáng |
| Tài liệu hóa mọi thứ | So sánh tiến độ của bạn với người khác |
| Thành thạo từng thứ một | Bỏ cuộc sau những thất bại |
| Nâng cao kỹ năng mềm | |

**- Tích hợp liên tục (CI):** Các thành viên trong nhóm tích hợp công việc của họ thường xuyên, hướng tới Chuyển giao liên tục (CD) và Triển khai liên tục.

## Cơ sở hạ tầng dưới dạng mã (IaC)

**- Lợi ích:** Tự động hóa, Khả năng mở rộng, Khả năng tái tạo và Hợp tác tốt hơn

## AWS CloudFormation

Công cụ IaC tích hợp sẵn của AWS, sử dụng các mẫu (templates) viết bằng YAML hoặc JSON, có thể xây dựng mọi cơ sở hạ tầng AWS một cách tự động.

**- Stack:** Một tập hợp các Tài nguyên AWS được định nghĩa trong một mẫu, có thể được CloudFormation sử dụng để tạo, cập nhật hoặc xóa các tài nguyên đó.

**- CloudFormation Template:** Một tệp YAML/JSON định nghĩa Cơ sở hạ tầng AWS, hoạt động như một bản thiết kế để triển khai và định cấu hình tài nguyên.

**- Cách thức hoạt động:** Tạo mẫu -> Lưu trữ trong S3 Bucket hoặc bộ nhớ cục bộ -> Sử dụng CloudFormation để tạo Stack dựa trên mẫu -> CloudFormation xây dựng tài nguyên.

**- Phát hiện sai lệch (Drift Detection):** Phát hiện các thay đổi trong cơ sở hạ tầng thực tế so với Stack => Cập nhật Stack hoặc hoàn tác thay đổi, hữu ích cho việc kiểm soát phiên bản.

## AWS Cloud Development Kit (CDK)

Khung phát triển phần mềm nguồn mở, hỗ trợ IaC bằng các ngôn ngữ lập trình thực (Python, Java, C#.Net, Type/JavaScript và Go).

**- Construct:** Các khối xây dựng, bao gồm các thành phần đại diện cho Tài nguyên AWS và Cấu hình của chúng, có 3 cấp độ construct:
  + L1 Construct: Tài nguyên cấp thấp ánh xạ trực tiếp đến một tài nguyên AWS CloudFormation đơn lẻ.
  + L2 Construct: Cung cấp mức độ trừu tượng cao hơn thông qua API dựa trên ý định trực quan, đóng gói các phương pháp hay nhất (best practices) và mặc định bảo mật.
  + L3 Construct: Các mẫu kiến trúc hoàn chỉnh với nhiều tài nguyên, được triển khai theo định hướng sẵn (opinionated) và triển khai nhanh chóng.

## AWS Amplify

Nền tảng AWS giúp dễ dàng xây dựng, triển khai và mở rộng các ứng dụng web và di động, sử dụng CloudFormation bên dưới: Các Stack được triển khai để xây dựng cơ sở hạ tầng theo chương trình.

## Terraform

Công cụ IaC, bắt đầu bằng việc định nghĩa cơ sở hạ tầng trong mã Terraform, lên kế hoạch (plan) và sau đó áp dụng (apply) cơ sở hạ tầng trên nhiều nền tảng đám mây như Azure, AWS, Google Cloud, v.v.

**- Điểm mạnh:** Hỗ trợ đa đám mây (Multi-Cloud), Theo dõi trạng thái (State tracking) với cùng một cấu hình.

## Cách chọn công cụ IaC?
**- Tiêu chí:**
  + Kế hoạch sử dụng một Đám mây hay nhiều Đám mây?
  + Vai trò là Developer hay Ops?
  + Hệ sinh thái và Đám mây đó có hỗ trợ công cụ không?

## Dịch vụ Container trên AWS

## Dockerfile

Dockerfile định nghĩa cách xây dựng một container image, mô tả môi trường, các phụ thuộc, các bước xây dựng và cấu hình runtime cuối cùng, đảm bảo ứng dụng chạy nhất quán trên mọi hệ thống hỗ trợ Docker.

**- Images:** Một bản thiết kế đóng gói của ứng dụng, được xây dựng từ Dockerfile sử dụng hệ thống tệp phân lớp, dùng để tạo các container nhất quán trên các môi trường.

**- Quy trình:** Dockerfile xây dựng Docker Image, image này có thể được dùng để chạy Container và đẩy lên ECR/Docker Hub.

## Amazon ECR

Một container registry được quản lý hoàn toàn giúp dễ dàng lưu trữ, quản lý và chia sẻ bảo mật các Docker container image.
Đây là registry container riêng tư, bảo mật và có khả năng mở rộng của chính AWS.

**- Tính năng:**
  + Quét Image (Image Scanning)
  + Thẻ bất biến (Immutable Tags)
  + Chính sách vòng đời (Lifecycle Policies)
  + Mã hóa & IAM

**- Điều phối (Orchestration):** Điều phối nhiều quy trình container: khởi động lại container, tự động mở rộng khi tải cao, phân phối lưu lượng hiệu quả, quản lý vị trí đặt và chạy container.

## Kubernetes
Mã nguồn mở, tự động hóa việc triển khai, mở rộng, phục hồi và cân bằng tải.
**- Thành phần:**
  + Master Node: Control Plane, quản lý các worker node và pod.
  + Worker Node: Chạy khối lượng công việc ứng dụng bên trong các pod.
  + Pod: Đơn vị triển khai nhỏ nhất, có thể chứa một hoặc nhiều container.
  + Service

So sánh ECS và EKS

| Tính năng | Amazon ECS (Elastic Container Service) | Amazon EKS (Elastic Kubernetes Service) |
| :--- | :--- | :--- |
| **Công nghệ cốt lõi** | Điều phối container gốc của AWS (AWS-native) | Dựa trên Kubernetes (tiêu chuẩn nguồn mở) |
| **Độ phức tạp** | Đơn giản hơn, dễ vận hành hơn | Linh hoạt cao nhưng **phức tạp** hơn |
| **Kiến thức yêu cầu** | **Không cần kiến thức Kubernetes** | Yêu cầu **kiến thức Kubernetes** (pods, deployments, v.v.) |
| **Tích hợp AWS** | Tích hợp sâu với AWS (ALB, IAM, CloudWatch, v.v.) | Tích hợp Kubernetes tiêu chuẩn |
| **Trường hợp sử dụng/Lợi ích** | Tuyệt vời cho **triển khai nhanh** & **chi phí vận hành thấp** | **Đa cụm (Multi-cluster)**, **khả năng di động đa đám mây** |
| **Hệ sinh thái/Cộng đồng** | Công cụ gốc AWS và cộng đồng | **Hệ sinh thái lớn hơn** & công cụ cộng đồng |
| **Tóm tắt** | ECS = dễ hơn, chạy nhanh hơn, **chi phí vận hành thấp hơn** | EKS = linh hoạt hơn, kiểm soát nhiều hơn, **phức tạp hơn** |

## App Runner

Phù hợp để triển khai nhanh các ứng dụng web và REST API, lý tưởng cho khối lượng công việc sản xuất từ nhỏ đến trung bình.

## Giám sát & Khả năng quan sát (Monitoring & Observability)

## CloudWatch
- Giám sát các Tài nguyên AWS và Ứng dụng chạy trên AWS trong thời gian thực
- Cung cấp khả năng quan sát
- Cảnh báo và phản hồi tự động
- Dashboard giúp tối ưu hóa vận hành và chi phí

**- CloudWatch metrics:** Dữ liệu về hiệu suất của hệ thống trên AWS hoặc on-premise với CloudWatch Agent, tích hợp tốt với EventBridge, Auto Scaling và quy trình DevOps.

## AWS X-Ray
**- Truy vết phân tán (Distributed Tracing):** Theo dõi các yêu cầu từ đầu đến cuối, vẽ bản đồ và đường đi giữa các dịch vụ đã truy cập, thêm SDK vào mã để theo dõi ID.

**- Performance Insight:** Phân tích nguyên nhân gốc rễ cho độ trễ và lỗi, suy ra thông tin chi tiết từ các dấu vết (traces) và cung cấp Giám sát Người dùng Thực (Real User Monitoring).

### Trải nghiệm Sự kiện

Sự kiện này rất quan trọng đối với dự án của chúng tôi vì nó giải quyết kế hoạch thêm IaC sử dụng CDK, thay vì sử dụng ClickOps, để tăng khả năng bảo trì và tái tạo. Ngoài ra, một số thông tin chi tiết về CloudWatch cũng giúp ích rất nhiều cho tính năng giám sát dữ liệu của chúng tôi.

Các diễn giả đã trả lời câu hỏi của nhóm:

- Hỏi: Dự án của chúng tôi cho đến nay hoàn toàn được xây dựng bằng ClickOps (thao tác thủ công trên console), và chúng tôi đang định sử dụng CDK. Có công cụ nào có thể quét và chuyển đổi cơ sở hạ tầng hiện có thành CDK hoặc CloudFormation thay vì phải tái tạo lại cơ sở hạ tầng từ đầu bằng IaC không?
- Đáp: Rất tiếc là không, chưa có công cụ nào có thể hỗ trợ vấn đề đó, nhóm của bạn sẽ phải xây dựng lại cơ sở hạ tầng từ đầu. Nếu tình cờ bạn tìm thấy một công cụ có thể hỗ trợ, hãy chia sẻ với chúng tôi nhé.

- Hỏi: Chúng tôi nhận thấy AWS X-Ray dùng với CloudWatch tương tự như CloudTrail trong phương pháp theo dõi, bạn có thể giải thích thêm về điểm khác biệt giữa chúng không?
- Đáp: X-Ray được sử dụng cho CloudWatch và dùng để theo dõi các tài nguyên và dịch vụ mà hệ thống đã tương tác, trong khi CloudTrail thường được sử dụng để theo dõi hành động của người dùng (user) AWS.

- Hỏi: Dự án của chúng tôi được xây dựng xoay quanh GuardDuty Findings, bạn có kinh nghiệm nào về cách kích hoạt Findings một cách đáng tin cậy cho các kịch bản demo không?
- Đáp: Theo kinh nghiệm của tôi, GuardDuty Findings có thể được kích hoạt bởi các hoạt động quét cổng (port scanning), nhưng tôi chắc chắn còn có những cách khác.
- Đáp: GuardDuty có thể được cấu hình để có một danh sách mối đe dọa (threat list) chứa các quy tắc tùy chỉnh để kích hoạt các finding khi có hoạt động liên quan đến các tên miền hoặc IP độc hại đã được cấu hình.

Sự kiện này cũng là lần đầu tiên một số diễn giả trình bày về một chủ đề:
- Các phần về DevOps và IaC được trình bày rất tốt.
- Phần Giám sát & Khả năng quan sát chưa thực sự xuất sắc và chúng tôi có thể nhận thấy sự lo lắng của diễn giả nhưng vẫn mang lại những giá trị tuyệt vời.

#### Một số hình ảnh sự kiện
![Ảnh nhóm chụp trong sự kiện bởi diễn giả Tran Dai Vi](/images/Events/CM2GroupPic.jpg)