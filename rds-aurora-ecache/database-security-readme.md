## RDS & Aurora Security
Trong AWS hỗ trợ bảo mật database theo các cách sau:
- At rest encryption: mã hóa dữ liệu của db được lưu trên ổ cứng.
  - Tùy chọn này cần phải được cài đặt tại lúc launch database.
  - Database master & replicas sẽ được mã hóa thông qua dịch vụ AWS KMS.
  - Nếu Master không được mã hóa, thì các replicas của nó cũng không được phép mã hóa.
  - Để mã hóa một database chưa được mã hóa, cần phải tạo bản snapshot cho DB đó rồi restore dưới tùy chọn mã hóa.
- In-flight encryption: mã hóa trên traffic truyền tải dữ liệu.
  - Cả RDS và Aurora đều được thiết lập sẵn để có thể bật tính năng TLS.
  - Người dùng sẽ cần sử dụng chứng chỉ AWS TLS để có thể kích hoạt SSL.
- IAM Authentication: bên cạnh việc sử dụng username / password theo cách truyền thống, EC2 instance có thể kết nối trược tiếp đến RDS/Aurora bằng cách sử dụng IAM Role.
- Security Groups: kiểm soát các traffic truy cập qua mạng đến RDS / Aurora DB.
- Không có SSH: ngoại trừ RDS Custom thì cho phép truy cập trực tiếp đến EC2 instance bên dưới qua SSH.
- Audit logs: trong trường hợp cần theo dõi thời gian kết nối, các câu truy vấn đã được sử dụng, ... bên trong DB thì có thể bật tính năng này để cho phép RDS/Aurora gửi logs đến **AWS CloudWatch** và lưu trữ tại đó.
