# AWS Transfer Family
- Là dịch vụ cho phép truyền tải file ra vào Amazon S3 hoặc Amazon EFS sử dụng giao thức FTP.
- Được quản lý sẵn về cơ sở hạ tầng, scalable, Reliable và High Available (Multi-AZ).
- Trả phí mỗi giờ cho một endpoint + data truyền tải tính theo GB.
- Lưu trữ và quản lý các xác thực của người dùng bên trong service.
- Có thể tích hợp với hệ thống xác minh bên ngoài như Microsoft Active Directory, LDAp, ...
- Sử dụng: chia sẻ file, các public dataset, CRM, ...

![img](../images/Screenshot%202025-03-22%20085551.png)

# AWS DataSync
- Dùng để di chuyển lượng lớn dữ liệu:
  - Từ On-primise / Cloud khác đến AWS (qua giao thức: NFS, SMB, S3 API, ...) - cần agent.
  - Từ một dịch vụ đến một dịch vụ khác trong AWS - không cần agent.
- Có thể đồng bộ hóa các dịch vụ như:
  - Amazon S3.
  - Amazon EFS.
  - Amazon FSx.
- Replication Task có thể được lên lịch theo giờ, theo ngày hoặc theo tuần.
- **Quyền truy cập file và metadata sẽ được giữ nguyên vẹn**.
- Một agent task có thể sử dụng 10 Gbps và có thể thay đổi được giới hạn bandwith này.

![img](../images/Screenshot%202025-03-22%20092255.png)