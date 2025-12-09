---
title: "Sự kiện 4"
date: "2025-11-29"
weight: 04
chapter: false
pre: " <b> 4.4. </b> "
---

# Báo cáo tóm tắt: “AWS Cloud Mastery Series #3: AWS Well-Architected – Security Pillar Workshop”

### Mục tiêu sự kiện

- Giới thiệu về AWS Cloud Club
- Trụ cột 1: Quản lý Danh tính & Truy cập (IAM)
- Trụ cột 2: Phát hiện & Giám sát liên tục
- Trụ cột 3: Bảo vệ Cơ sở hạ tầng
- Trụ cột 4: Bảo vệ Dữ liệu
- Trụ cột 5: Ứng phó sự cố

### Diễn giả

- **Lê Vũ Xuân An** - Chủ nhiệm AWS Cloud Club HCMUTE
- **Trần Đức Anh** - Chủ nhiệm AWS Cloud Club SGU
- **Trần Đoàn Công Lý** - Chủ nhiệm AWS Cloud Club PTIT
- **Danh Hoàng Hiếu Nghi** - Chủ nhiệm AWS Cloud Club HUFLIT

- **Huỳnh Hoàng Long** - AWS Community Builders
- **Đinh Lê Hoàng Anh** - AWS Community Builders

- **Nguyễn Tuấn Thịnh** - Thực tập sinh Kỹ sư Cloud
- **Nguyễn Đỗ Thành Đạt** - Thực tập sinh Kỹ sư Cloud

- **Văn Hoàng Kha** - Kỹ sư Bảo mật Cloud, AWS Community Builder

- **Thịnh Lâm** - Thành viên FCJ
- **Việt Nguyễn** - Thành viên FCJ

- **Mendel Grabski (Long)** - Cựu Trưởng bộ phận Bảo mật & DevOps, Kiến trúc sư Giải pháp Bảo mật Cloud
- **Tình Trương** - Kỹ sư Nền tảng tại TymeX, AWS Community Builder

### Các điểm nổi bật chính

### AWS Cloud Club
Giới thiệu về AWS Cloud Club:
- Giúp khám phá và phát triển kỹ năng điện toán đám mây
- Phát triển khả năng lãnh đạo kỹ thuật
- Xây dựng các kết nối có ý nghĩa trên toàn cầu
Cung cấp trải nghiệm thực tế với AWS, sự cố vấn từ các chuyên gia AWS và hỗ trợ sự nghiệp lâu dài.

Các AWS Cloud Club thuộc FCJA:
- AWS Cloud Club HCMUTE
- AWS Cloud Club SGU
- AWS Cloud Club PTIT
- AWS Cloud Club HUFLIT

Lợi ích: Xây dựng Kỹ năng, Cộng đồng và Cơ hội.

### Quản lý Danh tính & Truy cập (IAM)
IAM là một dịch vụ AWS thiết yếu, chịu trách nhiệm kiểm soát truy cập an toàn. IAM quản lý Người dùng (Users), Nhóm (Groups), Vai trò (Roles) và Quyền hạn (Permissions), đảm bảo cả việc xác thực (authentication) và ủy quyền (authorization).

- Các thực hành tốt nhất (Best Practices) bao gồm:

    + Nguyên tắc đặc quyền tối thiểu (Least Privilege Principle).

    + Xóa access keys của tài khoản root sau khi tạo.

    + Tránh dùng "*" trong Actions/Resources.

    + Sử dụng Đăng nhập một lần (SSO) để tích hợp đa tài khoản và quản lý truy cập tập trung.

- Service Control Policies (SCPs): Các chính sách cấp Tổ chức đặt ra quyền hạn tối đa khả dụng cho tất cả các tài khoản trong một Tổ chức. SCP chỉ lọc quyền; chúng không bao giờ cấp quyền.

- Permission Boundaries: Thiết lập quyền hạn tối đa mà một identity-based policy có thể cấp cho một User/Role cụ thể trong tài khoản.

