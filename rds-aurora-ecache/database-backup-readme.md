## RDS Backup 

Tự động:
- Thực hiện full backup **mỗi ngày** cho database.
- Transaction log được back up **mỗi 5 phút**, đồng nghĩa thời gian để rollback gần nhất là 5 phút trước so với thời điểm hiện tại.
- Có thể thiết lập khoảng thời gian cho bản backup được giữ từ 1 - 35 ngày, nếu thiết lập thành 0 thì sẽ vô hiệu hóa tính năng này.

Thủ công:
- Được kích hoạt bởi người dùng.
- Có thể giữ lại bản Backup trong bất kể bao lâu.

Mẹo: kể cả có dừng RDS database thì chúng ta vẫn sẽ trả một khoản phí lưu trữ. Cho nên nếu thời gian dừng sử dụng đủ lâu, thì thay vào đó ta nên tạo một bản snapshot rồi restore database từ bản snapshot đấy.

## Aurora Backup

Tự động:
- 1 - 35 ngày (không thể vô hiệu hóa).
- Có thể rollback về bất kì thời điểm nào trong khoảng thời gian này.

Thủ công:
- Kích hoạt bởi người dùng.
- Giữ lại backup bất kể bao lâu.

## Khả năng khôi phục
Có thể khôi phục RDS / Aurora snapshot để tạo thành một database mới hoàn toàn.

### Khôi phục MySQL RDS database từ S3
  - Tạo một bản backup cho database.
  - Lưu trữ bản backup này trên s3.
  - Load bản backup này trên một RDS instance khác đang chạy MySQL.

### Khôi phục MySQL Aurora cluster từ S3
  - Tạo bản backup cho database bằng Percona XtraBackup.
  - Lưu bản backup này trên s3.
  - Load bản backup này trên một Aurora instance khác đang chạy MySQL.

## Aurora Database Cloning
- Cho phép tạo một Aurora DB Cluster mới từ bản gốc.
- Tốc độ sẽ nhanh hơn snapshot hay restore.
- Sử dụng trong trường hợp cần tạo một "staging database" để thao tác thay vì trực tiếp trên production database.
- Sử dụng giao thức **copy-on-paste**:
  - Tạo một DB Cluster mới nhưng sử dụng chung ổ đĩa dữ liệu với DB Cluster gốc (không có quá trình copy data nên tốc độ nhanh hơn).
  - Khi có thay đổi trên DB Cluster mới tạo, thì sẽ cấp phát thêm một vùng nhớ mới trên ổ đĩa và viết dữ liệu mới vào vùng nhớ đấy (cô lập dữ liệu mới và dữ liệu cũ với nhau).
  - DB gốc không hề bị ảnh hưởng dù DB mới đang sử dụng cùng ổ đĩa với DB gốc.
  