---
title: "Blog 3"
date: 2025-06-04
weight: 1
chapter: false
pre: " <b> 3.3. </b> "
---

# CÁCH DERIVE MỞ RỘNG NỀN TẢNG GIAO DỊCH PHI TẬP TRUNG ĐỘ TRỄ THẤP BẰNG AWS GRAVITON, AMAZON EKS VÀ AMAZON AURORA

**Tác giả:** Daniel Wirjo, Christoph Niemann, Dillon Lin, và Joshua Kim
**Ngày:** 04/06/2025
**Chuyên mục:** Amazon Aurora, Amazon Elastic Kubernetes Service, Blockchain, Customer Solutions, Graviton, Intermediate (200)

Đây là bài viết cộng tác của Joshua Kim, Trưởng nhóm Kỹ thuật tại Derive, và Dillon Lin, Trưởng nhóm Phát triển tại Derive, phối hợp cùng AWS.

Thị trường phái sinh được dự báo sẽ tăng trưởng mạnh mẽ trong thập kỷ tới, được thúc đẩy bởi sự gia tăng tham gia của các tổ chức, đổi mới công nghệ và xu hướng chuyển dịch sang mô hình on-chain, tokenization và tài chính phi tập trung (DeFi). Khi thị trường toàn cầu đối mặt với nhiều biến động, phái sinh đang trở thành công cụ thiết yếu để quản lý rủi ro và tận dụng cơ hội. Sự hội tụ giữa các công cụ tài chính truyền thống và công nghệ blockchain này được kỳ vọng sẽ định hình lại toàn cảnh thị trường phái sinh, mang đến những cơ hội tăng trưởng và đổi mới mới trong ngành.

Trong bài viết này, chúng tôi chia sẻ cách Derive đã mở rộng thành công nền tảng giao dịch phi tập trung lai (hybrid decentralized trading platform) của họ - đạt được hàng tỷ đô la khối lượng giao dịch và độ trễ cực thấp, bằng cách sử dụng cơ sở hạ tầng tính toán và cơ sở dữ liệu mạnh mẽ, kết hợp AWS Graviton trên Amazon Elastic Kubernetes Service (Amazon EKS) và Amazon Aurora. Chúng tôi cũng khám phá mô hình sàn giao dịch lai của Derive và vai trò quan trọng mà AWS đã đóng góp trong quá trình tăng trưởng và mở rộng quy mô của họ.

## Tổng quan: Mô hình sàn giao dịch lai độc đáo của Derive

Derive là một giao thức DeFi tạo ra các sản phẩm phái sinh on-chain có thể lập trình và tùy chỉnh, bao gồm options (quyền chọn), perpetuals (hợp đồng vĩnh viễn) và các sản phẩm cấu trúc khác.

Nền tảng này vận hành theo mô hình lai (hybrid model) – kết hợp hiệu quả của việc khớp lệnh tập trung với tính bảo mật và minh bạch của việc thanh toán phi tập trung và quản lý ký quỹ trên Derive chain, được xây dựng trên OP Stack, một blockchain Ethereum Layer 2 mã nguồn mở. Cách tiếp cận này cho phép Derive mang đến trải nghiệm giao dịch liền mạch tương tự như các sàn tập trung (CEX), đồng thời vẫn đảm bảo người dùng kiểm soát tài sản của mình.

Điều này được hỗ trợ bởi hệ thống ký quỹ dựa trên đấu giá mở, giúp tăng tính minh bạch và giảm rủi ro thường thấy trong các hệ thống tập trung truyền thống nơi tài sản dự trữ do một bên trung tâm quản lý.

Mặc dù Derive cung cấp các sản phẩm giao dịch tiêu chuẩn như perpetuals và spot trading, nhưng trọng tâm cốt lõi của họ là phục vụ các nhà giao dịch chuyên nghiệp và tổ chức. Giải pháp của Derive cung cấp thanh khoản on-chain cho các quyền chọn phi tập trung (decentralized options), thông qua order book và hệ thống Request-for-Quote (RFQ) mạnh mẽ - cho phép thực hiện các chiến lược giao dịch nâng cao và tối ưu hóa việc khám phá giá (price discovery) trong thị trường phi tập trung.

