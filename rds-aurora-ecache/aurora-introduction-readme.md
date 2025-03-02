## Amazon Aurora
- Aurora là công nghệ DB thuộc về Amazon (không phải là engine mã nguồn mở).
- Cả Postgres và MySQL đều hỗ trợ Aurora DB (nghĩa là driver sẽ hoạt động như thể Aurora là Postgres hoặc MySQL).
- Aurora là database được tối ưu hóa cho cloud trên AWS, cho nên nó sẽ nhanh gấp 5 lần so với MySQL và 3 lần so với Postgres khi hoạt động trên RDS.
- Aurora storage sẽ tự động được mở rộng từ 10 GB -> 128 TB.
- Aurora có thể có 15 replica và quá trình sao chép sẽ nhanh hơn MySQL.
- Failover trong Aurora sẽ xảy ra gần như ngay lập tức mà không cần tốn thời gian để đồng bộ.
- Aurora tốn kém hơn RDS (đắt hơn 20%), nhưng tối ưu hơn nếu tính lâu dài.

### High Availability
- Amazon Aurora tự động sao chép dữ liệu đồng bộ giữa tối đa 6 bản sao lưu (replicas) trên 3 AZ trong cùng một Region.
- Một instance sẽ đảm nhận vai trò write. (master)
- Tối đa 15 replica khác sẽ đảm nhận vai trò read.
- Tự động thực hiện failover cho master trong vòng 30s.
- Hỗ trợ Cross Region Replication.

### Aurora DB Cluster

Aurora DB Cluster là kiến trúc trung tâm của Aurora, trong đó bao gồm các thành phần chính giúp đảm bảo hiệu năng và tính sẵn sàng cao.

Kiến trúc này bao gồm hai thành phần chính:
- Writer Endpoint: Client sẽ kết nối với instance đóng vai trò là Writer Endpoint khi thực hiện thao tác cập nhật, như cái tên của mình, instance này sẽ chỉ có nhiệm vụ ghi và cập nhật dữ liệu trong database.
- Reader Endpoint: Aurora có nhiều replica của database, số lượng các replica này có thể tự động mở rộng và tối đa là 15, do đó sẽ có một Load Balancing đóng vai trò là Reader Endpoint và kết nối toàn bộ Replica đó. Client sẽ kết nối đến endpoint này khi thực hiện thao tác đọc dữ liệu, quá trình load balancing sẽ diễn ra và một kết nối chính thức đến một trong các replica sẽ được thiết lập.

![img](../images/Screenshot%202025-03-03%20025240.png)