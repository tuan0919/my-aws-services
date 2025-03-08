## Route 53 Health Check
Health Check trong Route 53 giúp kiểm tra trạng thái hoạt động của một endpoint (EC2, ALB, website, API, v.v.). Nếu endpoint bị lỗi, Route 53 có thể tự động chuyển hướng traffic đến endpoint khác. HTTP Health Check chỉ có thể hoạt động trên các **public resource**

Health Check chủ yếu có các loại như sau:

1. Health check theo dõi hoạt động của một endpoint cụ thể (chương trình, server hay AWS resource).
2. Health check theo dõi health check khác (Calculated health check).
3. Health check theo dõi CloudWatch Alarm (full control).

### Health Check - Monitor an Endpoint
Có khoảng 15 global health checker sẽ kiểm tra tình trạng của một endpoint.

- Ngưỡng Healthy/Unhealthy mặc định là 3.
- Chu kỳ mặc định là 30 giây.
- Hỗ trợ các giao thức như: HTTP, HTTPS, TCP.
- Nếu >18% health checker cho biết endpoint là healthy, thì Route 53 sẽ xem như endpoint đang hoạt động bình thường. Còn không thì sẽ là Unhealthy.
- Có thể chọn các vị trí Health Checker mà Route 53 sẽ sử dụng.

Health Check được xem là pass nếu như endpoint trả về status code là 2xx hoặc 3xx. Ngoài ra, Health Check còn có thể kiểm tra cả nội dung bên trong 5120 bytes đầu của response nếu cần thiết.

Health Check hoạt động bằng cách request đến endpoint cụ thể để nhận response, thế nên về cơ bản chúng ta cần phải cấu hình tường lửa / router tại endpoint sao cho Healh Checker có request đến chúng.

![img](../images/Screenshot%202025-03-08%20121400.png)

### Health Check - Calculated Health Checks

Loại Health Check sẽ sử dụng kết quả của nhiều Health Checkers khác, logic pass có thể dùng toán tử **OR**, **AND** hoặc **NOT**.

Có thể theo dõi tối đa kết quả của 256 Health Checker khác nhau

Có thể thiết lập số lượng Health Check cần pass trước khi đưa ra quyết định.

TH sử dụng: thực hiện bảo trì trang web mà không khiến cho toàn bộ health check bị fail.

![img](../images/Screenshot%202025-03-08%20130659.png)

### Health Check - Private Hosted Zones

Route 53 Health Checker nằm bên ngoài các VPC, chúng không thể truy cập trực tiếp vào các private endpoint của VPC.

Thế nhưng, chúng ta có thể tạo một **CloudWatch Metric** và gắn nó vào **CloudWatch Alarm**, sau đó tạo Health Check dể check tại alarm này.

![img](../images/Screenshot%202025-03-08%20130622.png)