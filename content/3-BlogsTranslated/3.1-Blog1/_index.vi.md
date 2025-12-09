---
title: "Blog 1"
date: 2025-09-10
weight: 1
chapter: false
pre: " <b> 3.1. </b> "
---

# SQL to NoSQL: Hiện đại hóa lớp truy cập dữ liệu với Amazon DynamoDB

**AWS Database Blog**
**Bởi Ramana Mannava, Mahesh Kumar Vemula, và Akber Rizwan Shaik**
*03 JUL 2025*
*Chuyên mục: Advanced (300), Amazon DynamoDB, Migration, Technical How-to*

---

Trong Phần 1 của loạt bài, chúng tôi đã khám phá cách di chuyển hiệu quả từ SQL sang Amazon DynamoDB. Sau khi thiết lập các chiến lược mô hình hóa dữ liệu được thảo luận trong Phần 2, giờ đây chúng tôi xem xét những cân nhắc chính để phân tích và thiết kế bộ lọc, phân trang, các trường hợp biên (edge cases) và các phép tổng hợp, xây dựng trên các mô hình dữ liệu đã thiết kế nhằm tạo ra một lớp truy cập dữ liệu hiệu quả.

Thành phần này kết nối ứng dụng của bạn với các tính năng và khả năng của DynamoDB. Việc chuyển đổi từ các mẫu truy cập dựa trên SQL sang cách tiếp cận điều khiển bằng API của DynamoDB mở ra cơ hội tối ưu hóa cách ứng dụng tương tác với lớp dữ liệu của nó.

Phần cuối cùng của loạt bài này tập trung vào việc triển khai một lớp trừu tượng hiệu quả và xử lý các mẫu truy cập dữ liệu khác nhau trong DynamoDB.

## Thiết kế lại mô hình thực thể

Mô hình thực thể, đại diện cho cấu trúc dữ liệu trong ứng dụng của bạn, sẽ cần được thiết kế lại để phù hợp với mô hình dữ liệu của DynamoDB. Điều này có thể bao gồm việc phi chuẩn hóa (de-normalizing) các mô hình và tái cấu trúc các mối quan hệ giữa các thực thể.

Bên cạnh đó, hãy cân nhắc công sức liên quan tới các cấu hình sau:

* **Chú thích thuộc tính DynamoDB:** Gắn chú thích cho các thuộc tính thực thể với các thuộc tính đặc thù của DynamoDB, bao gồm partition key, sort key, thông tin local secondary index (LSI) và thông tin global secondary index (GSI). Ví dụ, khi sử dụng mô hình persistence đối tượng .NET, bạn cần ánh xạ các lớp và thuộc tính với các bảng và thuộc tính DynamoDB.
* **Cấu hình tiền tố khóa:** Trong thiết kế một bảng đơn (single table design), bạn có thể phải cấu hình tiền tố cho partition key và sort key trong các mô hình thực thể. Phân tích cách những tiền tố này sẽ được sử dụng để truy vấn trong lớp truy cập dữ liệu của bạn.

Đoạn code sau là ví dụ minh họa cho việc cấu hình tiền tố khóa trong các mô hình thực thể:

```csharp
public class Post
{
    private const string PREFIX = "POST#";
    public string Id { get; private set; }
    public string Content { get; private set; }
    public string AuthorId { get; private set; }

    public Post(string id, string content, string authorId)
    {
        Id = id;
        Content = content;
        AuthorId = authorId;
    }
  
    // Property that automatically adds prefix
    public string PartitionKey => $"{PREFIX}{Id}";
}

// Usage example
var post = new Post("123", "Hello World", "USER#456");
var queryKey = post.PartitionKey; // Gets "POST#123"
```

**Thiết kế lại quy tắc ánh xạ:** Do thay đổi trong mô hình thực thể, các quy tắc ánh xạ hiện có giữa view models của ứng dụng và các mô hình thực thể có thể cần được thiết kế lại.

## Thiết kế lớp trừu tượng API DynamoDB

Lớp trừu tượng API DynamoDB đóng gói các thao tác DynamoDB bên dưới đồng thời cung cấp cho ứng dụng của bạn một giao diện sạch sẽ. Hãy cùng khám phá các thành phần bạn có thể cần triển khai trong lớp này.

