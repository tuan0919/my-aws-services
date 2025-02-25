## Một số kiến thức về EC2 ở trình độ SAA
### I. Elastic IP trong EC2
- Khi chúng ta stop và start một EC2 instance, instance này sẽ bị thay đổi public IP.
- Nếu chúng ta cần một địa chỉ public ip cố định, sẽ cần có một **Elastic IP**.

>**Về cơ bản thì, nên tránh sử dụng đến Elastic IP**
>- Nhu cầu sử dụng Elastic IP thường xảy ra do các quyết định không tối ưu khi xây dựng hệ thống.
>- Thay vào đó, nên sử dụng public IP ngẫu nhiên và đăng ký một DNS name cho nó.
>- Hoặc, sử dụng Load Balancer và không dùng đến public IP.

### II. Placement Groups
- Đôi khi chúng ta muốn tự kiểm soát chiến lược bố trí (Placement Strategies) nơi đặt EC2 instance.
- Placement Strategies có thể được định nghĩa bằng cách sử dụng Placement Groups.
- Các loại Placement Strategies:
  - Cluster: 
    - Đặt tất cả instances gần nhau trên cùng một phần cứng vật lý.
    - Tối ưu tốc độ truyền dữ liệu giữa các instances.
    - Phù hợp với các ứng dụng yêu cầu low latency & high throughput, như HPC (High Performance Computing), Machine Learning, Big Data processing.
    - Chỉ hoạt động trong cùng một AZ, không hỗ trợ multi-AZ.
  - Spread:
    -  Trải đều các instance trên nhiều phần cứng khác nhau
    -  Hỗ trợ tối đa 7 instances trong một Availability Zone.
    -  Phù hợp với ứng dụng yêu cầu độ ổn định cao, như database cluster, ứng dụng quan trọng.
  - Partition:
    - Tách biệt các instances theo partition.
    - Mỗi partition được đặt trên một nhóm phần cứng vật lý riêng biệt. 
    - Giảm rủi ro mất dữ liệu khi một nhóm phần cứng bị lỗi
    - Tối ưu cho hệ thống phân tán lớn như Big Data, Hadoop, HDFS, Cassandra, Kafka.
    - Tối đa 7 partitions trong một Availability Zone. Hỗ trợ lên tới hàng trăm instance EC2.

### III. Elastic Network Interfaces (ENI)
#### 1) Khái niệm
- ENI là một adapter mạng ảo trong AWS EC2, giúp các instances có thể giao tiếp với nhau và với mạng bên ngoài.
- Nó giống như card mạng (NIC - Network Interface Card) trong máy tính vật lý, nhưng được AWS quản lý.
#### 2) Đặc điểm chính
- Có thể tạo và gán vào một hoặc nhiều EC2 instances.
- Hỗ trợ nhiều địa chỉ IP, bao gồm Primary & Secondary IPs.
- Gắn được Elastic IP để truy cập từ Internet.
- Có thể tách ENI khỏi một instance và gán vào một instance khác, giúp duy trì địa chỉ IP ngay cả khi instance thay đổi.
- Hỗ trợ Security Group & Network ACLs, giúp kiểm soát lưu lượng vào/ra.
- Bị giới hạn trong một AZ nhất định, nghĩa là nếu tạo ENI trong một AZ nào đó thì chỉ có thể sử dụng ENI này nếu ở trong AZ đó.

![img](../images/Screenshot%202025-02-26%20023116.png)

### IV. EC2 Hibernate State
#### 1) Khái niệm
EC2 Hibernate là một trạng thái (state) cho phép dừng một instance mà không mất dữ liệu trong RAM, giúp khởi động lại nhanh chóng mà không cần khởi động lại từ đầu. Nó hoạt động tương tự như Hibernate mode trên máy tính cá nhân.
#### 2) Cách hoạt động

1️⃣ Khi Hibernate được kích hoạt, AWS lưu trạng thái RAM vào ổ đĩa gốc (root volume) EBS.

2️⃣ EC2 instance được đưa vào trạng thái "Stopped" nhưng dữ liệu RAM vẫn được giữ lại.

3️⃣ Khi bật lại, AWS khôi phục dữ liệu RAM từ EBS và tiếp tục từ trạng thái trước đó.

📌 Khác với "Stop" bình thường, khi dùng Hibernate, instance không bị mất dữ liệu RAM.

#### 3) Nhu cầu sử dụng
-  Ứng dụng có quá trình khởi động dài (VD: tải nhiều dữ liệu vào RAM).
- Machine Learning / Big Data Processing, cần giữ dữ liệu RAM giữa các lần chạy.
- Ứng dụng yêu cầu giữ session liên tục, như giao dịch tài chính.
- Giảm chi phí, vì không cần chạy liên tục nhưng vẫn giữ trạng thái trước đó.