- MFA (Xác thực đa yếu tố):
| TOTP (Time-based One-Time Password) | FIDO2 (Fast Identity Online 2) |
| :--- | :--- |
| **Bí mật chia sẻ (Shared secret)** | **Mật mã khóa công khai (Public-key cryptography)** |
| Yêu cầu nhập thủ công mã 6 chữ số | Yêu cầu chạm đơn giản hoặc quét sinh trắc học |
| Miễn phí | Chi phí thay đổi tùy loại |
| Sao lưu và khôi phục linh hoạt | Sao lưu nghiêm ngặt và không thể khôi phục |

- Xoay vòng thông tin xác thực (Credential Rotation) với AWS Secrets Manager:
    + Credential Updater sử dụng các hàm của Secrets Manager theo chu kỳ: Tạo Secret, Thiết lập Secret (ví dụ: mỗi 7 ngày), Kiểm tra Secret, và Hoàn tất Secret.
    + Các sự kiện xoay vòng có thể được gửi đến EventBridge Schedule để kiểm soát thời gian.
    + Cuối cùng là loại bỏ Secret cũ.

### Phát hiện và Giám sát liên tục
- Khả năng hiển thị bảo mật đa lớp:
    + Management Events:** Các lệnh gọi API và hành động trên console trên tất cả các tài khoản của tổ chức.
    + Data Events:** Truy cập đối tượng S3 và thực thi Lambda ở quy mô lớn.
    + Network Activity Events:** Tích hợp VPC Flow Logs để giám sát cấp độ mạng.
    + Organization Coverage:** Ghi log thống nhất trên tất cả các tài khoản thành viên và các region.

- Cảnh báo & Tự động hóa với EventBridge

    + Sự kiện thời gian thực: Các sự kiện CloudTrail chuyển đến EventBridge để xử lý ngay lập tức. Đây là nền tảng của Kiến trúc hướng sự kiện (EDA), cho phép hệ thống phản ứng với các thay đổi khi chúng xảy ra.

    + Cảnh báo tự động: Phát hiện các hoạt động đáng ngờ trên tất cả các tài khoản của tổ chức.

    + Định tuyến sự kiện chéo tài khoản: Xử lý sự kiện tập trung và phản hồi tự động. EventBridge làm cho việc này trở nên liền mạch, định tuyến sự kiện dựa trên các quy tắc đến các đích trên các tài khoản hoặc region khác nhau.

    + Tích hợp & Quy trình làm việc: Tích hợp Lambda, SNS, SQS cho các quy trình bảo mật tự động.

- Phát hiện dưới dạng mã (Detection-as-Code):
    
    + CloudTrail Lake Queries: Tạo và sử dụng các quy tắc phát hiện dựa trên SQL để săn tìm mối đe dọa nâng cao.

    + Logic được kiểm soát phiên bản: Các quy tắc và logic phát hiện được theo dõi và quản lý thông qua kho lưu trữ mã (code repositories).

    + Triển khai tự động: Các trails và quy tắc phát hiện được triển khai tự động trên tất cả các tài khoản liên quan của tổ chức, đảm bảo phạm vi bảo mật đồng nhất.

    + Cơ sở hạ tầng dưới dạng mã (IaC): Sử dụng các công cụ IaC để thiết lập và cấu hình tự động việc ghi log và event trails của tổ chức.
### Guard Duty
- GuardDuty là giải pháp Phát hiện Mối đe dọa Thông minh, Luôn bật (Always-On).

- Cách GuardDuty hoạt động – Dựa vào phân tích liên tục **Ba Trụ cột Phát hiện**:

| Nguồn dữ liệu | Những gì nó giám sát | Ví dụ thực tế |
| :--- | :--- | :--- |
| **CloudTrail Events** | Hành động IAM, thay đổi quyền, gọi API | Kẻ tấn công tắt logging để xóa dấu vết. |
| **VPC Flow Logs** | Lưu lượng mạng đến/đi từ tài nguyên của bạn | EC2 gửi dữ liệu đến máy chủ điều khiển botnet (C2). |
| **DNS Logs** | Các truy vấn DNS từ hạ tầng của bạn | Các truy vấn nhiễm mã độc đến các trang đào tiền ảo. |

