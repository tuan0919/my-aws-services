## Load Balancing

Load Balancer là các server mà sẽ đóng vai trò điều phối traffic đến nhiều server khác bên dưới (chẳng hạn, EC2 instances).

![img](../images/Screenshot%202025-02-27%20123948.png)

Load Balancer mang lại nhiều lợi thế như:

- Chia nhỏ load ra cho nhiều instance bên dưới.
- Tạo ra một điểm truy cập tập trung (DNS) cho ứng dụng.
- Có thể xử lý failure một cách liền mạch khi có instance bị down (Load Balancer có thể kiểm tra xem instance đích có down hay không trước điều phối traffic đến).
- Health check định kỳ cho instance.
- High availability trên nhiều zone khác nhau.
- Tách biệt traffic public và traffic private trong ứng dụng.

### Tại sao lại sử dụng Elastic Load Balancer?

- Một Elastic Load Balancer là một **Managed Load Balancer**:
  - AWS đảm bảo rằng nó sẽ hoạt động.
  - AWS sẽ chịu trách nhiệm cho việc nâng cấp, bảo trì và high availability.
  - AWS chỉ cung cấp một vài nấc điều chỉnh cho chúng ta.
- Tiết kiệm thời gian thay với việc tự tay thiết lập thủ công một Load Balancer.
- Được tích hợp sẵn với nhiều dịch vụ và ưu đãi khác trong AWS.

### Health Check 

- Health Check là một bước quan trọng cần thực hiện của một Load Balancer.
- Bước này cho phép Load Balancer biết được nếu instance được chuyển tiếp traffic có khjả năng để phản hồi request hay không.
- Health Check được thực hiện qua một port và route nào đó (thường là /health).
  - LB sẽ gửi một request đến route để thực hiện health check đối với instance sẽ được forward request.
  - Nếu response không phải là 200 (OK), nghĩa là instance không sẵn sàng để xử lý request.

### Các loại Load Balancer trong AWS

Có 4 loại Managed Load Balancer trong AWS

#### Classic Load Balancer - CLB

- HTTP, HTTPS, TCP, SSL.
- Về cơ bản, AWS không khuyến khích sử dụng LB này, nên sẽ bị đánh dấu là deprecated.

#### Application Load Balancer - ALB

- HTTP, HTTPS, WebSocket.

#### Network Load Balancer - NLB

- TCP, TLS, UDP.

#### Gateway Load Balancer - GWLB

- Hoạt động ở layer 3 (Network layer) - IP Protocol

Về cơ bản, nên sử dụng Load Balancer thế hệ mới hơn vì chúng cung cấp nhiều tính năng hơn.

Một vài balancer có thể được thiết lập như là **internal (private) LB** hoặc **external (public) LB**.

### Load Balancer Security Groups

Nên thiết lập security group cho phép user có quyền truy cập đến Load Balancer thông qua hai giao thức là HTTP và HTTPS (port 80 và 443).

![img](../images/Screenshot%202025-02-27%20130903.png)

Khi đó, Security Group Rule của một EC2 nên được thiết lập như sau:

![img](../images/Screenshot%202025-02-27%20131029.png)

- EC2 chỉ cho phép traffic đến từ Load Balancer.
- Source của rule là security group của Load Balancer, nghĩa là đang link security group của Load Balancer với security group của EC2.