### Xử lý lỗi và cơ chế thử lại

Các kịch bản lưu lượng cao thường dẫn tới các lỗi tạm thời cần xử lý. Ví dụ, khi nội dung lan truyền mạnh hoặc một bài đăng của người nổi tiếng thu hút sự chú ý đột ngột, bạn có thể gặp ngoại lệ vượt quá throughput. Bạn có thể cần triển khai:

* Cơ chế thử lại tự động với exponential backoff cho các lỗi tạm thời.
* Chuyển dịch ngoại lệ DynamoDB thành các lỗi có ý nghĩa cho ứng dụng.
* Ghi nhật ký lỗi nhất quán để phục vụ khắc phục sự cố.
* Xử lý thất bại kiểm tra điều kiện (conditional check failures) trong các cập nhật đồng thời.

### Quản lý thao tác hàng loạt (Batch operation management)

Ứng dụng thường cần xử lý nhiều mục một cách hiệu quả để cung cấp trải nghiệm người dùng tốt. Xem xét các kịch bản như tải một news feed cá nhân hóa kết hợp bài đăng từ nhiều người theo dõi. Bạn có thể cần triển khai:

* Tự động chia nhỏ các yêu cầu trong giới hạn của DynamoDB.
* Xử lý song song để tối ưu hiệu năng.
* Cơ chế khôi phục cho các thất bại một phần trong batch.
* Theo dõi tiến độ cho các thao tác chạy dài.
### Tải dữ liệu liên quan của thực thể (Loading related entity data)

Khi di chuyển từ cơ sở dữ liệu quan hệ sang DynamoDB, có một nhận thức phổ biến rằng dữ liệu quan hệ thường được phi chuẩn hóa và việc truy cập dữ liệu liên quan trở nên đơn giản. Tuy nhiên, điều này không phải lúc nào cũng đúng. Mặc dù trong một số trường hợp các quan hệ có thể được mô hình hóa bằng chiến lược single-item modeling, tùy theo chi phí và cân nhắc hiệu năng, các quan hệ có thể được mô hình hóa bằng các chiến lược khác như vertical partitioning hoặc composite sort keys.

Khi thích nghi với DynamoDB, bạn có thể phải phát triển các phương thức trợ giúp trong lớp trừu tượng của mình để tải dữ liệu quan hệ của một thực thể (navigation properties) một cách hiệu quả. Các phương thức này cần xem xét kiến trúc ứng dụng, mẫu truy cập và chiến lược mô hình hóa dữ liệu.

Ví dụ, trong ứng dụng mạng xã hội của chúng tôi, việc tải các comment cho một bài đăng có thể yêu cầu các phương pháp khác nhau tùy thuộc vào chiến lược mô hình hóa được chọn – từ việc lấy thuộc tính đơn giản trong single-item models đến các thao tác truy vấn trong vertical partitioning.

* Đối với các thực thể liên quan sử dụng chiến lược single-item, có thể không cần logic tải cụ thể vì tất cả dữ liệu được truy xuất trong một thao tác API duy nhất.
* Tuy nhiên, đối với các chiến lược mô hình khác như vertical partitioning, các phương thức trong lớp trừu tượng của bạn cần xử lý truy vấn hiệu quả dựa trên điều kiện lọc và phân trang. Ví dụ, khi comments được lưu như các item riêng biệt chia sẻ partition key của bài đăng, phương thức phải truy vấn và phân trang các item liên quan một cách hiệu quả.
* Xây dựng dựa trên khả năng vận hành batch, bạn có thể mở rộng các phương thức này để xử lý tải dữ liệu liên quan cho nhiều mục. Ví dụ, khi tải comments cho nhiều bài đăng, sử dụng BatchGetItem để thực hiện các việc sau:
    * Sử dụng cơ chế batching đã thiết lập để nhóm các yêu cầu.
    * Áp dụng retry và chiến lược xử lý lỗi.
    * Cung cấp giao diện nhất quán cho cả thao tác đơn lẻ và thao tác hàng loạt.

