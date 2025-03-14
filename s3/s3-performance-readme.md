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
