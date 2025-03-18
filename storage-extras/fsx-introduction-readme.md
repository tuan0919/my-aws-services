## Amazon FSx
- Cho phép chúng ta launch một high-performance 3rd party file systems trên AWS.
- Là một service được quản lý sẵn.

### Amazon FSx for Windows (File server)
- Là FSx hỗ trợ cho file system share drive của Windows.
- Hỗ trợ giao thức SMB và Windows NTFS.
- Tích hợp Microsoft Active Directory, ACLs, user quotas.
- **Có thể được mount vào Linux EC2 instance**.
- Hỗ trợ **Microsoft Distributed File System Namespaces** (DFS), cho phép nhóm các tập tin trên nhiều file system khác nhau.
- Scale tối đa hơn 10GB/s, hàng triệu IOPS, hơn 100PB dữ liệu.
- Storage options:
  - SSD - workload yêu cầu độ trễ thấp (database, media processing, data analytics, ...)
  - HDD - các workload đa dạng hơn (home directory, CMS, ...)
- Có thể truy cập tại on-premise infrastructure (thông qua VPN hoặc kết nối trực tiếp).
- Có thể được thiết lập để hỗ trợ Multi-AZ.
- Dữ liệu được backup mỗi ngày vào S3.

### Amazon FSx for Lustre
- Lustre là loại file system phân tán song song, dùng cho các tác vụ tính toán lớn.
- Dùng cho Machine Learning, High Performance Computing (HPC).
- Scale đến hơn 100 GB/s, hàng triệu IOPs, độ trễ sub-ms.
- Storage options:
  - SSD
  - HDD
- Tích hợp liền mạch với S3.
  - Có thể đọc S3 như là một File System.
  - Có thể viết output của các tác vụ tính toán trực tiếp lên S3.
- Có thể được sử dụng tại on-premise sever (qua VPN hoặc direct connect).

### Amazon FSx for NetApp ONTAP
- NetApp ONTAP được quản lý trên AWS.
- **File system tương thích với giao thức NFS, SMB, iSCSI**
- Di chuyển workload đang chạy trên ONTAP hoặc NAS sang AWS.
- Hoạt động với:
  - Linux
  - Windows
  - MacOS
  - VMWare Cloud trên AWS
  - EC2, ECS, EKS.
- Storage tự động thu nhỏ và tăng.
- **Point-in-time instaneous cloning (hữu ích khi cần test workload mới)**

### Amazon FSx for OpenZFS
- OpenZFS file system được quản lý trên AWS.
- Là file system tương thích với NFS (v3, v4.1, v4.2).
- Cho phép di chuyển workloads đang chạy trên ZFS lên AWS.
- Hoạt động với:
  - Linux
  - Windows
  - MacOS
  - VMWare Cloud trên AWS
  - EC2, ECS, EKS.
- Hỗ trợ tới 1,000,000 IOPs với độ trễ < 0.5ms.
- Snapshot, compress và low-cost.
- **Point-in-time instaneous cloning (hữu ích khi cần test workload mới)**

### FSx File System Deployment Options
#### Scarch File System
- Temporary storage.
- Data không được replica (không bền vững nếu như server fail).
- High burst (nhanh hơn 6 lần, 200MBps per TiB).
- Usage: các tác vụ xử lý ngắn hạn, tối ưu hóa chi phí.

#### Persistent File System
- Long-term storage.
- Data được replica trong cùng AZ.
- Thay thế failed files trong vòng vài phút.
- Usage: long-term processing, sensitive data.

![img](../images/Screenshot%202025-03-18%20130915.png)