Khi sử dụng GSI, bạn có thể cần truy xuất các thuộc tính bổ sung không được bao gồm trong projection của GSI. Thiết kế các chiến lược để tải hiệu quả dữ liệu cần thiết trong khi tối thiểu hóa các cuộc gọi API và tối ưu hóa hiệu năng và chi phí. Phương thức trong lớp trừu tượng của bạn có thể cần cung cấp:

* Giao diện nhất quán để tải dữ liệu liên quan.
* Tối ưu hóa các cuộc gọi API và chi phí.
* Đơn giản hóa bảo trì thông qua triển khai tập trung.

Đoạn code sau là ví dụ minh họa cho việc tải các navigation properties:

```csharp
// Entity with navigation property
public class Post
{
    public string Id { get; set; }
    public string Content { get; set; }
    public IEnumerable<Comment> Comments { get; set; }
}

// Interface for loading related data
public interface INavigationPropertyManager
{
    Task<IEnumerable<T>> LoadRelatedItemsAsync<T>(string parentId);
    Task<IDictionary<string, IEnumerable<T>>> LoadRelatedItemsInBatchAsync<T>(IEnumerable<string> parentIds);
}

// Service using the loader
public class PostService
{
    private readonly INavigationPropertyManager _navigationPropertyManager;
  
    public PostService(INavigationPropertyManager navigationPropertyManager)
    {
        _navigationPropertyManager = navigationPropertyManager;
    }

    public async Task<IEnumerable<Comment>> GetPostCommentsAsync(string postId)
    {
        return await _navigationPropertyManager.LoadRelatedItemsAsync<Comment>(postId);
    }
}
```

Khi thiết kế các phương thức này, hãy phân tích các mẫu tải hiện tại của ứng dụng và đánh giá liệu việc duy trì các mẫu tương tự trong DynamoDB có thể mang lại lợi ích cho hiệu năng và trải nghiệm người dùng hay không.

### Ánh xạ phản hồi (Response mapping)

Khi ứng dụng phát triển, cấu trúc dữ liệu và yêu cầu thay đổi theo thời gian. Ví dụ, khi thêm các tính năng mới như phản ứng (reactions) cho bài đăng ngoài lượt thích đơn giản, hoặc giới thiệu nội dung đa phương tiện phong phú trong hồ sơ người dùng, khả năng tương thích ngược (backward compatibility) trở nên quan trọng. Bạn có thể cần triển khai logic ánh xạ để thực hiện các chức năng sau:

* Chuyển các item DynamoDB thành các domain object.
* Xử lý tương thích ngược khi mô hình dữ liệu tiến hóa.
* Quản lý giá trị mặc định cho các thuộc tính thiếu.
* Hỗ trợ các phiên bản khác nhau của cùng một thực thể.

### Xây dựng biểu thức filter (Filter expression building)

Các nhu cầu truy xuất dữ liệu phức tạp thường xuất hiện trong các ứng dụng hiện đại. Ví dụ, khi người dùng muốn tìm bài đăng trong khung thời gian cụ thể có mức tương tác cao, hoặc khi lọc comment dựa trên các mẫu tương tác người dùng. Lớp trừu tượng của bạn có thể cần:

* Chuyển đổi tiêu chí tìm kiếm phức tạp thành các biểu thức filter DynamoDB.
* Xử lý nhiều điều kiện filter một cách động.
* Quản lý expression attribute names và values.
* Hỗ trợ lọc thuộc tính lồng nhau.

### Triển khai phân trang (Pagination implementation)

Việc điều hướng dữ liệu hiệu quả quan trọng đối với trải nghiệm người dùng. Xem xét các kịch bản như người dùng cuộn qua news feed vô hạn, hoặc người kiểm duyệt duyệt các comment trên các bài viral. Bạn có thể cần triển khai:

* Phân trang dựa trên token sử dụng `LastEvaluatedKey`.
* Cấu hình kích thước trang (page size) có thể tùy chỉnh.
* Xử lý hiệu quả các tập kết quả lớn.
* Hành vi phân trang nhất quán trên các truy vấn khác nhau.

Đoạn code sau là ví dụ minh họa cho việc phân trang:

