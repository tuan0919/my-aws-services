# AWS Cloudfront
Cloudfront là một dịch vụ Content Delivery Network (CDN) của AWS, có nhiệm vụ tăng hiệu suất đọc bằng cách cache content tại các edge location của Amazon.
- Cloudfront có hơn 200 edge location ở toàn thế giới.
- Giúp bảo vệ hệ thống khỏi tấn công DDoS.
- Có thể tích hợp với Shield, AWS Web Application Firewall.

## Cloudfront Origins
Cloudfront có thể hỗ trợ các origin sau:

**S3 Bucket**
- Phân phối file và cache chúng lại ở các edge.
- Tăng cường bảo mật với Cloudfront Origin Access Control (OAC).
- Cloudfront có thể được sử dụng như một ingress (dùng để upload file lên S3).
  - Ingress là thuật ngữ dùng để chỉ lưu lượng vào (incoming traffic) từ bên ngoài vào một hệ thống hoặc mạng cụ thể.

**Custom Origin (HTTP)**
- Application Load Balancer.
- EC2 Instance.
- S3 Website.
- Bất kỳ HTTP backend nào khác.

## Phân biệt Cloudfront vs S3 Cross Region Replication

**Cloudfront**:
- Global Edge network.
- File đc cache trong 1 khoảng thời gian (có thể là 1 ngày).
- **Dùng cho các dữ liệu tĩnh cần phải phân phối đi khắp nơi**

**S3 Cross Region Replication**:
- Cần phải setup cho từng region nếu muốn thực hiện replication.
- File được cập nhật gần như ngay lập tức.
- Chỉ dùng để đọc.
- **Dùng cho các dữ liệu động cần phải đc phân phối đi một vài region với độ trễ thấp**.