Với sự tăng trưởng nhanh chóng của cơ sở người dùng và khối lượng giao dịch, Derive cần đảm bảo rằng hạ tầng của họ có thể xử lý nhu cầu ngày càng tăng mà không ảnh hưởng đến hiệu suất, ngay cả khi đội ngũ kỹ thuật tinh gọn và trong những giai đoạn biến động thị trường cao.

## Tổng quan giải pháp

Sơ đồ sau minh họa kiến trúc tổng thể cho nền tảng có hiệu suất cao và độ trễ thấp của Derive.


Kiến trúc tổng thể bao gồm nhiều thành phần chính, được trình bày chi tiết bên dưới.

**Tính toán hiệu năng cao**

Kiến trúc của Derive bao gồm hệ thống tính toán hiệu năng cao (high-performance compute) chạy trên Graviton nodes, được triển khai theo kiến trúc microservices trong Amazon EKS. Điều này mang lại độ trễ thấp và khả năng mở rộng cao, giúp xử lý giao dịch nhanh chóng.

Các microservice được thiết kế theo mô-đun và có thể mở rộng ngang (horizontally scalable), giúp hệ thống xử lý khối lượng giao dịch lớn một cách hiệu quả, với các dịch vụ chuyên biệt cho những chức năng cốt lõi sau:
* **Core matching engine:** Được xây dựng bằng Rust để đạt độ trễ thấp; chịu trách nhiệm xử lý lệnh, khớp giao dịch và quản lý trạng thái.
* **Risk management:** Các microservice chuyên dụng đảm nhận tính toán rủi ro tiêu chuẩn và danh mục đầu tư, đảm bảo tuân thủ và bảo vệ nền tảng lẫn người dùng.
* **Emitters:** Các dịch vụ như Orderbook Emitter và Ticker Emitter phát sóng các thay đổi trạng thái và cập nhật giá đến hệ thống và người dùng bên ngoài.
* **Additional microservices:** Kiến trúc có thể mở rộng, hỗ trợ việc bổ sung các microservice mới khi cần cho sự phát triển trong tương lai.

**Cơ sở dữ liệu**

Các microservice giao dịch dữ liệu trên PostgreSQL trong Amazon Aurora, tận dụng khả năng mở rộng và độ tin cậy cao của hệ thống này.

> “Trong ngày ra mắt, chúng tôi có hơn 50.000 người dùng chỉ trong một ngày, thực hiện hơn 50 triệu yêu cầu API khi giao dịch. Amazon Aurora đã đóng vai trò then chốt trong việc giúp chúng tôi nhanh chóng mở rộng cơ sở dữ liệu để xử lý lượng yêu cầu đọc khổng lồ.” — Josh Kim, Trưởng nhóm Kỹ thuật tại Derive.

**Tổng hợp và thanh toán blockchain**

Mô hình sàn giao dịch lai của Derive yêu cầu một thành phần quản lý việc tổng hợp (aggregation rollup) và thanh toán (settlement) giao dịch, kết nối với các microservice để hoàn tất giao dịch.

Để thực hiện thanh toán, Derive xây dựng blockchain Layer 2 dựa trên Ethereum, dùng OP Stack mã nguồn mở làm giải pháp mở rộng quy mô. Cách tiếp cận này mang lại tốc độ xử lý cao, chi phí thấp và kế thừa bảo mật từ Ethereum, cân bằng giữa tốc độ và an toàn.