- Các gói bảo vệ nâng cao: GuardDuty cung cấp các tiện ích phát hiện chuyên biệt để bảo vệ toàn diện:

    + S3 Protection: Phát hiện các mẫu truy cập S3 bất thường và quét mã độc trong các đối tượng S3 tại thời điểm tải lên.

    + EKS Protection: Giám sát nhật ký kiểm toán Kubernetes để phát hiện truy cập trái phép và liên kết các phát hiện với S3 để lập bản đồ đường đi tấn công đầy đủ.

    + Malware Protection: Tự động quét các volume EBS của các instance EC2 khi nghi ngờ bị xâm nhập.

    + RDS Protection: Phân tích nhật ký hoạt động đăng nhập vào cơ sở dữ liệu (Aurora/RDS) và phát hiện các cuộc tấn công brute-force (nhiều lần đăng nhập thất bại từ một IP duy nhất).

    + Lambda Protection: Giám sát nhật ký mạng từ các lệnh gọi hàm Lambda và phát hiện nếu một hàm bị xâm nhập gửi dữ liệu đến các IP độc hại.

    + Runtime Monitoring – Sâu bên trong hệ điều hành: Đạt được bằng cách sử dụng GuardDuty Agent cài đặt trên EC2/EKS/ECS Fargate. Nó giám sát các tiến trình đang chạy, mẫu truy cập tệp, lệnh gọi hệ thống và các nỗ lực leo thang đặc quyền hoặc reverse shells.

- Các tiêu chuẩn tuân thủ:

    + AWS Foundational Security Best Practices: Được phát triển bởi AWS và bao gồm một loạt các dịch vụ AWS.

    + CIS AWS Foundations Benchmark: Được phát triển bởi AWS và các chuyên gia trong ngành, tập trung vào Danh tính (IAM), Ghi log & Giám sát, và Mạng.

- Thực thi tuân thủ với Detection-as-Code

    + Công cụ IaC: AWS CloudFormation được sử dụng để triển khai các cấu hình.

    + Công cụ tuân thủ: AWS CloudFormation đẩy các kiểm tra cấu hình lên AWS Security Hub CSPM.

    + Áp dụng Tiêu chuẩn tuân thủ: Security Hub thực hiện kiểm tra dựa trên các tiêu chuẩn đã liệt kê (AWS Foundational Security Best Practices, CIS AWS Foundations Benchmark, PCI DSS, NIST).

    + Tài nguyên bao gồm: Amazon S3, Amazon EC2 và Amazon RDS.

### Kiểm soát An ninh Mạng

- Các véc-tơ tấn công: Các mối đe dọa được phân loại thành Tấn công đầu vào - Ingress (DDoS, SQL injection), Tấn công đầu ra - Egress (trích xuất dữ liệu, DNS tunneling), và Tấn công nội bộ - Inside (di chuyển ngang).

- Security Groups (SG): Hoạt động như một tường lửa có trạng thái (Stateful) ở cấp độ instance/giao diện mạng. Chúng chỉ hỗ trợ quy tắc cho phép (allow rules) và mặc định từ chối tất cả (implicit deny all).

- Network ACLs (NACLs): Hoạt động ở cấp độ subnet. Chúng là phi trạng thái (stateless) và sử dụng các quy tắc được đánh số để CHO PHÉP (ALLOW) hoặc TỪ CHỐI (DENY) lưu lượng truy cập một cách rõ ràng.

- AWS TGW Security Group Referencing: Cho phép Transit Gateway (TGW) VPCs xác định các quy tắc Inbound chỉ sử dụng tham chiếu SG.

- Route 53 Resolver: Định tuyến các truy vấn DNS đến Private DNS (private hosted zones), VPC DNS hoặc Public DNS.

- AWS Network Firewall:

    + Trường hợp sử dụng: Lọc đầu ra (chặn tên miền xấu, giao thức độc hại), Phân đoạn môi trường (VPC tới VPC), và Ngăn chặn xâm nhập (quy tắc IDS/IPS).

    + Phòng thủ chủ động: Có thể tự động chặn lưu lượng độc hại bằng cách sử dụng Amazon Threat Intelligence, nơi các phát hiện của GuardDuty được đánh dấu để chặn tự động.

