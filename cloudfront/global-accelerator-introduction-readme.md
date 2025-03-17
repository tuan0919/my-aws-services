
# Global Accelerator
## Global User
Khi chúng ta deploy một application tại một region nào đó, nhưng tập người dùng lại nằm khắp nơi trên thế giới thì sẽ có vấn đề về độ trễ khi người dùng muốn request đến server.

Chúng ta sẽ muốn giảm độ trễ đi nhiều nhất có thể bằng cách khiến traffic đi qua mạng nội bộ của AWS.

## Unicast vs Anycast
Trước khi tìm hiểu Global Accelerator thì cần phải hiểu hai concep này.

- **Unicast**: Là khái niệm chúng ta quen thuộc, một server giữ một IP address.
- **Anycast**: Nhiều server giữ chung một IP address và client sẽ được định hướng đến server gần nhất khi truy cập IP address này.

## AWS Global Accelerator
- Tận dụng mạng nội bộ của AWS để định hướng đến chương trình backend.
- 2 Anycast IP sẽ được tạo cho chương trình backend.
- Anycast IP sẽ gửi traffic trực tiếp đến các Edge Location

![img](../images/Screenshot%202025-03-17%20110258.png)

- Hỗ trợ **Elastic IP**, **EC2**, **ALB**, **NLB**, **public** hoặc **private**.
- Hiệu suất ổn định
  - Tự động routing đến nơi có độ trễ thấp nhất và failover nhanh.
  - Không gặp vấn đề về client cache vì IP không thay đổi.
  - Mạng nội bộ AWS.
- Health Checks.
  - Thực hiện health check cho application.
- Bảo mật.
  - Chỉ có 2 external IP cần được whitelist.
  - Được bảo vệ khỏi tấn công DDoS nhờ vào AWS Shield.

## AWS Global Accelerator vs CloudFront
- Đều sử dụng  AWS global network và edge location được trải dài toàn cầu.
- Đều tích hợp với AWS Shield để chống DDoS.

**Cloudfront**:
- Tăng hiệu suất cho cacheable content (chẳng hạn như images và videos).
- Phân phối dynamic content.
- **Content được gửi từ edge location**.

**Global Accelerator**:
- Tăng hiệu suất cho nhiều loại ứng dụng khác nhau sử dụng TCP hoặc UDP.
- **Proxy packet tại edge location đến chương trình backend gốc**.