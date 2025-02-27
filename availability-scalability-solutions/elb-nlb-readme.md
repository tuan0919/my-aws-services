## Network Load Balancer - NLB

- Hoạt động ở Layer 4 (TCP/UDP).
- Cho phép forward TCP & UDP traffic.
- Hỗ trợ hàng triệu kết nối đồng thời với độ trễ cực thấp (~1 ms). Thích hợp cho các ứng dụng yêu cầu độ trễ thấp và tốc độ cao.
- Mỗi NLB sẽ cung cấp một địa chỉ IP tĩnh cho từng AZ, và hỗ trợ gán Elastic IP.
- Không nằm trong free tier của AWS.

### Target Groups

- EC2 instances.
- IP Address.
- Application Load Balancer - ALB

![img](../images/Screenshot%202025-02-27%20200009.png)