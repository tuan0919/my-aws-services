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