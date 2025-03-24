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
