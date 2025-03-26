# Amazon SNS
Là dịch vụ phân phối tin nhắn sử dụng mô hình Pub/Sub.
- Producer chỉ gửi tin nhắn đến một SNS topic.
- Không giới số lượng Subscriber đăng ký lắng nghe một topic nào đó.
- Mỗi Subscriber đăng ký đến một topic thì sẽ nhận được toàn bộ message từ topic đó (có thể lọc bớt message).
- SNS được tích hợp sẵn với nhiều AWS service khác, cho phép chúng có thể gửi thông báo đến SNS.
## Cách để publish
**Publish vào topic (dùng SDK)**
- Tạo topic
- Tạo một hoặc nhiều đăng ký đến topic.
- Publish message vào topic

**Publish trực tiếp (cho SDK mobile app)**
- Tạo một ứng dụng trên mobile.
- Tạo một endpoint.
- Publish message trực tiếp vào endpoint đó.

## Bảo mật
Về cơ bản, SNS có cơ chế bảo mật cũng tương tự SQS:

**Mã hóa**
- Mã hóa truyền tải sử dụng HTTPS API.
- Mã hóa tại chỗ sử dụng KMS.
- Mã hóa phía client nếu client là bên chịu trách nhiệm mã hóa / giải mã.

**Quản lý truy cập**
- Sử dụng IAM Policy để quản lý truy cập đến các SNS API.

**SNS Access Policy** (tương tự như S3 bucket policy)
- Dùng khi muốn truy cập cross-account.
- Cho phép các service khác đc phép viết vào SNS topic

## Fan Out Pattern
Fan out pattern là một pattern sẽ kết hợp SQS + SNS lại với nhau, từ đó khắc phục được nhược điểm của SNS là có thể bị mất message. Cụ thể:
- Message sẽ được gửi một lần bởi SNS, sau đó được lưu trữ tại các SQS đã subscribe SNS.
- Đảm bảo không bị thất thoát dữ liệu.
- SQS sẽ có nhiệm vụ lưu trữ message tạm thời và cho phép retry xử lý message.
- Có thể tăng thêm số lượng SQS theo thời gian nếu cần.
- Cần đảm bảo rằng SQS acccess policy cho phép SNS được phép ghi vào.
- **Cross-Region Delivery**: một SNS có thể kết hợp với các SQS ở các region khác.

![img](../images/Screenshot%202025-03-26%20232441.png)

## FIFO Topic
Amazon SNS cũng hỗ trợ các FIFO topic giúp đảm bảo thứ tự các message bên trong một topic.

- Các tính năng tương tự như SQS FIFO:
  - Sắp xếp message theo group id (các message có cùng group id sẽ được sắp xếp theo thứ tự).
  - Tránh duplicate dựa vào id hoặc content.
- **Có thể có SQS Standard hoặc FIFO queues là subscribers**.
- Bị giới hạn throughput (giống như SQS FIFO).

Ngoài ra có thể áp dụng Fan Out pattern cho SNS FIFO trong trường hợp chúng ta muốn fan out + ordering + deduplication.

![img](../images/Screenshot%202025-03-26%20233700.png)

## Message Filtering
- Là một JSON Policy dùng để lọc message được gửi đến topic subscription.
- Nếu một suscription không có filter policy, nó sẽ nhận tất cả message.
