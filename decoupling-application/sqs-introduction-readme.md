# Amazon SQS
## Standard Queue
Là service được quản lý toàn diện, dùng cho các ứng dụng tách rời.
- Đặc tính:
  - Không giới hạn throughput, không giới hạn số lượng message nằm trong queue.
  - Giữ lại message mặc định trong 4 ngày, tối đa 14 ngày.
  - Độ trễ thấp (< 10ms cho tác vụ `publish` và `receive`).
  - Giới hạn 256KB cho mỗi message được gửi.
- Có thể có message lặp lại.
- Có thể có message không đúng thứ tự.

### Phát hành message
- Sử dụng SDK để phát hành message đến SQS (SendMessage API).
- Message sẽ được giữ lại trong SQS cho đến khi consumer xóa (tiêu thụ) nó.
- Message có thể được giữ lại trong: 4 - 14 ngày.

### Tiêu thụ message
- Consumer là một chương trình nào đó, EC2 instances, AWS Lambda, ...
- Consumer sẽ poll SQS để lấy message (có thể lấy tối đa 10 message một lúc).
- Sau khi có message, sẽ thực hiện xử lý message đó với tác vụ nào đấy.
- Sau khi xử lý xong message, sẽ xóa message bằng DeleteMessage API.

### Nhiều consumer đồng thời
Trong trường hợp có nhiều consumer đồng thời cùng poll SQS:

- Các message sẽ được phân phối song song (at least once delivery).
- Trong trường hợp này, nếu như một consumer chậm hơn một consumer khác, thì message có thể bị consumer khác lấy và tiêu thụ mất.
- Chúng ta có thể tăng throughput bằng cách scale consumer theo chiều ngang.

Để đạt best practice, thì SQS sẽ được sử dụng chung với ASG:
  - Các EC2 instance sẽ được đặt trong 1 ASG.
  - ASG được thiết lập sẽ tự động scale theo chiều ngang bởi một CloudWatch alarm.
  - CloudWatch được thiết lập để theo dõi metric nào đó của SQS (chẳng hạn: `ApproximateNumberOfMessages`).
  - Các instance EC2 sẽ tự động tăng giảm để đáp ứng lượng message hiện có trong SQS.

![img](../images/Screenshot%202025-03-22%20134849.png)

### Bảo mật SQS
**Mã hóa**:

  - Mã hóa trong lúc truyền tải sử dụng HTTPS API.
  - Mã hóa tại chỗ sử dụng key KMS.
  - Mã hóa phía client nếu client tự mã hóa và giải mã.

**Quản lý truy cập**: sử dụng IAM Policy để quản lý quyền truy cập vào SQS API

**SQS Access Policy** (tương tự như S3 Bucket Policy):
- Hữu ích khi muốn quản lý truy cập SQS trên nhiều tài khoản.
- Cho phép các service khác (SNS, S3, ...) được phép ghi vào SQS.