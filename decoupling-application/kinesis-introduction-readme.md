# Kinesis
- Là dịch vụ hỗ trợ việc thu thập, xử lý và phân tích stream data trong thời gian thực.
- **Kinesis Data Streams**: Thu thập, xử lý và lưu trữ các dữ liệu dạng stream.
- **Kinesis Data Firehose**: Tải data stream vào AWS data stores.
- **Kinesis Analystics**: Phân tích data stream bằng SQL hoặc Apache Flink.
- **Kinesis Video Streams**: Thu thập, xử lý và lưu trữ video stream.

## Kinesis Data Streams
Là dịch vụ cho phép chúng ta stream big data đến hệ thống. 

### Shard

Stream data được cấu thành nên từ các Shard. Dữ liệu sẽ được chia nhỏ ra và trải dài trên các Shard này. Shard cũng sẽ là căn cứ để quyết định mức độ tiêu thụ của hệ thống.

### Producer
 
Producer sẽ nguồn gửi dữ liệu đến **Kinesis Data Stream**, có thể là chương trình, client, SDK, ... tất cả các producer sẽ cung cấp các bản ghi cho Kinesis Data Stream. Bản ghi về cơ bản được cấu thành bởi hai thành phần:

- Partition Key: giúp xác định bản ghi sẽ được gửi đến Shard nào.
- Data Blob (tối đa 1MB): là dữ liệu.

Producer có thể gửi 1MB/giây hoặc 1000 msg/giây cho mỗi Shard.

Khi dữ liệu đang nằm trong Kinesis Data Stream thì chúng có thể được tiêu thụ bởi nhiều consumer khác nhau, các consumer này có thể là các SDK, Lambda, Kinesis Data Firehose hoặc Kinesis Data Analytics.

Khi consumer nhận được bản ghi, bản shi sẽ chứa các thôn ghi như:
- Partition Key.
- Sequence no, cho biết bản ghi này nằm ở đâu trong shard.
- Data Blob.

Có vài chế độ consume cho Kinesis Data Stream:
- 2MB/s mỗi shard và chia sẻ throughput với các consumer khác.
- 2MB/s (enhanced) mỗi shard cho mỗi consumer.

![img](../images/Screenshot%202025-03-29%20233537.png)

### Tóm tắt các điểm chính của Kinesis Data Stream

- Retention trong khoảng 1 ~ 365 ngày.
- Có khả năng tái xử lý dữ liệu.
- Một khi dữ liệu được thêm vào Kinesis, nó không thể bị xóa.
- Dữ liệu có cùng partition sẽ được gửi đến cùng một shard.
- Producer: AWS SDK, Kinesis Producer Library (KPL), Kinesis Agent.
- Consumer: 
  - Tự định nghĩa: Kinesis Client Library (KCL), AWS SDk.
  - Được quản lý sẵn: AWS Lambda, Kinesis Data Firehose, Kinesis Data Analytics

### Capacity Mode
Có nhiều chế độ khác nhau:
#### Provisioned
- Chúng ta tự dự đoán để chọn số lượng shard, tự mình scale hoặc thông qua API.
- Mỗi shard có 1MB/s cho throughput đầu vào stream (hay 1000 bản ghi trong 1 giây).
- Mỗi shard có 2MB/s cho throughput đầu ra ngoài stream.

Chúng ta sẽ trả tiền cho mỗi shard provision theo môi giờ.

#### On-demand
- Không cần dự đoán hay quản lý shard.
- Hiệu suất dự tính mặc định sẽ là 4MB/s cho throughput đầu vào.
- Tự động mở rộng dựa vào đỉnh throughput quan sát được trong 30 ngày.

Chúng ta trả tiền cho mỗi stream theo mỗi giờ và dữ liệu vào / ra tính theo GB.

> Tóm lại, nếu không rõ hiệu suất cần dùng là bao nhiêu thì nên sử dụng On-demand.

### Security
- Quản lý truy cập / phân quyền sử dụng IAM Policy.
- Mã hóa in flight sử dụng HTTPS endpoint.
- Mã hóa at rest sử dụng KMS.
- VPC endpoint cũng có sẵn cho Kinesis để cho phép nó được truy cập bên trong một VPC.
- Tất cả các API call có thể được theo dõi qua CloudTrail.
