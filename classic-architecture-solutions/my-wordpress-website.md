## Stateful Web App: MyWordPress.com
- Website yêu cầu có thể upload và hiển thị hình ảnh đã upload.
- Dữ liệu cá nhân người dùng trong website nên được lưu trữ trong MySQL database.

### Giải pháp 1
**Ý tưởng**:
- Route 53 để quản lý DNS cho tên miền MyWordPress.com.
- Một ELB Multi AZ để thực hiện Load Balancer.
- Route 53 có một Alias Record route traffic đến ELB.
- Nhiều EC2 Instance để chạy server, spawn trên nhiều AZ và được gói trong một ASG để thực hiện scaling nếu cần thiết.
- Một RDS sử dụng MySQL engine để lưu trữ dữ liệu người dùng. Sử dụng Read Replicas để tăng hiệu suất đọc.

![img](../images/Screenshot%202025-03-10%20232651.png)

**Vấn đề gặp phải**:
- Chưa có nơi để lưu trữ dữ liệu ảnh.

### Giải pháp 2
**Ý tưởng**:
- Có một EBS Volume để lưu trữ ảnh.

![img](../images/Screenshot%202025-03-10%20233058.png)

**Vấn đề gặp phải**:
- EBS Volume đi cùng với EC2 Instance cho nên với việc có nhiều EC2 Instance thì cũng có nhiều EBS Volume.
- EBS Volume ở các AZ khác nhau cho nên dữ liệu được lưu trữ sẽ khác nhau ở từng AZ.
- Cần có cơ chế để chia sẻ dữ liệu giữa các EBS Volume.

### Giải pháp 3
**Ý tưởng**:
- Thay vì sử dụng EBS Volume riêng biệt cho từng instance, sử dụng EFS.

![img](../images/Screenshot%202025-03-11%20021919.png)