```csharp
// Enhanced interface adding pagination support
public interface INavigationPropertyManager
{
    Task<IEnumerable<T>> LoadRelatedItemsAsync<T>(string parentId);
    Task<IDictionary<string, IEnumerable<T>>> LoadRelatedItemsInBatchAsync<T>(IEnumerable<string> parentIds);
    // method for paginated loading
    Task<PagedResult<T>> LoadRelatedItemsPagedAsync<T>(string parentId, PaginationOptions options);
}

public class PaginationOptions
{
    public int PageSize { get; set; } = 20;
    public string ExclusiveStartKey { get; set; }
}

public class PagedResult<T>
{
    public IEnumerable<T> Items { get; set; }
    public string LastEvaluatedKey { get; set; }
}

// With pagination support
public class PostService
{
    private readonly INavigationPropertyManager _navigationPropertyManager;

    public PostService(INavigationPropertyManager navigationPropertyManager)
    {
        _navigationPropertyManager = navigationPropertyManager;
    }

    public async Task<PagedResult<Comment>> GetPostCommentsPagedAsync(string postId, int pageSize = 20, string nextToken = null)
    {
        var options = new PaginationOptions
        {
            PageSize = pageSize,
            ExclusiveStartKey = nextToken
        };
        return await _navigationPropertyManager.LoadRelatedItemsPagedAsync<Comment>(postId, options);
    }
}
```

### Mã hóa dữ liệu (Data encryption)

Bảo vệ dữ liệu nhạy cảm của người dùng là điều tối quan trọng trong các ứng dụng hiện đại. Bạn có thể cần triển khai:

* Mã hóa phía client sử dụng AWS Database Encryption SDK bên cạnh mã hóa phía server do DynamoDB cung cấp.
* Mã hóa chọn lọc các thuộc tính.
* Xử lý lỗi cho các thao tác mã hóa.

### Observability (Quan sát/Giám sát)

Giám sát sức khỏe ứng dụng và hiệu năng là điều cần thiết. Hãy xem xét giám sát các chỉ số Amazon CloudWatch sau:

* **Theo dõi độ trễ request:** Giám sát các chỉ số DynamoDB như `SuccessfulRequestLatency`, và tạo các metric tùy chỉnh cho `TransactionConflict` và `ConditionalCheckFailedRequests`.
* **Tiêu thụ capacity:** Theo dõi `ConsumedReadCapacityUnits` và `ConsumedWriteCapacityUnits`.
* **Tỷ lệ lỗi và các mẫu lỗi:** Giám sát `ConditionalCheckFailedRequests`, `SystemErrors`, `UserErrors`.
* **Hiệu năng truy vấn:** Theo dõi `ThrottledRequests`, `ScannedCount` hoặc `Count`, thời gian lọc phía client, và độ trễ cuộc gọi dịch vụ bên ngoài.

### Quản lý giao dịch (Transaction management)

Duy trì tính nhất quán dữ liệu là điều quan trọng trong nhiều kịch bản. Bạn có thể cần:

* Xử lý các thao tác giao dịch.
* Quản lý timeout và xung đột.
* Logic bù trừ (compensation) cho các giao dịch thất bại.

---

## Xử lý bộ lọc (Handling filters)

Sau khi bạn thiết kế lớp trừu tượng API DynamoDB với các thao tác cơ bản và khả năng tải dữ liệu, hãy phân tích cách thích nghi các mẫu truy vấn hiện có để phù hợp với cách truy vấn của DynamoDB.

Trong khi các cơ sở dữ liệu quan hệ sử dụng trình tối ưu hóa truy vấn cho các điều kiện WHERE, DynamoDB trao quyền cho nhà phát triển kiểm soát chính xác luồng thực thi truy vấn. DynamoDB xử lý truy vấn theo hai bước:

1.  Đầu tiên, nó truy xuất các item khớp với key condition expression dựa trên partition và sort keys.
2.  Sau đó, trước khi trả kết quả, nó áp dụng filter expressions lên các thuộc tính không phải khóa.

Mặc dù filter expressions không giảm tiêu thụ RCU vì toàn bộ tập kết quả vẫn được đọc trước khi lọc, chúng giảm chi phí truyền tải dữ liệu và cải thiện hiệu năng ứng dụng bằng cách lọc dữ liệu ở cấp độ dịch vụ DynamoDB.

