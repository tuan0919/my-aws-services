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

## Amazon S3 - Requester Pays
Thông thường thì bucket owner phải chịu chi phí cho việc lưu trữ object trên S3 và data transfer của các tài nguyên trên bucket.

Với **Requester Pays** bucket, người request sẽ là bên chịu chi phí data transfer khi truy cập đến một tài nguyên trên bucket. Hữu ích trong trường hợp muốn chia sẻ dataset lớn với một tài khoản khác.

Requester cần phải là một tài khoản AWS được xác minh rõ ràng để có thể là bên chịu phí.

## Amazon S3 - Event Notifications
Một event S3 sẽ được tạo ra khi có một thao tác nào đó xảy ra, chẳng hạn: `S3:ObjectCreated`, `S3:ObjectRemoved`, `S3:ObjectRestore`, ... Các event này có thể được truyền tới các service như **AWS SNS**, **AWS SQS** hoặc **AWS Lambda**.

Trường hợp sử dụng: tự động tạo thumbnail cho ảnh hoặc video được upload lên S3.

Không giới hạn số lượng event tạo ra trong S3, các event này thường sẽ được phân phối trong vài giây, nhưng cũng có một vài trường hợp tốn đến vài phút.

### IAM Permission

Để S3 có thể phân phối các event đến các service khác thì cần một số thiết lập về quyền dành cho S3, cụ thể:
- SNS: Cần thiết lập policy cho phép S3 có quyền `SNS:Publish` để publish event message vào SNS.
- SQS: Cần thiết lập policy cho phép S3 có quyền `SQS:SendMessage` để publish event message vào SQS.
- Lambda Function: Cần thiết lập policy cho phép S3 có quyền `lambda:InvokeFunction` để có thể gọi đến function cần thiết khi có event xảy ra.

![img](../images/Screenshot%202025-03-14%20235742.png)

### EventBridge

Ngoài việc để S3 phân phối event trực tiếp đến các service đã liệt kê phía trên, thì còn cách tiếp cận khác là tất cả các event của S3 sẽ được phân phối đến **EventBridge**.

Tại EventBridge, chúng ta sẽ thiết lập một số rule và nhờ các rule này mà các event sẽ được phân phối đến các AWS Service khác.

![img](../images/Screenshot%202025-03-15%20000805.png)