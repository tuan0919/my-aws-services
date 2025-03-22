## Các lựa chọn lưu trữ trong AWS
#### Object Storage (Lưu trữ đối tượng)
- **Amazon S3**: Lưu trữ đối tượng, có độ bền cao, chi phí thấp, thích hợp cho backup, data lake, và web hosting.
- **Amazon S3 Glacier**: Lưu trữ dữ liệu ít truy cập (archive), chi phí cực thấp, truy xuất có thể mất vài phút đến vài giờ.
#### Block Storage 🔗 (Lưu trữ khối - dành cho máy ảo, container)
- **Amazon EBS** (Elastic Block Store): Lưu trữ gắn với EC2, hiệu suất cao, dùng cho database, ứng dụng yêu cầu IOPS ổn định.
- **Amazon EC2 Instance Store**: Lưu trữ tạm thời, nhanh hơn EBS nhưng dữ liệu mất khi instance bị tắt.
#### File Storage 📁 (Lưu trữ tệp - dùng cho nhiều máy cùng truy cập)
- **Amazon EFS** (Elastic File System): Hệ thống file NFS dùng chung, mở rộng tự động, thích hợp cho container, analytics, và machine learning.
- **Amazon FSx**: Dịch vụ file system chuyên biệt, gồm:
  - **FSx for Windows**: dành cho ứng dụng Windows.
  - **FSx for Lustre**: Hiệu suất cao, tối ưu cho vác vụ tính toán hiệu suất cao. (High Performance Computing - HPC).
  - **FSx for NetApp ONTAP**: tương thích nhiều dạng hệ điều hành.
  - **FSx for OpenZFS**: dành cho ZFS file system.
#### Hybrid & Data Migration 🌉 (Lưu trữ kết hợp on-premise và cloud)
- **AWS Storage Gateway**: Cầu nối giữa on-premise và AWS, hỗ trợ File Gateway, Volume Gateway, và Tape Gateway.
- **AWS DataSync**: Dịch vụ sao chép dữ liệu nhanh giữa on-premise và AWS.
#### Edge Storage 🌍
- **AWS Snow Family**: Thiết bị phần cứng di động để chuyển dữ liệu lớn lên AWS.

