## Backup dữ liệu với S3 Replication
### S3 Replication

- Có thể sao chép các object từ một bucket đến một bucket khác, Versioning phải được bật ở cả hai bucket nguồn và bucket đích.
- Các object đã tồn tại trong bucket không được sao chép tự động.
- Tất cả các object được cập nhật vào sẽ được tự động sao chép, chỉ khi replication được bật.
- Delete marker là mặc định không được sao chép: những version riêng lẻ hoặc delete markers sẽ không được sao chép.