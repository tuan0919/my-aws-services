# AWS Snow Family
## Overview

AWS Snow Family là nhóm các thiết bị vật lý được sử dụng để di chuyển dữ liệu lớn giữa on-premises và AWS khi băng thông mạng không đủ hoặc yêu cầu bảo mật cao. Snow Family bao gồm AWS Snowcone, AWS Snowball và AWS Snowmobile.

## Khi nào sử dụng Snow Family?
- Di chuyển dữ liệu lớn (>10 TB) từ on-premises lên AWS.
- Mạng yếu hoặc không ổn định không thể dùng AWS Direct Connect hoặc Internet.
- Dữ liệu nhạy cảm cần được xử lý tại chỗ trước khi đưa lên AWS.
- Triển khai tại vùng xa (tàu biển, quân sự, dầu khí) nơi không có kết nối mạng ổn định.

###  AWS Snowcone
- Nhỏ gọn nhất (8.5 lbs ~ 4 kg), có pin di động, chịu điều kiện khắc nghiệt.
- Dung lượng 8 TB HDD hoặc 14 TB SSD.
- Hỗ trợ AWS DataSync để di chuyển dữ liệu liên tục.
- Chạy EC2 instances & IoT Greengrass cho edge computing.
- Kết nối: Wi-Fi, Ethernet, USB-C.

### AWS Snowball
Có hai phiên bản:
- **Snowball Edge Storage Optimized** (80 TB HDD, 1 TB SSD cache).
- **Snowball Edge Compute Optimized** (42 TB HDD, GPU optional).
  - Hỗ trợ EC2 instances, AWS Lambda, S3-compatible storage.
  - AES-256 encryption + TPM (Trusted Platform Module).
  - Kết nối: 10G/25G/40G Ethernet.

### AWS Snowmobile
- Siêu lớn, có thể di chuyển 100 PB trong một container 45-foot.
- Được bảo vệ vật lý chặt chẽ (GPS tracking, multi-factor authentication, security escort).
- Chỉ dùng cho data migration cực lớn (các trung tâm dữ liệu lớn, media, tài chính).

