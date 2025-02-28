## Auto Scaling Group - ASG

Trên thực tế khi triển khai một website hoặc một chương trình, load có thể thay đổi theo thời gian, kết hợp với việc tại môi trường cloud, việc tạo và hủy các server là rất nhanh chóng và dễ dàng. ASG sẽ giúp:

- Scale out (thêm EC2 instance) để phù hợp với lượng load đang tăng.
- Scale in (bớt EC2 instance) để phù hợp với lượng load đang sụt giảm.
- Cho phép ta có thể thiết lập một lượng tối đa và tối thiểu các instance EC2.
- Tự động đăng ký instance mới với load balancer.
- Tự động tạo lại EC2 instance nếu nó bị terminated hoặc unhealthy.
- ASG là service miễn phí (chỉ trả phí cho các EC2 instance nếu chúng có tính phí).

![img](../images/Screenshot%202025-03-01%20021520.png)

### Launch Template

Để tạo một ASG, chúng ta cần chuẩn bị một Launch Template, là nơi chứa các thông tin về cách khởi tạo một EC2 bên trong ASG:
- AMI + Instance type.
- EC2 User Data.
- EBS Volumes.
- Security Groups.
- SSH Key Pair.
- IAM Roles cho EC2.
- Network + Subnet.
- Thông tin liên quan đến Load Balancer.
- ...

### Auto Scaling với CloudWatch

Có thể scale ASG dựa vào CloudWatch alarms.

Nghĩa là chúng ta có thể thay đổi số lượng EC2 bên trong ASG dựa vào một lệnh trigger tự động được tạo ra bởi CloudWatch Alarm.

Lệnh trigger có thể liên quan đến thông số CPU hoặc các thông tin metrics khác tương tự.

### Scaling Policy

**Dynamic Scaling**
- Target Tracking Scaling:
  - Dễ dàng thiết lập.
  - Ví dụ: thiết lập để ASG CPU trung bình ở mức 40%.
- Simple / Step Scaling:
  - Khi CloudWatch alarm trigger (chẳng hạn CPU > 70%), thì thêm 2 instance.
  - Khi CloudWatch alarm trigger (chẳng hạn CPU < 30%), thì xóa 1 instance.
- Scheduled Scaling:
  - Lập lịch scale khi biết được một số pattern.
  - Ví dụ: tăng min capacity lên 10 vào mỗi 5 giờ chiều thứ 6 vì lượng người dùng tăng cao vào thời điểm đó.
- Predictive Scaling: liên tục tính toán, dự đoán load và scale dựa theo kết quả đó.