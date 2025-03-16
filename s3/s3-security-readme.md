## Amazon S3 Security - Encryption object
Trong S3, chúng ta có thể bảo mật object bên trong Bucket bằng cách mã hóa chúng, có thể sử dụng 1 các cách sau:

Server-Side Encryption (SSE):

- Server-side Encryption với Key được quản lý bởi Amazon (SSE-S3) (*Mặc định được bật*)
- Server-side Encryption với Key được lưu trữ tại **AWS KMS** (SSE-KMS)
  - Sử dụng dịch vụ **AWS Key Management Service** (KMS) để tự quản lý các key dùng để mã hóa.
- Server-side Encryption với key do khách hàng cung cấp (SSE-C)
  - Khách hàng tự quản lý key của mình.

### SSE-S3
- Quá trình mã hóa sẽ sử dụng key được quản lý bởi AWS.
- Object được mã hóa bên phía server.
- Chuẩn mã hóa là **AES-256**.
- Khi muốn yêu cầu Amazon S3 mã hóa dùm chúng ta (sử dụng SSE-S3), thì phải thiết lập header request là 
`"x-amz-server-side-encryption":"AES256"`
- Mặc định được bật cho bucket mới & object mới.

![img](../images/Screenshot%202025-03-16%20142304.png)

### SSE-KMS
- Thay vì dựa vào key được quản lý bởi AWS thì quá trình mã hóa sẽ sử dụng key được người dùng quản lý thông qua AWS KMS.
- Object được mã hóa bên phía server.
- Phải thiết lập header 
`"x-amz-server-side-encryption":"aws:kms"`

![img](../images/Screenshot%202025-03-16%20143725.png)

- Lợi thế: 
  - Người dùng quản lý key + theo dõi lịch sử sử dụng bằng CloudTrail.
- Bất lợi:
  - Với phương pháp này, khi upload file thì phải gọi đến API **GenerateKey** còn khi download file thì phải gọi đến API khác để giải mã file.
  - Mỗi lời gọi API này sẽ được tính vào tổng request/s được phép gọi đến KMS.
  - Nếu S3 có lượng throughput rất cao, và tất cả object đều đc mã hóa bằng KMS thì cách tiếp cận này không tối ưu.

### SSE-C
- Key được quản lý hoàn toàn bên ngoài AWS.
- Quá trình mã hóa vẫn sử dụng key trên, vì khi request sẽ gửi kèm luôn key để mã hóa.
- AWS S3 sẽ KHÔNG lưu key mã hóa mà khách hàng đã cung cấp.
- Bắt buộc sử dụng giao thức HTTPS.
- Key mã hóa bắt buộc phải gửi kèm vào HTTP header, cho mỗi lời gọi request.

![img](../images/Screenshot%202025-03-16%20144712.png)

### Client-Side Encryption
- Phía client sử dụng thư viện Amazon S3 nào đó để thực hiện mã hóa.
- Client bắt buộc phải mã hóa dữ liệu trước khi gửi lên S3.
- Client cũng sẽ là phía thực hiện giải mã khi nhận file về từ S3.
- Nghĩa là, Client toàn quyền quản lý quá trình mã hóa cũng như bảo mật key.

![img](../images/Screenshot%202025-03-16%20145222.png)

## Amazon S3 Security - Encryption in Transit
- Mã hóa trong quá trình truyền tải còn được gọi là SSL/TLS.
- Amazon S3 cung cấp hai endpoint:
  - HTTP endpoint - không mã hóa
  - HTTPS endpoint - mã hóa khi truyền tải
- Để bắt buộc phải mã hóa trong quá trình truyền tải khi client request, có thể sử dụng Bucket Policy để định nghĩa:

  ```js
    {
        "Version": "2012-10-17",
        "Id": "ForceSSLOnlyAccess",
        "Statement": [
            {
                "Sid": "DenyNonSSLRequests",
                "Effect": "Deny",
                "Principal": "*",
                "Action": "s3:GetObject",
                "Resource": [
                    "arn:aws:s3:::your-bucket-name",
                    "arn:aws:s3:::your-bucket-name/*"
                ],
                "Condition": {
                    "Bool": {
                    "aws:SecureTransport": "false"
                    }
                }
            }
        ]
    }
  ```


