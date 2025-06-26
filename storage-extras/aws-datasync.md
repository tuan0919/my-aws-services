# AWS Data Sync

- Di chuyển một lượng lớn dữ liệu lớn ra vào:
  - Các hạ tầng tại chỗ / các dịch vụ đám mây khác của AWS (NFS, SMB, HDFS, S3 API, ...) - cần agent.
  - Từ một AWS đến một AWS khác (các dịch vụ lưu trữ khác nhau) - không cần đến agent.
- Có thể đồng bộ hóa với:
  - Amazon S3 (bất kỳ lớp lưu trữ nào - bao gồm cả Glacier).
  - Amazon EFS.
  - Amazon FSx (Windows, Lustre, NetApp, OpenZFS, ...)
- Các task Replication có thể được lên lịch theo giờ, theo ngày hoặc theo tuần.
- **Data Sync có khả năng giữ lại quyền truy cập file cũng như metadata của chúng** (NFS POSIX, SMB, ...)
- Một agent task có thể sử dụng 10Gbps, và cũng có thể giới hạn lại băng thông nếu muốn.

![img](../images/Screenshot%202025-06-23%20160107.png)
