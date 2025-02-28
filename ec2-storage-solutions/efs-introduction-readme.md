## EFS - Elastic File System
### I) Khái niệm

- Dịch vụ file storage (lưu trữ dạng tệp) dành cho nhiều EC2 instances truy cập đồng thời.
- Là một mạng file system (network file system) có thể được mount vào nhiều EC2 instance.
- EFS hoạt động với EC2 trong nhiều AZ.
- Độ sẵn sàng cao, có thể mở rộng, tốn kém (gấp 3 lần gp2).
- Trả tiền mỗi lần sử dụng

![img](../images/Screenshot%202025-02-26%20182339.png)

### II) Đặc điểm
- Tương thích với NFS (Network File System v4).
- Sử dụng security group để điều chỉnh control access vào EFS.
- **Chỉ tương thích với các AMI của Linux**.
- File system sẽ tự động được mở rộng, trả tiền mỗi lần dùng, không cần dự trù trước dung lượng.

### III) Use case

- Khi nhiều EC2 instances cần truy cập chung một hệ thống file.
- Khi cần HA cao, dữ liệu lưu trữ nhiều AZ.
- Khi muốn lưu trữ theo dạng file thay vì block storage (EBS).

### IV) Performance Mode

####  General Purpose

- Hiệu suất cân bằng, phù hợp với hầu hết ứng dụng.
- Dùng cho web server, CMS (WordPress), container.

#### Max I/O

- Dành cho workload cần nhiều kết nối đồng thời (Big Data, Machine Learning).
- Có độ trễ cao hơn General Purpose.

### V) Storage Classes

#### Storage Tier

- Với tính năng quản lý lifecycle, các file trong EFS sẽ được di chuyển sang các tier khác nhau để lưu trữ sau N ngày.
- Khai báo lifecycle policies để quản lý lifecycle.

![img](../images/Screenshot%202025-02-26%20184724.png)

##### Standard

- Dùng cho dữ liệu truy cập thường xuyên.
- Giá cao hơn Infrequent Access.

##### Infrequent Access tier (EFS-IA)

- Dùng cho dữ liệu ít truy cập để tiết kiệm chi phí.
- Có thể tự động chuyển dữ liệu giữa Standard ↔ IA.

##### Archive

- Dữ liệu hiếm khi truy cập (vài lần mỗi năm), rẻ hơn 50%.

#### Availability & durability tier

##### Standard

- Nằm trên nhiều AZ.
- Dành cho ứng dụng ở môi trường production, yêu cầu tính khả dụng cao, tránh thảm họa.

##### One Zone

- Một AZ.
- Phù hợp cho môi trường phát triển.
- Phù hợp với IA (EFS One Zone - IA).
- Tiết kiệm hơn.

## EFS vs EBS
### EBS

- 1 instance (trừ trường hợp mutli-attach io1/io2).
- Bị giới hạn trong một AZ cụ thể.
- Để di chuyển ESB volume qua nhiều AZ thì cần phải tạo snapshot rồi chép qua AZ khác.
- Root EBS Volume mặc định sẽ bị terminate cùng với EC2 instance.

### EFS

- Hỗ trợ hàng trăm instance trải dài trên nhiều AZ.
- EFS chia sẻ file vs nhau.
- Chỉ hỗ trợ AMI Linux.
- EFS tốn kém hơn EBS.