### Xử lý các yêu cầu lọc phức tạp (Handling complex filter requirements)

Khả năng biểu thức linh hoạt của DynamoDB xử lý nhiều kịch bản lọc trực tiếp, và bạn có thể triển khai lọc phía client cho bất kỳ yêu cầu bổ sung nào. Một vài ví dụ bao gồm:

* **Các hàm hoặc phương thức không được hỗ trợ:** Khi làm việc với các bộ lọc tham chiếu đến các hàm hệ thống (như `SUBSTRING`, `CONCAT`, `DATEADD`, `DATEDIFF`), hãy truy xuất dữ liệu từ DynamoDB và áp dụng các bộ lọc chuyên biệt này ở lớp ứng dụng.
* **Tải dữ liệu thực thể liên quan:** Đối với các truy vấn lọc dựa trên thuộc tính của các thực thể liên quan, ứng dụng có thể cần tải dữ liệu từ nhiều bảng DynamoDB hoặc các bộ sưu tập item và áp dụng lọc tại lớp ứng dụng.
* **Tích hợp với nguồn dữ liệu bên ngoài:** Trong kiến trúc microservice, lọc có thể yêu cầu dữ liệu từ các dịch vụ hoặc cơ sở dữ liệu khác.

Hãy xem xét trường hợp sử dụng truy xuất comment bài đăng theo tác giả đang hoạt động (active) và điểm sentiment, yêu cầu dữ liệu từ dịch vụ người dùng ngoài và cơ sở dữ liệu phân tích:

**Original SQL Query demonstrating filters across different data sources:**

```sql
SELECT c.*, u.name, u.profile_pic, u.status, m.sentiment_score
FROM comments c
JOIN users u ON c.user_id = u.id
JOIN comment_analytics m ON c.id = m.comment_id
WHERE c.post_id = '123'
AND c.created_at > DATEADD(year, -1, GETUTCDATE())
AND u.status = 'ACTIVE'
AND m.sentiment_score > 0.8
```

**Mã C# minh họa:**

```csharp
public class PostCommentService
{
    // ... Initialize readonly fields ...

    public async Task<IEnumerable<Comment>> GetPostCommentsAsync(
        string postId,
        DateTime startDate,
        double minSentimentScore)
    {
        // Step 1: Query DynamoDB for comments
        var comments = await _dynamoDbContext.QueryAsync<Comment>(postId,
            QueryOperator.GreaterThanOrEqual,
            new [] { startDate.ToString("yyyy-MM-dd") }).GetRemainingAsync();
          
        // Step 2: Get user details and filter by active status
        var userIds = comments.Select(c => c.UserId).Distinct();
        var userDetails = await _userService.GetUserDetailsAsync(userIds);
        comments = comments.Where(c => userDetails[c.UserId].Status == "ACTIVE");

        // Step 3: Apply sentiment score filter from analytics
        var commentIds = comments.Select(c => c.CommentId);
        var sentimentScores = await _analyticsDb.GetSentimentScoresAsync(commentIds);
      
        return comments.Where(c => sentimentScores[c.CommentId] > minSentimentScore);
    }
}
```

Khi phân tích các truy vấn hiện có, hãy xác định các kịch bản yêu cầu lọc phía client và đánh giá tác động hiệu năng của chúng.
---

## Xử lý phân trang (Handling pagination)

Đánh giá chiến lược phân trang hiện tại của ứng dụng và điều chỉnh cho phù hợp với khả năng của DynamoDB. Trong khi các ứng dụng cơ sở dữ liệu quan hệ thường hiển thị tổng số trang cho người dùng, DynamoDB được tối ưu cho phân trang theo khóa và tiến tới trước (forward-only), sử dụng `LastEvaluatedKey`.

* Vì việc triển khai các tính năng như tổng số bản ghi cần duyệt toàn bộ bảng (full table scans), hãy cân nhắc các giải pháp thay thế như điều hướng theo con trỏ (cursor-based) hoặc các mẫu “load more".
* Đối với các ứng dụng cần ngữ cảnh kích thước tập kết quả, hãy cân nhắc triển khai các bộ đếm (counters) thay vì tính tổng thời gian thực.

