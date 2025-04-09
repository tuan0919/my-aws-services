# Tại sao lại dùng AWS Lambda
AWS Lambda mang lại một số lợi thế nhất định khi so với cách sử dụng các EC2 instance truyền thống:
- EC2 Instance:
    - Là máy chủ ảo trong đám mây.
    - Bị giới hạn bởi RAM và CPU.
    - Phải liên tục chạy.
    - Scale đồng nghĩa là phải thêm hoặc bớt số lượng máy chủ.
- Lambda:
    - Là các hàm ảo - không cần quản lý máy chủ.
    - Bị giới hạn thời gian - chủ yếu dùng khi cần xử lý trong thời gian ngắn.
    - Chạy theo yêu cầu.
    - Scale một cách tự động.
## Lợi thế của việc sử dụng AWS Lambda
- Dễ dàng định giá:
    - Trả theo mỗi request và thời gian tính toán.
    - Free tier cho 1,000,000 request và 400,000GBs tính toán.
- Tương thích rất nhiều AWS service khác.
- Hỗ trợ nhiều ngôn ngữ lập trình khác nhau.
- Dễ dàng để theo dõi thông qua AWS CloudWatch.
- Dễ dàng có thêm tài nguyên để chạy hàm (lên tới 10GB RAM).

## Một số dịch vụ tương thích với AWS Lambda.
### Các trường hợp sử dụng chính
- API Gateway: Tạo REST API để gọi Lambda Function.
- Kinesis: Sử dụng Lambda để thực hiện một số bước chuyển hóa dữ liệu trong khi truyền tải.
- DynamoDB: Sử dụng Lambda để tạo một số trigger để mà khi có một số thay đổi nào đó trong DB thì lamda function sẽ chạy.
- S3: Trigger Lambda Function khi có một sự kiện nào đó xảy ra.
- Cloudfront: có dịch vụ Lambda@edge.
- CloudWatchEvents / EventBridge: Bất kì thay đổi nào xảy ra trong hệ thống sẽ được ghi nhận và gọi đến Lambda function nếu cần thiết.
- Cloudwatch Logs: Stream các log này đến nơi mà chúng ta cần.
- SNS: Phản ứng lại một thông báo xảy ra trong SNS Topic.
- SQS: Xử lý message từ SQS Queue.
- Cognito: Phản ứng lại hành vi mỗi khi có một user đăng nhập vào DB.
