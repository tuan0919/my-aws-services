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
