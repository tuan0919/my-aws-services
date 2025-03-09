## Stateless Webapp: WhatIsTheTime.com
Giả sử chúng ta đang cần xây dựng một kiến trúc hệ thống cho một trang web đơn giản có tên miền là WhatIsTheTime.com, các yêu cầu cần phải có như sau:
- Trang web cho phép người dùng biết được thời gian hiện tại trong ngày.
- Flow rất đơn giản, khi người dùng request đến thì sẽ nhận được response trả về kết quả.
- Không cần database.
- Có khả năng scale theo cả chiều ngang lẫn chiều dọc, không bị down time.

### Giải pháp 1
**Ý tưởng**:

- Chúng ta sẽ tạo nhiều EC2 instance (giả sử là 3) để đảm bảo có thể xử lý nhiều yêu cầu đồng thời.
- Tạo 1 hosted zone với Route 53 cho tên miền WhatIsTheTime.com.
- Tạo 3 A record cho truy vấn DNS, mỗi record trỏ đến một EC2 instance, TTL là 1 giờ.

![img](../images/Screenshot%202025-03-09%20133624.png)

**Vấn đề gặp phải**:

- Khi một EC2 instance bị xóa hoặc downtime.
- Route 53 do set TTL là 1 giờ, dù cho có bật tính năng health check thì vẫn có khả năng kết quả truy vấn của instance hiện đang down vẫn đang được cache tại máy client.
- Khi họ query đến tên miền đó vẫn sẽ thấy instance bị down.

### Giải pháp 2
**Ý tưởng**:

- Với giải pháp trước đó, vấn đề gặp phải là có khả năng client vẫn bị truy cập vào EC2 instance bị down.
- Thay vì public EC2 instance ra bên ngoài, chúng ta sẽ cho chúng vào một mạng VPC.
- Gắn thêm một Elastic Load Balancer đứng trước, ELB sẽ lo nhiệm vụ route traffic đến VPC và Health Check các EC2 instance trước khi route traffic.
- Route 53 sẽ có một Alias Record trỏ đến Load Balancer thay vì 3 EC2 Instance. 
- Vì ELB được đảm bảo hoạt động bởi AWS, nên chúng ta có thể tin tưởng rằng khả năng nó không hoạt động là rất thấp.

![img](../images/Screenshot%202025-03-09%20134520.png)

**Vấn đề gặp phải**:

- Vẫn còn vấn đề với cách tiếp cận này là với việc scaling.
- Việc scale ứng dụng hiện tại vẫn yêu cầu người quản trị thực hiện một cách thủ công.

### Giải pháp 3
**Ý tưởng**:

- Giải pháp trước đó vẫn còn gặp chút vấn đề trong việc scaling thủ công.
- Ý tưởng là các instance EC2 bây giờ sẽ được gói gọn bên trong một Auto-scaling Group.
- Với ASG, ứng dụng bây giờ có thể tự động mở rộng / thu nhỏ theo nhiều tiêu chí khác nhau mà không khiến cho người quản trị phải thực hiện thủ công.

![img](../images/Screenshot%202025-03-09%20135943.png)

**Vấn đề gặp phải**:

- Chúng ta đang thiết kế kiến trúc dựa trên giả định là các service của AWS không thể bị down.
- Trên thực tế là có khả năng chúng vẫn bị down.
- Các service đang sử dụng hiện tại đang nằm trên cùng một AZ.
- Thế nên, nếu AZ đấy bị down, toàn bộ hệ thống sẽ bị down theo.

### Giải pháp 4

**Ý tưởng**:
- Các giải pháp trước đó chưa thể đảm bảo được vấn đề khi có thảm họa xảy ra.
- Cần tăng cường tính Availability bằng cách spawn sevice trên nhiều AZ khác nhau.
- ELB sẽ được spawn trên nhiều AZ (giả sử là từ AZ1 -> AZ3).
- ASG cũng sẽ trải dài trên nhiều AZ (AZ1 -> AZ3).
- Các instance sẽ được spawn đồng đều trên các AZ này, giả sử có 2 cho AZ1, 2 cho AZ2 và 1 cho AZ3.
- Giả sử một AZ bị down, thì chúng ta vẫn còn 2 AZ khác hoạt động.

![img](../images/Screenshot%202025-03-09%20140742.png)

**Tối ưu hóa chi phí**:

- Chúng ta nhận ra rằng để hệ thống chạy ổn định, luôn luôn có ít nhất 1 instance trên 2 AZ.
- Để tiết kiệm chi phí, chúng ta nghĩ đến việc reserved 1 instance cho hai AZ này.
- Reserved instance sẽ tiết kiệm chi phí hơn.
