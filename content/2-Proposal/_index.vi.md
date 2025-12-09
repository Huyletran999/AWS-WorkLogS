---
title: "Bản đề xuất"
date: "2000-01-01"
weight: 2
chapter: false
pre: " <b> 2. </b> "
---

![AWS Logo](/images/2-Proposal/image.png)

# Bản Đề Xuất Dự Án Thực Tập FCJ

# Hệ thống Ứng phó Sự cố và Điều tra Số Tự động trên AWS

**Thực hiện bởi:** The Ballers – Đại học FPT  
**Ngày:** 5 tháng 12 năm 2025  
**Chương trình:** Thực tập AWS First Cloud Journey (FCJ)  
**Thời lượng dự án:** 6 Tuần  
**Trạng thái:** Sẵn sàng cho Xem xét & Phê duyệt <br>
**Liên kết Đề xuất:** [Proposal](https://docs.google.com/document/d/1RcPJmiVxS80qdi0wOvHltBcSoZtRC97LngEZEkKC09k/edit?brid=hv-MPz2j8n_U1ZiCdslbyw&tab=t.0) 

## Mục lục

1. [Bối cảnh và Động lực](#1-boi-canh-va-dong-luc)
2. [Kiến trúc Giải pháp](#2-kien-truc-giai-phap--so-do-kien-truc)
3. [Hoạt động và Sản phẩm bàn giao](#3-hoat-dong-va-san-pham-ban-giao)
4. [Phân tích Chi phí AWS Dự kiến theo Dịch vụ](#4-phan-tich-chi-phi-aws-du-kien-theo-dich-vu)
5. [Đội ngũ](#5-doi-ngu)
6. [Nguồn lực & Ước tính Chi phí](#6-nguon-luc--uoc-tinh-chi-phi)
7. [Nghiệm thu](#7-nghiem-thu)

## 1. Bối cảnh và Động lực

### 1.1 Tóm tắt Dự án

Nhóm của chúng tôi đang xây dựng một giải pháp ứng phó sự cố và điều tra số tự động như một phần của chương trình thực tập AWS First Cloud Journey. Ý tưởng rất đơn giản—khi một vấn đề bảo mật xảy ra trong AWS, chúng tôi muốn hệ thống phản ứng tự động mà không cần chờ đợi sự can thiệp thủ công.

Chúng tôi đang tạo ra một nền tảng tự động phát hiện các phát hiện bảo mật từ GuardDuty, cô lập các tài nguyên bị ảnh hưởng, thu thập bằng chứng pháp y thông qua việc thu thập dữ liệu toàn diện, và cung cấp các phân tích và bảng điều khiển để các đội bảo mật có thể điều tra những gì đã xảy ra. Mọi thứ được xây dựng bằng Infrastructure-as-Code với AWS CDK, vì vậy khách hàng có thể dễ dàng triển khai nó vào tài khoản AWS của riêng họ.

Các trường hợp sử dụng chính bao gồm phát hiện việc sử dụng trái phép thông tin xác thực AWS, xác định các EC2 instance bị xâm nhập, và đảm bảo dữ liệu pháp y được thu thập, xử lý và lưu trữ đúng cách để điều tra. Kiến trúc của chúng tôi tích hợp VPC Flow Logs, CloudTrail, và GuardDuty để phát hiện các mối đe dọa, trong khi Step Functions điều phối quy trình ứng phó tự động bao gồm cô lập EC2, tách khỏi ASG, và cách ly IAM. Tất cả bằng chứng được thu thập và xử lý thông qua Lambda ETL tùy chỉnh và Data Firehose, sử dụng Athena để phân tích pháp y.

### 1.2 Tiêu chí Thành công của Dự án

Chúng tôi đo lường sự thành công thông qua các mục tiêu chính sau:

* Triển khai thành công một bộ điều phối ứng phó sự cố đầy đủ chức năng mà khách hàng có thể sử dụng ngay sau khi cài đặt
* Giảm thời gian điều tra từ hàng giờ xuống còn vài phút bằng cách tự động hóa việc thu thập bằng chứng và phản ứng
* Đảm bảo tất cả bằng chứng pháp y được thu thập, xử lý và lưu trữ đúng cách
* Bàn giao mọi thứ đúng tiến độ trong thời hạn 6 tuần của chúng tôi
* Giữ chi phí triển khai dưới 5$/tháng cho mức sử dụng thông thường
* Cho phép tất cả các thành viên trong nhóm thể hiện năng lực về các dịch vụ bảo mật AWS, kiến trúc serverless, thu thập pháp y và bảo vệ ứng dụng web.

### Vấn đề Chúng tôi Muốn Giải quyết

Tần suất và sự tinh vi ngày càng tăng của các mối đe dọa mạng đặt ra những rủi ro đáng kể cho các tổ chức dựa vào cơ sở hạ tầng đám mây. Quy trình ứng phó sự cố thủ công thường chậm chạp, không nhất quán và dễ mắc lỗi của con người, có thể dẫn đến thời gian ngừng hoạt động hệ thống kéo dài, vi phạm dữ liệu và tổn thất tài chính. Dự án nhằm giải quyết những thách thức này bằng cách phát triển một hệ thống ứng phó sự cố tự động, đáng tin cậy và có khả năng mở rộng, giúp giảm thiểu thời gian phản hồi, tăng cường khả năng pháp y và giảm chi phí vận hành.

### Lợi ích

* Phát hiện mối đe dọa nhanh chóng và phản ứng tự động giúp giảm thiểu khoảng thời gian dễ bị tổn thương.
* Thu thập dữ liệu pháp y tự động đảm bảo thu thập bằng chứng toàn diện, tạo điều kiện cho các cuộc điều tra nhanh hơn.
* Triển khai hiệu quả về chi phí tận dụng các dịch vụ serverless của AWS giúp giảm thiểu chi phí cơ sở hạ tầng.
* Cải thiện tư thế bảo mật thông qua giám sát liên tục và cảnh báo thời gian thực.
* Trao quyền cho các đội bảo mật với những hiểu biết sâu sắc có thể hành động thông qua bảng điều khiển và phân tích.
* Kiến trúc có khả năng mở rộng thích ứng với các tổ chức có quy mô và khối lượng sự cố khác nhau.

### 1.3 Giả định

**Giả định về Khách hàng:**

* Khách hàng có tài khoản AWS với quyền phù hợp để triển khai ứng dụng CDK của chúng tôi.
* Khách hàng có sự quen thuộc cơ bản với các dịch vụ AWS và có thể chạy các lệnh CLI và CMD đơn giản.
* GuardDuty đã được bật hoặc khách hàng sẵn sàng bật nó như một phần của quy trình thiết lập.
* Khách hàng muốn một giải pháp trọn gói cho việc triển khai ban đầu.
* Nhóm có quyền truy cập nhất quán vào AWS trong thời gian dự án 6 tuần.

**Phụ thuộc và Ràng buộc:**

* Giải pháp của chúng tôi chỉ tích hợp với các dịch vụ gốc của AWS (tại thời điểm hiện tại).
* Thu thập pháp y bao gồm VPC Flow Logs, DNS Logs, CloudTrail, và EC2 snapshot.
* Chúng tôi sử dụng các dịch vụ có sẵn trong bậc miễn phí hoặc chi phí thấp (Lambda, Step Functions, Data Firehose, Athena).
* Tất cả cơ sở hạ tầng được định nghĩa trong AWS CDK (Python) để triển khai có thể tái tạo.
* Bảng điều khiển là trang web tĩnh lưu trữ trên S3 với xác thực Cognito, CloudFront CDN.
* Chúng tôi tuân theo các nguyên tắc của AWS Well-Architected Framework trong suốt quá trình.

### Giảm thiểu Rủi ro

Để giải quyết các thách thức tiềm ẩn liên quan đến việc triển khai các dịch vụ AWS và xử lý dữ liệu pháp y ở quy mô lớn, một kế hoạch giảm thiểu rủi ro toàn diện nên được áp dụng. Kế hoạch này bao gồm các biện pháp sau:

* **Đào tạo và Phát triển Kỹ năng:** Ngoài việc đào tạo ban đầu, thiết lập các chương trình giáo dục liên tục và chứng chỉ cho các thành viên trong nhóm để cập nhật các tiến bộ và thực tiễn tốt nhất của AWS. Điều này giúp giảm độ khó khi học tập và nâng cao hiệu quả hoạt động.
* **Tối ưu hóa Hiệu suất Mạnh mẽ:** Thường xuyên xem xét và tinh chỉnh các truy vấn Athena và cấu hình Data Firehose. Triển khai các công cụ giám sát tự động để phát hiện sớm các tắc nghẽn hiệu suất và điều chỉnh tài nguyên động để duy trì thông lượng tối ưu.
* **Bảo mật Dữ liệu và Tuân thủ:** Kết hợp các giao thức bảo mật nghiêm ngặt, bao gồm mã hóa, kiểm soát truy cập và ghi nhật ký kiểm toán, để bảo vệ dữ liệu pháp y nhạy cảm. Đảm bảo tuân thủ các quy định liên quan như GDPR, HIPAA hoặc các tiêu chuẩn cụ thể của ngành.
* **Khôi phục sau Thảm họa và Duy trì Hoạt động Kinh doanh:** Phát triển và thử nghiệm các kế hoạch khôi phục sau thảm họa bao gồm sao lưu dữ liệu, quy trình chuyển đổi dự phòng và các biện pháp dự phòng để giảm thiểu thời gian ngừng hoạt động và mất dữ liệu khi có sự cố.
* **Lập kế hoạch Mở rộng:** Dự đoán sự tăng trưởng dữ liệu và khối lượng công việc trong tương lai bằng cách thiết kế kiến trúc có khả năng mở rộng. Sử dụng các tính năng tự động mở rộng và công cụ quản lý chi phí để tối ưu hóa việc sử dụng tài nguyên và kiểm soát chi phí.
* **Đánh giá Nhà cung cấp và Công nghệ:** Liên tục đánh giá các bản cập nhật dịch vụ AWS và các giải pháp thay thế để đảm bảo các công cụ được chọn vẫn hiệu quả và tiết kiệm chi phí khi các yêu cầu thay đổi.

Việc thực hiện các chiến lược giảm thiểu rủi ro nâng cao này sẽ cung cấp một khuôn khổ linh hoạt hơn để quản lý sự phức tạp của việc xử lý dữ liệu pháp y và triển khai dịch vụ đám mây, cuối cùng làm giảm rủi ro hoạt động và đảm bảo tính toàn vẹn và bảo mật dữ liệu.

## 2. Kiến trúc Giải pháp / Sơ đồ Kiến trúc

### 2.1 Sơ đồ Kiến trúc Kỹ thuật

![AWS Architecture](/images/2-Proposal/AWSWorkshopArchitecture-Stepfunctions.drawio.png)

Giải pháp của chúng tôi sử dụng một kiến trúc đa giai đoạn toàn diện cho việc ứng phó sự cố và điều tra số tự động:

#### Lớp Thu thập Dữ liệu & Phát hiện

Hệ thống thu thập các sự kiện bảo mật từ nhiều nguồn:

* **VPC Flow Logs và DNS Logs** từ các giao diện mạng ghi lại các mẫu lưu lượng mạng.
* **CloudTrail** ghi lại tất cả các cuộc gọi API và hoạt động quản lý của AWS.
* **EC2 Instances** tạo ra dữ liệu đo lường từ cấp hệ thống.
* **GuardDuty** liên tục theo dõi các mối đe dọa bảo mật và hoạt động đáng ngờ.
* **CloudWatch** thu thập các số liệu và nhật ký từ tài nguyên AWS.

#### Lớp Xử lý Sự kiện

Khi GuardDuty phát hiện một phát hiện:

* **Event Bridge** định tuyến các phát hiện đến Step Functions của chúng tôi.
* Các sự kiện được phân loại theo loại để xác định hành động ứng phó.

#### Điều phối Ứng phó Tự động (Quy trình Step Functions)

Máy trạng thái Step Functions của chúng tôi điều phối việc ứng phó sự cố với các hành động tuần tự sau:

1. **Phân tích Phát hiện (Parse Findings)** - Trích xuất thông tin quan trọng từ sự kiện bảo mật.
2. **Loại Phát hiện (Finding Type)** - Điểm quyết định để xác định chiến lược ứng phó.
3. **Cô lập EC2 (Isolate EC2)** - Loại bỏ instance bị xâm nhập khỏi môi trường sản xuất và cô lập chúng.
4. **Bảo vệ Chấm dứt & Gắn thẻ (Termination Protection & Tagging)** - Bảo vệ instance và gắn thẻ cho pháp y.
5. **Tách khỏi ASG (Detach ASG)** - Tách instance khỏi Auto Scaling Group.
6. **Tạo Snapshot** - Bắt đầu tạo EBS snapshot để phân tích pháp y.
7. **Cách ly IAM (Quarantine IAM)** - Cô lập thông tin xác thực và quyền hạn.

#### Lớp Cảnh báo & Thông báo

* **Amazon SNS** phân phối cảnh báo đến nhiều kênh.
* **Alert Dispatch** định tuyến các thông báo một cách thích hợp.
* **Simple Email Service (SES)** gửi thông báo qua email.
* **Nền tảng nhắn tin bên thứ ba (Slack)** gửi cảnh báo thời gian thực đến các đội bảo mật.

#### Lớp Xử lý Dữ liệu & Phân tích

Dữ liệu pháp y thu thập được chảy qua:

* **CloudWatch** logs để phân tích ngay lập tức.
* **Dữ liệu Nhật ký Thô** được lưu trữ trong S3 để lưu giữ lâu dài.
* **DATA ETL** pipeline xử lý dữ liệu thô.
* **Data Firehose** truyền dữ liệu đã xử lý đến S3 bucket.
* **Dữ liệu Đã xử lý** lưu trữ thông tin pháp y đã được chuẩn hóa.
* **Athena** cho phép thực hiện các truy vấn SQL trên các tập dữ liệu pháp y.

#### Lớp Bảng điều khiển & Phân tích

Các nhà phân tích bảo mật truy cập các công cụ điều tra thông qua:

* **Giao diện Truy vấn Bảng điều khiển** cho các cuộc điều tra.
* **API Gateway** cung cấp quyền truy cập lập trình vào dữ liệu pháp y.
* **Athena** cung cấp kết quả truy vấn SQL thời gian thực.
* **S3 Static Dashboard** cung cấp giao diện điều tra trực quan.
* **Cognito** xử lý xác thực và ủy quyền.
* **CloudFront** CDN tăng tốc độ phân phối bảng điều khiển.

**Đầu ra & Thông báo:**

* Các cảnh báo cuối cùng và phát hiện được gửi đến **Slack và Email**.
* **Người dùng** (đội bảo mật) nhận được thông tin tình báo có thể hành động để điều tra.

### 2.2 Kế hoạch Kỹ thuật

Nhóm của chúng tôi phát triển toàn bộ giải pháp bằng cách sử dụng AWS Cloud Development Kit (CDK) với Python. CDK cho phép chúng tôi viết cơ sở hạ tầng dưới dạng mã, cho phép kiểm soát phiên bản, kiểm thử và tùy chỉnh dễ dàng bởi khách hàng.

**Cách tiếp cận:**

Tạo một dự án CDK với các cấu trúc mô-đun đại diện cho từng lớp kiến trúc:
* Lớp phát hiện (GuardDuty, CloudWatch, tích hợp EventBridge, CloudTrail).
* Lớp điều phối (Step Functions, Lambda functions cho từng hành động).
* Lớp thu thập dữ liệu (Data Firehose, lưu trữ S3, quy trình ETL).
* Lớp phân tích (Athena, dashboards, API Gateway, CloudFront).
* Lớp thông báo (SNS, SES, tích hợp bên thứ ba).

**Quy trình Step Functions:**
* Máy trạng thái với logic quyết định dựa trên loại phát hiện.
* Các phát hiện kích hoạt ngay lập tức việc ngăn chặn (cô lập EC2, tách ASG, cách ly IAM).

**Step Functions:**
Được viết bằng Python để tương thích với AWS SDK.

Trách nhiệm cụ thể:
* **Phân tích Phát hiện (Lambda)** - Trích xuất và chuẩn hóa dữ liệu GuardDuty.
* **Cô lập EC2 (Lambda)** - Sửa đổi security groups và loại bỏ khỏi load balancers.
* **Bảo vệ Instance** - Thiết lập bảo vệ chấm dứt và gắn thẻ pháp y.
* **Tách khỏi ASG** - Tách instance khỏi auto scaling group.
* **Tạo Snapshot** - Bắt đầu tạo EBS snapshot để phân tích pháp y.
* **Cách ly IAM (Lambda)** - Áp dụng các chính sách hạn chế cho thông tin xác thực bị xâm nhập.

Sự phân tách các mối quan tâm cho phép kiểm thử dễ dàng và cập nhật độc lập.

**Đường ống Thu thập Dữ liệu:**
* Nhật ký được xuất từ CloudWatch và CloudTrail.
* ETL dựa trên Lambda chuẩn hóa các định dạng dữ liệu.
* Data Firehose truyền dữ liệu pháp y đã xử lý đến S3 với phân vùng tự động.
* Các bảng Athena được tạo để truy vấn SQL hiệu quả.

**Phát triển Bảng điều khiển:**
* Giao diện HTML/CSS/JavaScript (React) tĩnh được lưu trữ trên S3.
* Tích hợp Cognito để xác thực.
* API Gateway kết nối bảng điều khiển với các chức năng Lambda.
* Kết quả truy vấn thời gian thực từ Athena.
* CloudFront CDN lưu trữ bộ đệm bảng điều khiển và kết quả truy vấn.

**Kiểm thử:**
* Kiểm thử tích hợp mô phỏng các phát hiện GuardDuty thực tế.
* Kiểm thử đầu cuối (End-to-end) xác nhận các quy trình ứng phó hoàn chỉnh.

---

### 2.3 Kế hoạch Dự án

Chúng tôi sử dụng Agile Scrum với các sprint 1 tuần trong vòng 6 tuần (tổng cộng 6 sprint).

**Sprint 1:**
* Đào tạo nhóm về GuardDuty, Step Functions, Data Firehose, Athena.
* Xem xét thiết kế kiến trúc với cố vấn AWS.
* Thiết lập VPC và security group.

**Sprint 2:**
* Triển khai quy trình Step Functions với tất cả logic điều phối.
* Phát triển các hàm Lambda cho từng hành động ứng phó.
* Tích hợp GuardDuty và EventBridge.
* Thiết lập SNS và SES cho thông báo.
* Kiểm thử tích hợp các luồng ứng phó sự cố.
* Sản phẩm bàn giao: Bộ điều phối hoạt động đầu cuối phản ứng với các phát hiện bảo mật.

**Sprint 3:**
* Tạo lưu trữ dữ liệu pháp y dựa trên S3.
* Phát triển các bảng Athena và truy vấn để phân tích pháp y.
* Triển khai xử lý dữ liệu ETL.
* Sản phẩm bàn giao: Đường ống thu thập và phân tích dữ liệu pháp y hoạt động.

**Sprint 4:**
* Xây dựng giao diện bảng điều khiển tĩnh được lưu trữ trên S3.
* Tạo kết nối API Gateway đến các chức năng backend.
* Tích hợp kết quả truy vấn Athena vào bảng điều khiển.
* Thiết lập CloudFront CDN.
* Sản phẩm bàn giao: Bảng điều khiển hoạt động.

**Sprint 5:**
* Triển khai xác thực Cognito.
* Kiểm thử hiệu suất của các đường ống dữ liệu và truy vấn.
* Mô phỏng các kịch bản sự cố.
* Kiểm thử thủ công và sửa lỗi.
* Triển khai Firehose để tối ưu hóa.
* Tối ưu hóa các truy vấn Athena.

**Sprint 6 (Tài liệu & Bàn giao):**
* Tạo hướng dẫn triển khai.
* Quay video demo.
* Các phiên chuyển giao kiến thức.
* Sản phẩm bàn giao: Tài liệu hoàn chỉnh và kho lưu trữ GitHub/GitLab công khai.

**Các nghi thức Sprint:**
* Họp đứng (standup) 30 phút nửa tuần một lần để đồng bộ tiến độ.
* Đánh giá sprint hàng tuần trình bày công việc đã hoàn thành.
* Họp cải tiến (restrospective) để thảo luận về những gì đã làm tốt và các lĩnh vực cần cải thiện.

---

### 2.4 Cân nhắc về Bảo mật

Chúng tôi thực hiện bảo mật trên năm khía cạnh chính:

**Kiểm soát Truy cập:**
* Mỗi hàm Lambda chỉ nhận được các quyền cụ thể cần thiết cho hành động của nó.
* Quản lý cẩn thận vai trò và chính sách IAM với đặc quyền tối thiểu.
* Xác thực Cognito cho quyền truy cập bảng điều khiển.

**Bảo mật Cơ sở hạ tầng:**
* Cơ sở hạ tầng trong các private VPC subnet nếu có thể.
* Security groups hạn chế lưu lượng giữa các thành phần.
* VPC Flow Logs cho khả năng hiển thị mạng.
* GuardDuty để phát hiện mối đe dọa thời gian thực trong nhật ký.
* CloudTrail ghi lại mọi cuộc gọi API cho các dấu vết kiểm toán đầy đủ.
* Các quy tắc EventBridge được xác thực và hạn chế.

**Bảo vệ Dữ liệu:**
* Mã hóa AES-256 cho tất cả bằng chứng pháp y trong S3.
* TLS 1.2+ cho tất cả việc truyền dữ liệu giữa các dịch vụ.
* Mã hóa khi truyền cho các luồng Data Firehose.

**Phát hiện & Giám sát:**
* CloudWatch giám sát các hàm Lambda, thực thi Step Functions và các số liệu.
* Bảng điều khiển tùy chỉnh để theo dõi sự cố thời gian thực.
* Ghi nhật ký truy vấn Athena cho các dấu vết kiểm toán.

**Ứng phó Sự cố:**
* Tự động cô lập EC2 khi xảy ra các phát hiện bảo mật.
* Bằng chứng pháp y được thu thập ngay lập tức.
* Chuỗi hành trình (chain of custody) đầy đủ với nhật ký có dấu thời gian.
* Cách ly thông tin xác thực IAM.
* Thông báo cho đội bảo mật qua Slack và Email.
* Lưu giữ bằng chứng trong thời gian điều tra.

## 3. Hoạt động và Sản phẩm bàn giao

### 3.1 Hoạt động và Sản phẩm bàn giao

| Giai đoạn Dự án | Thời gian | Hoạt động | Sản phẩm bàn giao |
| :--- | :--- | :--- | :--- |
| **Nền tảng & Thiết lập** | Tuần 6-7 | Thiết lập dự án CDK với các cấu trúc mô-đun, đào tạo nhóm về GuardDuty/Step Functions/Firehose, xem xét thiết kế kiến trúc, thiết lập VPC và bảo mật. | Kho lưu trữ dự án CDK hoạt động, tài liệu kiến trúc v1, hoàn thành đào tạo nhóm, kho lưu trữ GitHub được thiết lập. |
| **Điều phối Cốt lõi** | Tuần 7-9 | Phát triển quy trình Step Functions, lập trình hàm Lambda cho tất cả các hành động ứng phó, tích hợp EventBridge, thiết lập SNS/SES, kiểm thử tích hợp. | Định nghĩa máy trạng thái Step Functions, hơn 7 hàm Lambda có tài liệu, tích hợp GuardDuty, hệ thống thông báo, API Gateway. |
| **Dữ liệu & Phân tích** | Tuần 10 | Triển khai Data Firehose, thiết lập lưu trữ pháp y S3, tạo bảng Athena, phát triển đường ống ETL, thư viện truy vấn SQL. | Đường ống Data Firehose, hơn 15 truy vấn Athena được ghi lại, sách hướng dẫn phân tích pháp y, lưu trữ dữ liệu đã xử lý. |
| **Bảng điều khiển & UI** | Tuần 11 | Phát triển bảng điều khiển tĩnh, xác thực Cognito, thiết lập API Gateway, cấu hình CloudFront CDN, tích hợp bảng điều khiển. | Bảng điều khiển lưu trữ trên S3, hệ thống xác thực, giao diện truy vấn, tích hợp kết quả thời gian thực. |
| **Kiểm thử & Xác thực** | Tuần 12 | Kiểm thử thủ công, quét bảo mật bao gồm các kịch bản sự cố mô phỏng (hơn 5 quy trình), kiểm thử hiệu suất, mô phỏng tấn công. | Kết quả quét bảo mật, video mô phỏng sự cố. |
| **Tài liệu & Bàn giao** | Tuần 13 | Hướng dẫn triển khai, tài liệu API, các phiên chuyển giao kiến thức, demo cuối cùng, dọn dẹp GitHub. | Kho lưu trữ GitHub hoàn chỉnh (công khai), hướng dẫn triển khai, buổi trình diễn workshop trực tiếp. |

**Quản trị:**

* GitHub và GitLab để kiểm soát phiên bản với lịch sử cam kết đầy đủ.
* Các cuộc họp với thành viên và cố vấn AWS FCJ để xem xét kiến trúc.
* Đánh giá sprint hàng tuần với các bên liên quan (nhóm của chúng tôi).
* Sổ đăng ký rủi ro được cập nhật nửa tuần một lần trong các cuộc họp đứng.

---

### 3.2 Ngoài Phạm vi

Những mục này KHÔNG được bao gồm trong dự án của chúng tôi:

* Pháp y cho các tài nguyên bên ngoài AWS (máy chủ tại chỗ, máy tính người dùng).
* Tư vấn pháp lý hoặc chứng nhận chính thức về khả năng chấp nhận bằng chứng trước tòa.
* Tích hợp với các hệ thống bán vé (ServiceNow, Jira) - chỉ triển khai ban đầu.
* Kiểm thử tải cho hàng chục nghìn sự cố đồng thời.
* Các mô hình học máy để dự đoán mối đe dọa.
* Chứng nhận tuân thủ (PCI-DSS, ISO 27001) - thiết kế tuân theo các nguyên tắc nhưng không được chứng nhận.
* WAF
* Lambda@Edge (chỉ có sẵn cho các gói thanh toán theo mức sử dụng).
* Tự động hóa khôi phục sau thảm họa đa vùng (multi-region).
* Cognito nâng cao với MFA – chỉ xác thực cơ bản.
* Bảo vệ DDoS nâng cao (AWS Shield Advanced) - chỉ bảo vệ tiêu chuẩn.
* Glue ETL Jobs và Crawler.
* Các dịch vụ bảo mật bên thứ ba.

### 3.3 Đường đến Môi trường Thực tế (Path to Production)

Chúng tôi đang cung cấp một bằng chứng khái niệm (PoC) sẵn sàng cho sản xuất và nền tảng cho tự động hóa ứng phó sự cố. Nó đầy đủ chức năng để trình diễn, hội thảo và triển khai quy mô vừa và nhỏ.

Đối với triển khai doanh nghiệp lớn, khách hàng sẽ cần thêm:

* Quy trình leo thang tự động và tích hợp luân phiên trực ban.
* Tích hợp hệ thống bán vé doanh nghiệp (ServiceNow, Jira).
* Kết nối nền tảng nhắn tin bổ sung (Teams, PagerDuty).
* Tối ưu hóa cho khối lượng sự cố lớn mỗi ngày.
* Khả năng chuyển đổi dự phòng đa vùng và khôi phục sau thảm họa.
* Tích hợp công cụ pháp y nâng cao.
* Xác thực tuân thủ và ánh xạ quy định (HIPAA, GDPR, PCI-DSS).
* Tích hợp SIEM để ghi nhật ký tập trung.
* Các tính năng AWS WAF Premium (kiểm soát bot, thông tin mối đe dọa nâng cao).
* Tích hợp phân tích và ghi nhật ký WAF nâng cao.
* AWS Shield Advanced DDoS

Chúng tôi được thiết kế như một nền tảng dễ dàng xây dựng thêm.

## 4. Phân tích Chi phí AWS Dự kiến theo Dịch vụ

Đây là bảng phân tích chi phí triển khai hàng tháng điển hình sử dụng bậc miễn phí:

[**Ước tính Giá**](https://calculator.aws/#/estimate?id=b9b2c0423dcd3b21dadd62e5053a5fdf2d003339)

| Dịch vụ AWS | Chi phí Hàng tháng | Tại sao Chúng tôi Sử dụng | Khu vực |
| :--- | :---: | :--- | :--- |
| **Lambda** | $0-1 | Chạy các hàm tự động hóa của chúng tôi | Châu Á Thái Bình Dương (Singapore) |
| **SES** | $0.09-1 | Gửi Email | Châu Á Thái Bình Dương (Singapore) |
| **Amazon EventBridge** | $0-1 | Định tuyến sự kiện | Châu Á Thái Bình Dương (Singapore) |
| **Step Functions** | $0-1 | Điều phối quy trình làm việc | Châu Á Thái Bình Dương (Singapore) |
| **S3** | $1.07-2 | Lưu trữ bằng chứng pháp y | Châu Á Thái Bình Dương (Singapore) |
| **Athena** | $0.29-1 | Truy vấn SQL trên dữ liệu pháp y | Châu Á Thái Bình Dương (Singapore) |
| **GuardDuty** | $1.80-2 | Phát hiện các phát hiện bảo mật | Châu Á Thái Bình Dương (Singapore) |
| **CloudTrail** | $0.55-1 | Ghi nhật ký tất cả các hành động | Châu Á Thái Bình Dương (Singapore) |
| **CloudWatch** | $0-1 | Giám sát và bảng điều khiển | Châu Á Thái Bình Dương (Singapore) |
| **SNS** | $0-1 | Thông báo sự cố | Châu Á Thái Bình Dương (Singapore) |
| **API Gateway** | $0.05-1 | API backend cho bảng điều khiển | Châu Á Thái Bình Dương (Singapore) |
| **Cognito** | $0-1 | Xác thực bảng điều khiển | Châu Á Thái Bình Dương (Singapore) |
| **CloudFront** | $0-1 | Tăng tốc CDN cho bảng điều khiển | Châu Á Thái Bình Dương (Singapore) |
| **EC2 (t3.micro)** | $0-1 | Các instance phân tích tùy chọn | Châu Á Thái Bình Dương (Singapore) |
| **KMS** | $1.12-2 | Quản lý khóa | Châu Á Thái Bình Dương (Singapore) |
| **Firehose** | $0.04-1 | Phân phối dữ liệu | Châu Á Thái Bình Dương (Singapore) |
| **Tổng cộng** | **$5.01-19** | | |

**Giả định Chính:**

Đối với thiết lập của chúng tôi, chi phí khoảng **$5.01** cho cả tháng với mức sử dụng này:

* Mức sử dụng thông thường: 20-150 sự cố mỗi tháng
* Bảng điều khiển được phục vụ qua CloudFront với WAF
* Truy vấn Athena được tối ưu hóa với phân vùng

**Tôi đã thêm $1 vào mỗi dịch vụ để mở rộng quy mô với CƠ SỞ HẠ TẦNG LỚN HƠN.**

---

## 5. Đội ngũ

**Trưởng Chương trình AWS FCJ (Cố vấn/Mentor)**

* **Tên:** Nguyễn Gia Hưng
* **Chức danh:** Head of Solutions Architect
* **Mô tả:** Cung cấp cố vấn kỹ thuật, xem xét kiến trúc và hướng dẫn thực tiễn tốt nhất của AWS.
* **Email:** hunggia@amazon.com

**Các bên liên quan của Dự án**
* **Nhóm:** Các Cố vấn AWS FCJ.
* **Chức danh:** Người hướng dẫn Chương trình
* **Bên liên quan cho:** Giám sát học thuật, đánh giá dự án, tín chỉ thực tập

**Nhóm Thực tập (Đại học FPT)**

| Tên | Chức danh | Vai trò | Email |
| :--- | :--- | :--- | :--- |
| **Huỳnh An Khương** | Trưởng nhóm | Điều phối, Thiết kế kiến trúc, CDK, GuardDuty, Lambda, ETL Pipeline, Phân tích pháp y. | huynhankhuong0511@gmail.com |
| **Mai Quốc Anh** | Thành viên | Quản lý Dự án (Jira), Cảnh báo (Email/Telegram), Xác thực, Thiết kế bảng điều khiển. | maiquocanh2608@gmail.com |
| **Nguyễn Trần Minh Quân** | Thành viên | Lambda, ETL Pipeline, Phân tích pháp y, Cảnh báo (Slack). | nguyentranminhquanb@gmail.com |
| **Lâm Gia Kiệt** | Thành viên | Thiết kế/triển khai bảng điều khiển, CDK, CloudFront, API Gateway. | lamgiakiet2005@gmail.com |
| **Lê Trần Gia Huy** | Thành viên | Lambda, Phát triển tự động hóa Step Functions, GuardDuty, Eventbridge, Policies và IAM roles. | huyletran188205@gmail.com |

**Liên hệ Leo thang Dự án**

* **Tên:** Huỳnh An Khương
* **Chức danh:** Trưởng nhóm
* **Vai trò:** Liên hệ chính về tình trạng dự án và leo thang
* **Email:** huynhankhuong0511@gmail.com

---

## 6. Nguồn lực & Ước tính Chi phí

**Phân bổ Nguồn lực**

| Nguồn lực | Trách nhiệm |
| :--- | :--- |
| **Huỳnh An Khương** | Điều phối, Thiết kế kiến trúc, CDK, GuardDuty, Lambda, ETL Pipeline, Phân tích pháp y |
| **Mai Quốc Anh** | Quản lý Dự án (Jira), Cảnh báo (Email/Telegram), Xác thực, Thiết kế bảng điều khiển, Bản đề xuất. |
| **Lâm Gia Kiệt** | Phát triển bảng điều khiển, CDK, CloudFront, API Gateway, Quy trình làm việc Gitlab |
| **Nguyễn Trần Minh Quân** | Lambda, ETL Pipeline, Phân tích pháp y, Cảnh báo (Slack), Xác thực (Validation), Tài liệu |
| **Lê Trần Gia Huy** | Lambda, Phát triển tự động hóa Step Functions, GuardDuty, Eventbridge, Policies và IAM roles. |

Chi phí quá thấp để chúng tôi thực sự tính toán chi phí Tỷ lệ(USD)/Giờ.

**Giờ theo Giai đoạn Dự án**

| Giai đoạn Dự án | Huỳnh An Khương | Mai Quốc Anh | Lâm Gia Kiệt | Nguyễn Trần Minh Quân | Lê Trần Gia Huy | Tổng số giờ |
| ---: | :---: | :---: | :---: | :---: | :---: | :---: |
| *Nền tảng* | 30 | 30 | 30 | 30 | 30 | 150 |
| *Điều phối Cốt lõi* | 30 | 30 | 30 | 30 | 30 | 150 |
| *Lớp Phân tích* | 30 | 30 | 30 | 30 | 30 | 150 |
| *Kiểm thử & Xác thực* | 30 | 30 | 30 | 30 | 30 | 150 |
| *Tài liệu & Bàn giao* | 30 | 30 | 30 | 30 | 30 | 150 |
| **Tổng số giờ** | **150** | **150** | **150** | **150** | **150** | **750** |

Không dễ để có được thời gian chính xác chúng tôi dành cho dự án, mặc dù chúng tôi trung bình 5 giờ mỗi ngày cho nó, vì vậy tôi sẽ viết 5 cho mỗi ngày.

**Phân bổ Chi phí**

| Bên | Đóng góp (USD) | % Tổng cộng |
| ---: | :--- | :---: |
| *Chương trình AWS FCJ* | $0 (Thực tập phi lợi nhuận) | 0% (tín chỉ học thuật) |
| *Đại học FPT* | Lao động sinh viên (thực tập) | 0% (tín chỉ học thuật) |
| *AWS* | $15 (Bao gồm chạy thử nghiệm.) | 100% |
| **Tổng Chi phí Dự án** | **$15** | **100%** |

Điều này hiệu quả về chi phí vì các thành viên trong nhóm đang hoàn thành việc này như một phần kỳ thực tập của họ (tính vào yêu cầu học thuật) và AWS chi trả chi phí cơ sở hạ tầng thông qua chương trình FCJ.

## 7. Nghiệm thu

### Tiêu chí Nghiệm thu Giai đoạn

Sau khi hoàn thành mỗi giai đoạn, nhóm nộp các sản phẩm bàn giao cho Trưởng Chương trình AWS FCJ và các bên liên quan của dự án. Trong vòng 5 ngày làm việc, người đánh giá sẽ đánh giá các sản phẩm bàn giao dựa trên các tiêu chí nghiệm thu. Nếu được chấp thuận, giai đoạn sẽ được nghiệm thu. Nếu có vấn đề, nhóm sẽ nhận được phản hồi cụ thể và có 5 ngày làm việc để giải quyết và nộp lại.

**Nghiệm thu Giai đoạn 1:** Tài liệu kiến trúc được xem xét và phê duyệt, tất cả thành viên nhóm hoàn thành khóa đào tạo AWS, kho lưu trữ GitHub được thiết lập và hoạt động với tài liệu phù hợp.

**Nghiệm thu Giai đoạn 2:** Quy trình Step Functions chạy đầu cuối mà không bị lỗi, các hàm Lambda được kiểm thử và hoạt động, tích hợp EventBridge hoạt động, thông báo SNS kích hoạt chính xác, kiểm thử tích hợp, mã không có vấn đề bảo mật nghiêm trọng.

**Nghiệm thu Giai đoạn 3:** Lưu trữ S3 hoạt động với phân vùng phù hợp, các bảng Athena có thể truy vấn, quy trình ETL chuẩn hóa dữ liệu chính xác, tài liệu hoàn chỉnh với hơn 15 ví dụ truy vấn.

**Nghiệm thu Giai đoạn 4:** Bảng điều khiển tải không có lỗi, API Gateway kết nối với backend, CloudFront CDN phục vụ nội dung, kết quả truy vấn hiển thị theo thời gian thực, giao diện thân thiện với người dùng được kiểm thử.

**Nghiệm thu Giai đoạn 5:** Xác thực Cognito hoạt động, các quy trình sự cố mô phỏng thực thi chính xác từ đầu đến cuối, điểm chuẩn hiệu suất đáp ứng mục tiêu (sự cố được xử lý trong vòng 60 giây).

**Nghiệm thu Giai đoạn 6:** Hướng dẫn triển khai đủ rõ ràng để người mới tham gia dự án có thể làm theo và thiết lập hệ thống, kho lưu trữ GitHub công khai với README toàn diện, bản demo trực tiếp chạy mà không có vấn đề lớn, tài liệu bài học kinh nghiệm của nhóm.

### Đánh giá Thành công Dự án

Dự án được coi là thành công nếu:

* Tất cả các giai đoạn được nghiệm thu đúng hạn hoặc trong vòng 1 tuần kể từ thời hạn
* Các thành viên trong nhóm có thể chứng minh sự hiểu biết về các dịch vụ AWS được sử dụng (GuardDuty, Step Functions, Data Firehose, Athena, Cognito, v.v.)
* Kho lưu trữ GitHub công khai và bao gồm tài liệu đầy đủ
* Buổi trình diễn workshop trực tiếp cho thấy thành công hoạt động ứng phó sự cố từ phát hiện đến phân tích bảng điều khiển.
* Hướng dẫn triển khai cho phép một nhóm mới thiết lập hệ thống độc lập trong vòng 1 giờ.
* Chi phí AWS duy trì trong mức ước tính $5/tháng cho mức sử dụng thông thường
* Ứng phó sự cố đầu cuối hoàn thành trong vòng 60 giây.

---

## Phụ lục

### Phụ lục A: Ngăn xếp Công nghệ

**Frontend & Bảng điều khiển:**
* HTML/CSS/JavaScript tùy chỉnh
* AWS Management Console
* API Gateway (tạo điều kiện kết nối giữa bảng điều khiển tĩnh và các chức năng dữ liệu pháp y backend.)
* CloudFront (CDN để tăng tốc độ phân phối bảng điều khiển tĩnh được lưu trữ trên S3.)

**Backend & Xử lý:**
* AWS Step Functions (điều phối quy trình làm việc)
* AWS Lambda (Python 3.12)
* Amazon EC2 (các instance phân tích)
* Amazon EventBridge (bộ định tuyến sự kiện gửi các phát hiện bảo mật từ GuardDuty đến quy trình làm việc Step Functions.)

**Dữ liệu & Lưu trữ:**
* Amazon S3 (lưu trữ bằng chứng pháp y)
* Amazon EBS (snapshots)
* Amazon Athena (truy vấn SQL trên dữ liệu S3)
* AWS CloudTrail (nhật ký kiểm toán)
* AWS CloudWatch (nhật ký luồng)
* Firehose (chịu trách nhiệm truyền dữ liệu pháp y đã xử lý đến S3)

**Cơ sở hạ tầng & Tự động hóa:**
* AWS CDK (Cơ sở hạ tầng dưới dạng Mã, Python)
* GitHub (kiểm soát phiên bản và CI/CD)
* GitLab (kiểm soát phiên bản và CI/CD)

**Bảo mật & Giám sát:**
* Amazon GuardDuty (phát hiện mối đe dọa)
* Amazon CloudWatch (giám sát và cảnh báo)
* Amazon Cognito (xác thực)
* SNS (Phân phối cảnh báo sự cố đến các kênh như Slack và Email.)
* SES (Gửi thông báo email như một phần của quy trình cảnh báo.)
* KMS (Được sử dụng để quản lý khóa, điều cần thiết cho AES-256)

### Phụ lục B: Thuật ngữ Chính

| Thuật ngữ | Định nghĩa |
| :--- | :--- |
| **AWS FCJ** | AWS First Cloud Journey - chương trình thực tập cho sinh viên |
| **GuardDuty** | Dịch vụ AWS tự động phát hiện các mối đe dọa bảo mật |
| **Step Functions** | Dịch vụ AWS để điều phối các quy trình làm việc serverless |
| **Lambda** | AWS serverless compute - chạy mã không cần quản lý máy chủ |
| **CDK** | AWS Cloud Development Kit - viết cơ sở hạ tầng dưới dạng mã |
| **Forensics** | Thu thập và phân tích bằng chứng từ các sự cố bảo mật |
| **Chain of Custody** | Chuỗi hành trình bằng chứng đầy đủ hiển thị ai đã chạm vào bằng chứng nào khi nào |
| **Incident Response** | Quy trình ứng phó với các sự kiện bảo mật |
| **IaC** | Infrastructure as Code - định nghĩa cơ sở hạ tầng trong mã |

### Phụ lục C: Tài liệu Tham khảo

* Hướng dẫn Quy định của AWS: Tự động hóa ứng phó sự cố và pháp y ([https://aws.amazon.com/prescriptive-guidance/](https://aws.amazon.com/prescriptive-guidance/))
* AWS Well-Architected Framework ([https://aws.amazon.com/architecture/well-architected/](https://aws.amazon.com/architecture/well-architected/))
* Tài liệu AWS Step Functions ([https://docs.aws.amazon.com/step-functions/](https://docs.aws.amazon.com/step-functions/))
* Các thực tiễn tốt nhất cho AWS Lambda ([https://docs.aws.amazon.com/lambda/](https://docs.aws.amazon.com/lambda/))
* Tài liệu AWS CDK ([https://docs.aws.amazon.com/cdk/](https://docs.aws.amazon.com/cdk/))
* Chi tiết Bậc Miễn phí AWS ([https://aws.amazon.com/free/](https://aws.amazon.com/free/))

---

**Phiên bản Tài liệu:** 1.0  
**Cập nhật lần cuối:** 8 tháng 12 năm 2025  
**Trạng thái:** Sẵn sàng cho Xem xét & Phê duyệt  
**Mã Dự án:** AWS-FCJ-IR-FORENSICS-2025