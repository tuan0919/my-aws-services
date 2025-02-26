## EBS Volume
### I) Tóm tắt

- EBS (Elastic Block Store) Volume là một ổ cứng ảo mà có thể được gắn trực tiếp vào instance, kể cả khi chúng đang hoạt động.
- Cho phép instance có thể lưu trữ lại dữ liệu, kể cả khi chúng đã bị terminated.
- Ở trình độ CCP - một instance chỉ có thể được gắn một EBS.
- Bị giới hạn trong một AZ.
- Ở free-tier: 30GB of free EBS storage of type General Purpose (SSD).

![img](../images/Screenshot%202025-02-26%20130745.png)

### II) Tùy chọn Delete on Terminate
- EBS có thể được thiết lập để tự động xóa khi một instance bị xóa.
- Mặc định, root volume sẽ **tự động bị xóa** còn các volume khác thì không. (Có thể thay đổi nếu cần thiết)

![img](../images/Screenshot%202025-02-26%20131043.png)

## ESB Snapshot
### I) Khái niệm
- Chúng ta có thể tạo một bản chụp (snapshot) của EBS tại một thời điểm nhất định.
- **Không cần** detach một volume để tạo snapshot, nhưng được **khuyến khích**.
- Có thể **sao chép** snapshot qua nhiều **AZ khác nhau**.

![img](../images/Screenshot%202025-02-26%20134542.png)

### II) Features
#### 1. EBS Snapshot Archive:
- Chuyển một snapshot vào 'archive tier' có giá rẻ hơn 75%.
- Mất 24 - 72 giờ để khôi phục dữ liệu.
#### 2. Recycle Bin
- Có thể thiết lập để giữ lại các bản snapshot đã xóa trong một khoảng thời gian nhất định, đề phòng trường hợp xóa nhầm.
- Thời gian giữ lại có thể từ 1 ngày - 1 năm.
#### 3. Fast Snapshot Restore (FSR)
- Tạo một EBS volume từ snapshot với tốc độ gần như bất kì.
- Phù hợp với các ứng dụng cần tốc độ khởi động nhanh.
- Đây là tính năng tốn kém và cần cân nhắc khi sử dụng.

### ESB Volume Type

ESB được định danh bởi Size, Throughput, IOPS (I/O Ops Per Sec)

#### I) SSD - Dành cho workload yêu cầu hiệu suất cao
##### General Purpose SSD (gp3, gp2)

- gp3: Mặc định, giá rẻ hơn gp2, hiệu suất ổn định.
- gp2: Cũ hơn, hiệu suất tăng theo dung lượng, ít dùng hơn gp3.

##### Đặc điểm chung

- Cân bằng giữa việc lưu trữ và hiệu suất.
- Phù hợp với đa số tác vụ.

##### Use case

- Khi cần tối ưu dung lượng lưu trữ với độ trễ thấp.
- Làm boot volume của hệ thống, Virtual Desktop, Development hoặc môi trường Test.

##### Provisioned IOPS SSD (io2, io1)

- io2: Cao cấp nhất, dành cho database quan trọng.
- io1: Cũ hơn io2, ít dùng hơn.

##### Đặc điểm chung

- Hỗ trợ EBS Multi-attach
- Phù hợp với các tác vụ có hiệu suất IOPS cao.

##### Use case

- Các chương trình quan trọng cần duy trì hiệu suất IOPS.
- Chương trình cần hơn 16,000 IOPS.
- Các tác vụ database (nhạy cảm với hiệu suất lưu trữ và tính nhất quán). 

#### II) HDD - Dành cho workload throughput cao

- st1: Dành cho workload cần tốc độ truyền tải cao nhưng không yêu cầu IOPS cao.
- sc1: Giá rẻ nhất, hiệu suất thấp, phù hợp cho dữ liệu ít truy cập.

##### Đặc điểm chung

- Không thể dùng làm boot volume.

##### Use case

- st1: Big Data, log processing, streaming.
- sc1: Archive, backup.