Khi thiết kế phân trang trong lớp truy cập dữ liệu cho DynamoDB, hiểu hành vi phân trang cốt lõi của nó. DynamoDB có thể không trả tất cả các item khớp trong một cuộc gọi API do hai ràng buộc chính: tham số "Limit" và kích thước đọc tối đa 1 MB.

* **Phân tích tác động của lọc:** Đánh giá các bộ lọc truy vấn và tính phân phối (cardinality) của dữ liệu.
* **Tối ưu hóa tham số Limit:** Hướng tới giá trị limit phù hợp gần với kích thước trang mong muốn trong khi tính đến tác động của bộ lọc.
* **Giám sát hiệu năng:** Theo dõi số cuộc gọi API trên mỗi yêu cầu trang và thời gian phản hồi trung bình.

---

## Xử lý các trường hợp biên (Handling edge cases)

Khi di chuyển lớp truy cập dữ liệu sang DynamoDB, hãy xác định và giải quyết các trường hợp biên liên quan tới các thao tác dữ liệu ở quy mô lớn:

* **Các thao tác khối lượng lớn có thể dự đoán được:** Xem xét kịch bản một người dùng có hàng triệu người theo dõi đăng nội dung. Các mẫu thiết kế như write sharding hoặc batch processing có thể giúp quản lý những kịch bản này.
* **Các sự kiện tăng đột biến không mong đợi:** Ví dụ, khi một bài đăng bất ngờ nhận được lượng tương tác lớn. Những kịch bản này đòi hỏi các chiến lược như scaling động, caching và mô hình bất đồng bộ.

---

## Xử lý các phép tổng hợp và dữ liệu phi chuẩn hóa (Handling aggregations and de-normalized data)

### Quản lý các phép tổng hợp (Managing aggregations)

Các cơ sở dữ liệu thường dùng JOIN và GROUP BY cho các phép tổng hợp thời gian thực. Các mẫu truy cập của DynamoDB hỗ trợ các cách tiếp cận khác như duy trì các thực thể aggregation để lưu các giá trị được tiền tính toán.

### Xử lý dữ liệu phi chuẩn hóa (Handling de-normalized data)

DynamoDB thường yêu cầu phi chuẩn hóa dữ liệu. Ví dụ, chúng tôi lưu trạng thái người dùng trực tiếp trên các thực thể bài đăng để cho phép lọc hiệu quả. Cách tiếp cận này đánh đổi tăng số thao tác ghi để cải thiện hiệu năng đọc.

### Quản lý cập nhật (Managing updates)

* **Cập nhật đồng bộ (Synchronous updates):** Cho các tính năng quan trọng cần tính nhất quán ngay lập tức (ví dụ: dùng giao dịch).
* **Cập nhật bất đồng bộ (Asynchronous updates):** Sử dụng Amazon DynamoDB Streams và AWS Lambda cho các cập nhật không cần tính nhất quán ngay lập tức.

### Xử lý phân tích (Analytical processing)

Đối với các truy vấn phân tích phức tạp, hãy cân nhắc các dịch vụ bổ trợ: Amazon Redshift, Zero-ETL integration, Amazon Athena, hoặc Amazon SageMaker Lakehouse.

---

## Kết luận

Trong bài viết này, chúng tôi đã khám phá các chiến lược để hiện đại hóa lớp truy cập dữ liệu của ứng dụng cho DynamoDB. Việc chuyển đổi từ các mẫu dựa trên SQL sang cách tiếp cận điều khiển bằng API của DynamoDB đem lại cơ hội tối ưu hóa cách ứng dụng tương tác với dữ liệu của nó. Sự hợp tác chặt chẽ giữa các nhóm cơ sở dữ liệu và ứng dụng giúp tạo ra các giải pháp cân bằng giữa hiệu năng, tối ưu chi phí và khả năng mở rộng.

### Về các tác giả

* **Ramana Kiran Mannava:** Chuyên gia Tư vấn Cấp cao tại AWS Professional Services, chuyên sâu về .NET và AWS.
* **Akber Rizwan Shaik:** Chuyên gia Tư vấn Cấp cao tại AWS Professional Services.
* **Mahesh Kumar Vemula:** Chuyên gia Tư vấn Cấp cao tại AWS Professional Services, đam mê Serverless.