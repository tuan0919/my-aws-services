## Amazon Relational Database Service - RDS

Là dịch vụ database được quản lý bởi AWS, sử dụng SQL làm ngôn ngữ truy vấn.

Cho phép chúng ta tạo ra các database trên đám mây và được quản lý bởi AWS. Hỗ trợ nhiều database engine như:
- Postgres.
- MySQL.
- MariaDB.
- Oracle.
- Microsoft SQL Server.
- IBM DB2.
- Aurora (DB của AWS).

### Lợi thế của việc sử dụng RDS thay vì tự deploy một DB trên EC2

RDS là dịch vụ đc quản lý sẵn bởi AWS, cung cấp các tính năng như:
- Tự động được cài đặt, nâng cấp và cung cấp các bản vá.
- Liên tục được backup và khôi phục lại tại một thời điểm bất kì.
- Quan sát thông qua dashboard.
- Có nhiều replica để tối ưu cho quá trình đọc dữ liệu.
- Có thể cài đặt trên nhiều AZ để tránh thảm họa.
- Khả năng mở rộng (theo cả hai chiều).
- Dữ liệu được lưu lại trên EBS (gp2 hoặc io1).

**Nhưng không thể kết nối SSH đến DB**.

### Storage Auto Scaling
RDS cung cấp khả năng tự động mở rộng cho RDS DB instance khi nó phát hiện ra database đang gần hết dung lượng.

Chúng ta có thể cài đặt **Maximum Storage Threshold** (ngưỡng tối đa cho DB Storage) để chỉ định RDS có thể mở rộng tối đa bao nhiêu.

Mặc định, RDS sẽ tự động mở rộng khi:
- Free storage bé hơn 10% dung lượng được cấp phát.
- Tình trạng low-storage diễn ra ít nhất được 5p.
- 6 tiếng kể từ lần mở rộng cuối.

Tính năng này rất hữu ích cho các chương trình mà không xác định được workload cụ thể.

### RDS Read Replicas

Các Replica có mục đích là để tăng hiệu suất của tác vụ read trong database.

- RDS hỗ trợ 15 Read Replicas.
- Replica có các loại như: within AZ, cross AZ hoặc cross region.
- Thao tác sao chép dữ liệu sang Replica là async, nghĩa là dữ liệu có thể không đồng bộ ngay lập tức.
- Nếu cần thiết, một replica có thể được "thăng chức" trở thành một database khác, nhưng khi đó Replica này sẽ trở thành một DB độc lập và không còn được tối ưu cho tác vụ read. 

**Tình huống cần sử dụng đến Replica**

1. Chúng ta có một production database đang chạy bình thường.
2. Chương trình yêu cầu thêm một số tính năng liên quan đến thống kê hay phân tích số liệu.
3. Chúng ta tạo một Read Replica từ database gốc, sau đó thực hiện các tác vụ thống kê tại đó. (để database gốc không bị ảnh hưởng hiệu suất)
4. Tại replica, chỉ chấp nhận các câu truy vấn READ.

### Network Cost

Trong AWS, thường sẽ có một phí cho việc truyền tải data từ AZ này đến AZ khác, nhưng một số service sẽ là ngoại lệ, RDS Replica là một trong số đó.

Đối với các RDS Replicas nằm **trong cùng một region**, chúng ta không cần trả khoản phí này. Nhưng vẫn sẽ bị tính phí nếu thực hiện truyền tải Cross Region.

### RDS Multi AZ (Phục hồi sau thảm họa)

RDS Multi AZ về cơ bản là đối với một RDS A (Master), chúng ta sẽ tạo thêm một RDS B (Slave) nằm ở AZ khác.

Mỗi khi A thực hiện update, tác vụ đó sẽ phải được thực hiện đồng bộ sang B, nếu thất bại tại B thì coi như tại A cũng thất bại.

Chương trình chính khi giao tiếp với RDS sẽ sử dụng một DNS name nào đó chứ không chỉ định instance cụ thể.

RDS B sẽ tồn tại như là một bản backup cho A, nghĩa là không ai có quyền đọc nó, update nó hay mở rộng nó một cách trực tiếp, nó chỉ được sử dụng khi A xảy ra sự cố nghiêm trọng.

**Lưu ý**: Như đã nhắc đến trong phần [Read Replicas](#rds-read-replicas), các Read Replicas nếu cần thiết hoàn toàn có thể trở thành một DB độc lập, nghĩa là các Read Replica có thể đc thăng cấp thành một **RDS Multi AZ**.

![img](../images/Screenshot%202025-03-03%20011727.png)