### Quản trị & Bảo vệ Dữ liệu

- Mã hóa (KMS): Dữ liệu được mã hóa bằng Data Key, được bảo vệ bởi Master Key (CMK). Các chính sách KMS thực thi lớp bảo mật thứ hai với các Condition keys để xác định KHI NÀO việc mã hóa/giải mã được cho phép.

- Quản lý Chứng chỉ (ACM): Cung cấp chứng chỉ công khai miễn phí và tự động gia hạn chứng chỉ 60 ngày trước khi hết hạn. Xác thực DNS là phương pháp xác thực được khuyến nghị.

- Secrets Manager: Giải quyết vấn đề thông tin xác thực bị hardcode. Nó sử dụng logic Lambda 4 bước (createSecret, setSecret, testSecret, finishSecret) để tự động xoay vòng thông tin xác thực mà không gây gián đoạn (downtime).

- Bảo mật Dịch vụ API (S3 & DynamoDB): S3 yêu cầu TLS 1.2+ và bucket policies với aws:SecureTransport để thực thi. DynamoDB được bảo mật mặc định với HTTPS bắt buộc.

- Bảo mật Dịch vụ Cơ sở dữ liệu (RDS): Yêu cầu sự tin cậy phía máy khách vào AWS Root CA Bundle để xác minh danh tính máy chủ, và thực thi phía máy chủ (ví dụ: rds.force_ssl=1 cho PostgreSQL).

### Ứng phó sự cố & Phòng ngừa

- Các phương pháp phòng ngừa tốt nhất: Các bước chính bao gồm sử dụng thông tin xác thực tạm thời, không bao giờ để lộ trực tiếp các S3 buckets, đặt các dịch vụ nhạy cảm sau các private subnets, quản lý mọi thứ thông qua Infrastructure as Code, và sử dụng quy trình thay đổi rủi ro cao với hai lớp kiểm soát (phê duyệt PR, triển khai pipeline).

- Quy trình Ứng phó sự cố: Một phương pháp tiếp cận có cấu trúc gồm 5 bước: Chuẩn bị, Phát hiện & Phân tích, Ngăn chặn (cô lập, thu hồi thông tin xác thực), Loại bỏ & Khôi phục, và Sau sự cố (bài học kinh nghiệm).

### Trải nghiệm sự kiện

- Sự kiện này cực kỳ hữu ích cho nhóm chúng tôi, phù hợp trực tiếp với dự án về Tự động Ứng phó Sự cố và Điều tra số (Forensics) của nhóm.

- Hỏi: Dự án của nhóm em là một công cụ Tự động Ứng phó Sự cố và Điều tra số với GuardDuty là trọng tâm chính của việc phản hồi sự cố, nhưng qua thử nghiệm, bọn em thấy rằng GuardDuty có thể mất tới 5 phút để tạo ra một finding (phát hiện) khi sự cố xảy ra. Em muốn hỏi có giải pháp nào để giảm độ trễ này không ạ?

- Đáp: Việc GuardDuty mất 5 phút để tạo ra các phát hiện là điều bạn phải chấp nhận, vì đó là cách GuardDuty được cấu hình để hoạt động: GuardDuty phải đi qua một lượng lớn bộ dữ liệu bảo mật để xác định mối đe dọa chính xác và sau đó tạo ra finding. Tuy nhiên, nếu bạn muốn giảm độ trễ, một trong những cách để giải quyết là tích hợp các dịch vụ bảo mật của bên thứ 3 như: Open Clarity (Miễn phí) cho các phát hiện gần như thời gian thực và bạn cũng có thể phát hiện các bất thường và hành vi người dùng lạ với CloudTrail.

- Ông Mendel Grabski rất nhiệt tình đề nghị hỗ trợ khi chúng tôi hỏi về dự án của mình sau sự kiện.

#### Một số hình ảnh sự kiện
![Group Picture With Speaker Mendel Grabski and Speaker Van Hoang Kha](/images/Events/Event6PicturewithSpeakers.jpg)
_Ảnh chụp nhóm cùng Diễn giả Mendel Grabski và Diễn giả Văn Hoàng Kha_