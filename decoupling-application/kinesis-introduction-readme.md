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