Kim giải thích: "Các sàn lai thêm một tầng phức tạp mới cho giao dịch độ trễ thấp, vì chúng yêu cầu tự quản lý tài sản (self-custody) thông qua chữ ký lệnh mật mã và xác thực rủi ro on-chain theo thời gian thực, ngay cả khi việc khớp lệnh diễn ra off-chain. Một ví dụ điển hình là nhà giao dịch tần suất cao bị thanh lý on-chain trong khi đang gửi hàng nghìn lệnh đến sàn Derive. Engine khớp lệnh cần có khả năng truy cập nhanh vào trạng thái giao thức on-chain và xử lý song song một số khối lượng công việc nhất định."

**Kiến trúc hướng sự kiện (Event-driven architecture)**

Các yêu cầu của người dùng được xử lý thông qua các endpoint WebSocket và REST API, đảm bảo bảo mật và hiệu quả khi quản lý lệnh và dữ liệu thị trường. Hệ thống hàng đợi dựa trên Valkey điều phối việc xếp hàng và xử lý lệnh đến, đồng thời cơ chế giới hạn tốc độ (rate limiter) đảm bảo công bằng và ngăn chặn lạm dụng.

Để phát dữ liệu thị trường theo thời gian thực và cập nhật lệnh với độ trễ tối thiểu, cơ chế publish/subscribe dựa trên Valkey giúp truyền tải sự kiện đến tất cả các client được kết nối một cách hiệu quả. Kiến trúc còn bao gồm event streaming để theo dõi và ghi lại thay đổi trạng thái phục vụ các microservice hạ tầng. Cách tiếp cận hướng sự kiện này sử dụng NATS, được triển khai trên Amazon EKS, giúp đảm bảo tính mở rộng và độ tin cậy cho toàn bộ nền tảng.

Kim cho biết: "Ngoài việc xây dựng engine bằng Rust hiệu năng cao, chúng tôi còn phát triển nhiều thành phần nội bộ đặc thù – một trong số đó là hệ thống hàng đợi tùy chỉnh để định tuyến lệnh trong phạm vi độ trễ cực thấp. Đội ngũ AWS đã hỗ trợ tuyệt vời qua nhiều phiên brainstorm kỹ thuật trực tiếp với các chuyên gia nội bộ, giúp cải thiện tốc độ thực thi đáng kể. Ngay sau khi ra mắt, sàn giao dịch đã xử lý khối lượng 3,7 tỷ đô la và giao dịch gần 1 triệu lệnh on-chain chỉ trong một tháng."

**Bảo mật**

Bên cạnh lớp bảo mật vốn có của việc thanh toán phi tập trung, Derive còn sử dụng các dịch vụ bảo mật của AWS như AWS Control Tower (Quản trị đám mây tập trung), AWS IAM Identity Center (Quản lý danh tính đơn giản hóa), AWS Key Management Service (AWS KMS – Mã hóa an toàn), Amazon GuardDuty (Phát hiện mối đe dọa thông minh). Nhờ đó, Derive có thể đáp ứng các yêu cầu bảo mật nghiêm ngặt và tiêu chuẩn cao mà các nhà đầu tư tổ chức kỳ vọng.

## Hợp tác với AWS

Derive đã hợp tác với AWS ngay từ khi khởi đầu, tham gia chương trình AWS Activate dành cho startup. Sau khi nhận đầu tư từ Coinbase Ventures và Framework Ventures (đều là nhà cung cấp AWS Activate), Derive đã có thể truy cập tín dụng AWS hỗ trợ cho phát triển sản phẩm.

Dominic Romanowski, Đồng sáng lập Derive, chia sẻ: “Đội ngũ AWS Startups đóng vai trò cực kỳ quan trọng trong hành trình của chúng tôi - mang lại nguồn tài trợ, công cụ và chuyên môn giúp chúng tôi đổi mới trong không gian DeFi. Bằng cách tận dụng sức mạnh của hạ tầng AWS, chúng tôi không chỉ tối ưu chi phí, mà còn đảm bảo nền tảng mở rộng liền mạch để đáp ứng nhu cầu ngày càng tăng, đồng thời giữ vững bảo mật. Điều đó giúp chúng tôi tập trung vào điều quan trọng nhất: xây dựng nền tảng giao dịch hiệu năng cao cho cả khách hàng tổ chức và bán lẻ.”

