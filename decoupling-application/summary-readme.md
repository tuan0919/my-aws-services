## Phân biệt SQS vs SNS vs Kinesis

### SQS
- Consumer chủ động pull dữ liệu để tiêu thụ.
- Dữ liệu tự động bị xóa sau khi bị tiêu thụ.
- Không giới hạn số lượng consumer.
- Không cần phải ước tính throughput vì đây là một dịch vụ được quản lý toàn diện.
- Khả năng sắp xếp message chỉ áp dụng cho dạng hàng đợi FIFO.
- Có thể trì hoãn message một cách độc lập.

### SNS
- Dữ liệu được push đến cho nhiều subscriber cùng một lúc.
- Tối đa 12,500,000 subsrciber.
- Dữ liệu không bền vững vì có thể bị thất thoát nếu không được gửi.
- Là mô hình dạng Pub/sub.
- Tối đa 10,000 topic.
- Không cần phải ước tính throughput vì đây là một dịch vụ được quản lý toàn diện.
- Có thể kết hợp với **SQS** để hiện thực Fan-out pattern.
- Có khả năng FIFO để phục vụ cho SQS FIFO.

### Kinesis
- Standard: pull dữ liệu.
- Dạng fan-out cải tiến hơn: push dữ liệu.
- Có khả năng replay dữ liệu.
- Được sử dụng cho tác vụ thời gian thực, big data, phân tích, ...
- Sắp xếp message ở mức độ các shard.
- Dữ liệu hết hạn sau 1 khoảng thời gian.
- Có hai mode: provisioned và on-demand.

### Amazon MQ

Các dịch vụ như SQS, SNS là dịch vụ thuần đám mây, sử dụng giao thức độc quyền bởi AWS.

Các ứng dụng truyền thống thì lại thường sử dụng các giao thức mở như MQTT, AMQP, STOMP, Openwire, WSS...

Điều này sẽ khiến ứng dụng khá khó khăn để có thể tích hợp vào máy chủ đám mây, vì thế thay vì tái cấu trúc lại các hệ thống này để sử dụng SQS hay SNS, chúng ta có thể sử dụng Amazon MQ.

Amazon MQ là một dịch vụ message broker được quản lý phục vụ cho hai công nghệ phổ biến: **RabbitMQ** và **ActiveMQ**.

- Amazon MQ sẽ không scale thoải mái như SQS / SNS.
- Amazon MQ chạy trên các máy chủ, cho nên có thể chạy đa vùng (Multi-AZ) với các cơ chế chuyển đổi dự phòng (failover).
- Amazon MQ có cả hai tính năng: queue như SQS và topic như SNS.

