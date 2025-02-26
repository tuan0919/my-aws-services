## EC2 Instance Store
- EBS volumes là các ổ cứng đám mây ảo nên có độ trễ nhất định.
- Nếu cần sử dụng một ổ cứng vật lý với hiệu năng cao, sử dụng EC2 Instance Store.

### Đặc điểm của EC2 Instance Store
- Hiệu suất I/O tốt hơn.
- EC2 Instance Store sẽ mất data nếu bị stopped.
- Use case: buffer / cache / scratch data / temporary content.
