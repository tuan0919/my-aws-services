# Hybrid Cloud for Storage
AWS hiện tại đang thúc đẩy mô hình "hybrid cloud", nghĩa là:
- Một phần hạ tầng được triển khai trên đám mây.
- Một phần hã tầng đượcc triển khai nội bộ tại chỗ.

Nguyên nhân có thể là do:

- Quá trình chuyển đôi sang lâu tốn nhiều thời gian.
- Các yêu cầu về bảo mật.
- Một số quy tắc của dự án.
- Các chiến lược trong IT.

**Các service như AWS S3** lại là dạng service độc lập trên đám mây (không như EFS / NFS), vậy làm sao để có thể tiết lộ dữ liệu trên S3 cho các hạ tầng tại chỗ khác? Cầu nối giữa S3 và cơ sở hạ tầng tại chỗ này sẽ là **AWS Storage Gateway**.

## AWS Storage Gateway
- Có thể xem là một dạng cầu nối cho dữ liệu tại chỗ và dữ liệu trên đám mây.
- Use case:
  - Khôi phục sau thảm họa.
  - Backup & restore.
  - Phân lớp cách thức lưu trữ trong dự án.
  - Tận dụng Storage gateway như là một cache cho dữ liệu tại chỗ.
- Có vài loại Storage gateway:
  - S3 File Gateway
  - FSx File Gateway
  - Volume Gateway
  - Tape Gateway

### S3 File Gateway
- Cho phép các S3 buckets có thể được truy cập tại hạ tầng tại chỗ bằng cách sử dụng protocol NFS và SMB.
- **Dữ liệu được sử dụng gần đây nhất sẽ được cache tại file gateway**.
- Hỗ trợ: S3 Standard, S3 Standard IA, S3 One Zone, S3 Intelligent Tiering.
- **Tuy gaterway không truy cập trực tiếp vào S3 Glacier được nhưng vẫn có thể chuyển object từ S3 đến S3 Glacier bằng cách dùng Lifecycle Policy**.
- Việc truy cập vào bucket sẽ cần IAM Role đối với mỗi File Gateway.
- Giao thức SMB được tích hợp với Active Directory (AD) để xác thực người dùng.

![img](../images/Screenshot%202025-03-22%20013619.png)

### FSx File Gateway
Thực tế, FSx vẫn cho phép truy cập tại cơ sở hạ tầng tại chỗ mà không cần dùng đến gateway, thế nhưng việc dùng gateway vẫn mang lại các lợi ích sau:
- **Local cache các dữ liệu được truy cập thường xuyên tại gateway**.
- Tương thích với hệ thống Windows (SMB, NTFS, Active Directory, ...)
- Hữu ích khi muốn nhóm tệp tin và các thư mục gốc.
 
![img](../images/Screenshot%202025-03-22%20014456.png)

### Volume Gateway
- Là thành phần lưu trữ dạng khối (block storage) sử dụng iSCSI protocol với backend là S3.
- Hỗ trợ khôi phục lại dữ liệu tại chỗ với backend là EBS Snapshot.
- Có hai chế độ hoạt động:
  - Cached Volume Mode: Lưu trữ dữ liệu chính trên Amazon S3, hạ tầng tại chỗ chỉ giữ lại cache để truy xuất nhanh.
  - Stored Volume Mode: Lưu trữ toàn bộ dữ liệu tại hạ tầng tại chỗ, đồng thời sao lưu lên AWS bằng EBS Snapshots.

![img](../images/Screenshot%202025-03-22%20020158.png)

### Tape Gateway
- Một số công ty vẫn backup dữ liệu bằng các băng từ vật lý (physical tapes).
- Với Tape Gateway, công ty vẫn sử dụng cùng quy trình, nhưng là lưu trữ tại đám mây.
- Mô phỏng thư viện băng từ (VTL - Virtual Tape Library), cho phép phần mềm sao lưu nhận diện như một thiết bị vật lý.
- Lưu trữ dữ liệu sao lưu trên Amazon S3 và có thể di chuyển sang Amazon Glacier để tối ưu chi phí lưu trữ lâu dài.

![img](../images/Screenshot%202025-03-22%20021201.png)

## Hardware appliance
- Sử dụng Storage Gateway sẽ yêu cầu sử dụng một cơ chế ảo hóa ở hạ tầng tại chỗ.
- Có một cách tiếp cận khác là đặt mua tại Amazon một thiết bị phần cứng chuyên biệt để sử dụng.
- Thiết bị này có đủ cấu hình yêu cầu để chạy Storage Gateway, hỗ trợ được: File Gateway, Volume Gateway và Tape Gateway.
- Lựa chọn này đôi khi sẽ hữu ích đối với các data center nhỏ không có đủ hạ tầng để hỗ trợ ảo hóa.

![img](../images/Screenshot%202025-03-22%20021726.png)