Derive cũng làm việc chặt chẽ với các chuyên gia chuyên môn của AWS trong nhiều lĩnh vực, bao gồm tính toán, cơ sở dữ liệu và Web3, để giải quyết các thách thức kỹ thuật độc đáo và tăng tốc phát triển. Romanowski nói thêm: "Thật yên tâm khi biết rằng chúng tôi có thể gọi và nhận tư vấn chuyên sâu bất cứ khi nào cần.".

## Lộ trình tiếp theo

Nhìn về phía trước, Derive cam kết liên tục nâng cao năng lực và giảm độ trễ. Trong lộ trình sắp tới, Derive tập trung vào hai sáng kiến chính:
1.  **Khả năng phát lại và kiểm toán toàn diện (replay & audit):** Cho phép người dùng phát lại chính xác các lệnh và giao dịch, phục vụ khách hàng tổ chức cần dữ liệu lịch sử chi tiết để debug thuật toán và đảm bảo công bằng.
2.  **Tích hợp sâu hơn với Ethereum Virtual Machine (EVM):** Biến Derive thành một phần mở rộng tự nhiên của node EVM.

Cách tiếp cận này giúp giảm sai lệch giữa số dư trên sàn và trạng thái on-chain, đơn giản hóa cấu trúc dữ liệu thị trường, tài khoản và giao dịch, và trong tương lai cho phép người dùng tích hợp liền mạch các thành phần của Derive với các giao thức khác.

Dillon Lin, Trưởng nhóm Phát triển tại Derive, cho biết: “Chúng tôi tin rằng những phát triển này sẽ đưa Derive trở thành người dẫn đầu trong giao dịch blockchain-native, đồng thời mở đường cho những đổi mới rộng hơn trong ngành.”.

## Kết luận

Bằng việc sử dụng các dịch vụ AWS, Derive có thể tập trung vào đổi mới và mở rộng danh mục sản phẩm trong tokenization và phái sinh phi tập trung. Sự kết hợp này giúp Derive mở rộng quy mô thành công, mang lại môi trường giao dịch an toàn và hiệu quả, đáp ứng nhu cầu ngày càng phát triển của các tổ chức tài chính.

Lin khẳng định: “Khi chúng tôi tiếp tục đổi mới trong lĩnh vực DeFi và đáp ứng nhu cầu ngày càng tăng về phái sinh on-chain, sự hợp tác với AWS vẫn là yếu tố then chốt. Sự hỗ trợ của họ đóng vai trò cực kỳ quan trọng trong hành trình của chúng tôi, giúp mở rộng hiệu quả và cung cấp giải pháp phù hợp với nhu cầu của các nhà đầu tư tổ chức. Chúng tôi mong muốn tiếp tục hợp tác với AWS để mở rộng nền tảng hơn nữa.”

**Tài nguyên tham khảo:**
* Tìm hiểu thêm về phái sinh phi tập trung tại Derive và Developer Hub của họ.
* Tìm hiểu thêm về Web3 trên AWS.
* Tìm hiểu thêm về AWS Startups tại startups.aws.

## Về tác giả

**Joshua Kim:** Trưởng bộ phận Kỹ thuật tại Derive, lãnh đạo phát triển hạ tầng phái sinh. Từng làm việc tại Apple và sở hữu nhiều bằng sáng chế.

**Dillon Lin:** Trưởng bộ phận Phát triển tại Derive, phụ trách chiến lược go-to-market và phân phối cho người dùng bán lẻ và tổ chức.

**Daniel Wirjo:** Kiến trúc sư Giải pháp tại AWS, hỗ trợ các startup và từng là CTO của một startup.

**Christoph Niemann:** Kiến trúc sư Blockchain Cao cấp tại AWS, đam mê công nghệ Blockchain.