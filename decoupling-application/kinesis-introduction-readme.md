# Kinesis
- Là dịch vụ hỗ trợ việc thu thập, xử lý và phân tích stream data trong thời gian thực.
- **Kinesis Data Streams**: Thu thập, xử lý và lưu trữ các dữ liệu dạng stream.
- **Kinesis Data Firehose**: Tải data stream vào AWS data stores.
- **Kinesis Analystics**: Phân tích data stream bằng SQL hoặc Apache Flink.
- **Kinesis Video Streams**: Thu thập, xử lý và lưu trữ video stream.

## Kinesis Data Streams
Là dịch vụ cho phép chúng ta stream big data đến hệ thống. 

![img](../images/Screenshot%202025-03-29%20233537.png)

### Summary

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

## Kinesis Data Firehose

Dùng để phân phối stream data nhận vào đến một đích lưu trữ nào đó.

### Summary

- Dịch vụ được quản lý hoàn toàn, không cần quản trị, tự động mở rộng, serverless.
  - AWS: Redshift / Amazon S3 / OpenSearch.
  - Dịch vụ bên thứ ba: Splunk / MongoDB / DataDog / NewRelic / ...
  - Tự thiết lập: HTTP endpoint nào đó.
- Trả tiền cho lượng dữ liệu được truyền tải qua Firehose.
- Gần như ngay lập tức.
- Hỗ trợ nhiều data format, conversion, transformation, compression.
- Hỗ trợ cho phép tự custom một tác vụ transform data bằng AWS Lambda.
- Có thể gửi các dữ liệu thất bại hoặc tất cả dữ liệu đến S3 Bucket.

### Kinesis Data Stream vs. Kinesis Data Firehose
|Kinesis Data Stream|Kinesis Data Firehose|
|-------------------|---------------------|
|Là dịch vụ streaming dữ liệu để tiêu thụ|Là dịch vụ load dữ liệu stream vào một đích đến nào đó|
|Tự viết mã (cho producer / consumer)|Được quản lý sẵn|
|Thời gian thực|Gần thời gian thực|
|Tự kiểm soát scale|Tự động scale|
|Lưu trữ dữ liệu từ 1 - 365 ngày|Không lưu trữ dữ liệu|
|Hỗ trợ khả năng replay|Không hỗ trợ replay|