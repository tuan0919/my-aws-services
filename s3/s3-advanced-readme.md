## Amazon S3 - Lifecycle Rules
Lifecycle rule của S3 cho phép tự động chuyển đổi object trong bucket sang storage class khác.
- **Transaction action** - thiết lập chuyển đổi object sang một storage class khác
  - Chẳng hạn, di chuyển object sang lớp Standard IA sau 60 ngày lưu trữ.
  - Di chuyển sang Glacier để bảo vệ sau 6 tháng lưu trữ.
- **Expiration action** - thiết lập cho phép object hết hạn hoặc bị xóa sau một khoảng thời gian nào đó.
  - Chẳng hạn, access log có thể bị xóa sau 365 ngày.
  - Có thể được sử dụng để xóa các version cũ của một file một cách tự động (nếu versioning được bật).

Rules có thể được thiết lập để áp dụng cho các object với prefix nào đó: (chẳng hạn: s3://mybucket/mp3/*)

Rules có thể được thiết lập để áp dụng cho các object với tag nào đó (chẳng hạn: Departmant: Finance)