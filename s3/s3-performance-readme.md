## S3 - Baseline Performance
- Amazon S3 mặc định hỗ trợ 3,500 PUT/COPY/DELETE hoặc 5,500 GET/HEAD request mỗi giây cho từng prefix bên trong bucket.
- Không có giới hạn về số lượng prefix có trong một bucket.
## Tăng hiệu suất khi upload
- Multi-part upload:
   - Chia file upload thành các file nhỏ hơn sau đó upload song song đến server để tăng hiệu suất.
   - Khuyến khích sử dụng cho các file > 100MB, bắt buộc sử dụng khi file > 5GB. 
- S3 Transfer Accelaration:
  - Tăng tốc độ truyền tải bằng cách di chuyển file đến AWS edge location.
  - Bằng việc đưa file đến edge location, AWS sẽ thực hiện upload file đó đến S3 bằng private traffic của họ => tối ưu hơn so với public traffic.

![img](../images/Screenshot%202025-03-15%20005724.png)

## Tăng hiệu suất khi đọc
- **S3 Byte-Range Fetches**:
  - Về cơ bản cũng giống Multi-part upload, đọc file theo từng range byte nhỏ hơn nhưng thực hiện song song.

## S3 Select & Glacier Select
Đôi khi chúng ta cần fetch một file trên S3 về, sau đó lại thực hiện truy vấn trên file đấy để filter ra các dataset mình cần sử dụng. Cách tiếp cận này tạo ra sự lãng phí data transfer vì chúng ta chỉ cần một phần dữ liệu trong file đó.

**S3 Select** có thể được sử dụng để truy vấn dữ liệu ngay trên file, sau đó trả kết quả truy vấn về. Cách tiếp cận này sẽ tối ưu hơn rất nhiều nếu như giả sử chúng ta chỉ cần 100 row trong một file CSV có hàng ngàn record.

Bên cạnh S3 Select, AWS cũng hỗ trợ Glacier Select, cho phép ta truy vấn record trong các file đang nằm ở Glacier class.

![img](../images/Screenshot%202025-03-15%20122924.png)

## S3 Batch Oprations
Chúng ta có thể thực hiện hàng loạt thao tác trên nhiều Object khác nhau trong S3 với một request duy nhất:
- Chỉnh sửa object metadata & properties.
- Sao chép object giữa các bucket khác nhau.
- Mã hóa các object chưa được mã hóa.
- Chỉnh sửa ACLs, tags trên các object.
- Khôi phục object từ S3 Glacier.
- Gọi Lambda Function để thực hiện một thao tác nào đó trên mỗi object.

Một **job** sẽ bao gồm list object sẽ bị tác động, hành động sẽ thực hiện và các tham số kèm theo nếu cần thiết.

S3 Batch Operations sẽ quản lý việc retry, track progress, gửi thông báo hoàn thành, tạo report, ...

Có thể sử dụng S3 Inventory để lấy object list rồi dùng S3 Select để filter các object trong lsit đó.

![img](../images/Screenshot%202025-03-15%20141805.png)

## S3 - Storage Lens
Dùng để quan sát, phân tích và tối ưu hóa lưu trữ cho toàn bộ AWS Organization.

Phát hiện điểm bất thường, tìm hướng tối ưu hóa chi phí, áp dụng các cơ chế bảo vệ dữ liệu trên toàn bộ AWS Organization (trong phạm vi 30 ngày gần nhất).

Hỗ trợ dashboard, có thể sử dụng dashboard mặc định hoặc tự custom dashboard nếu muốn.

Có thể được thiết lập để export các reports, metrics mỗi ngày vào S3 Bucket.

![img](../images/Screenshot%202025-03-15%20160447.png)

### Metrics

Có các loại metrics sau trong Storage Lens:
- Summary Metrics:
  - Thông số tổng quan về S3 Storage.
  - StorageBytes, ObjectCount, ...
  - Use case: xác định xu hướng phát triển nhanh (hoặc không đc sử dụng) của một bucket hay prefix nào đó.
- Cost-Optimization Metrics:
  - Cung cấp các thông số có thể được sử dụng để tối ưu hóa chi phí.
  - NonCurrentVersionStorageBytes, IncompleteMultipartUploadStorageBytes, ...
  - Use case: xác định bucket nào có các file chưa được upload hoàn thiện (do cơ chế multipart-upload) trong 7 ngày, xác định xem object nào có thể được chuyển xuống các lớp lưu trữ có giá thấp hơn, ...
- Data-Protection Metrics:
  - Các thông số liên quan đến các tính năng bảo vệ dữ liệu.
  - VersioningEnabledBucketCount MFADeleteEnabledBucketCount, ...
  - Use case: xác định bucket nào đang không tuân theo best practice trong bảo mật dữ liệu.
- Access-management Metrics:
  - Các thông số liên quan đến quyền sở hữu S3 Object.
  - ObjectOwnershipBucketOwnerEnforcedBucketCount, ...
  - Use case: xác định bucket đang sử dụng thiết lập Object Ownership nào.
- Event Metrics:
  - Các thông số liên quan đến Event Notifications.
  - EventNotificationEnabledBucketCount.
  - Use case: xác định bucket nào đang được thiết lập sử dụng S3 Event Notification.
- Performance Metrics:
  - Thông số liên quan đến S3 Transfer Accelaration.
  - TransferAccelarationBucketCount.
  - Use case: xác định bucket nào đang bật transfer accelaration.
- Activity Metrics:
  - Thông số liên quan đến việc storage được request đến như thế nào.
  - AllRequests, GetRequests, PutRequests, ListRequests, BytesDownloaded, ...
- Detailed Status Code Metrics:
  - Thông số liên quan đến HTTP Status Code.
  - 200OKStatusCount, 403ForbiddenErrorCount, 404NotFoundErrorCount, ...

### Free Tier vs Paid Tier
#### Free Metrics
- Tự động có sẵn cho toàn bộ khách hàng.
- Có 28 metrics khả dụng.
- Dữ liệu sẵn sàng để query trong vòng 14 ngày.

#### Advanced Metrics và Recommendations
- Các metrics nâng cao - Activiy, Advanced Cost Optimization, Advanced Data Protection, Status Code, ...
- CloudWatch Publish - Cho phép truy cập metrics trong CloudWatch mà không phải trả thêm phí.
- Prefix Aggregation - Thu thập metrics ở cấp độ prefix.
- Dữ liệu sẵn sàng để query trong vòng 15 tháng.