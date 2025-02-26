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