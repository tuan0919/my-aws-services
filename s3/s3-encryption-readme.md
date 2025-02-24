## Bảo mật & mã hóa các đối tượng tài nguyên trong S3
### Mã hóa khi di chuyển (Encryption in Transmit)

- SSL/TLS
- HTTPS

### Mã hóa ở trạng thái nghỉ (Encryption at rest): Server-Side Encryption

Khi Object thật sự nằm trong S3:
- SSE-S3: Bản thân S3 sẽ quản lý key cũng như giải mã, sử dụng kiểu mã hóa AES 256-bit encryption, phổ biến & dễ sử dụng nhất.
- SSE-KMS: AWS Key Management Service quản lý key.
- SSE-C: Customer-Provided key.

### Mã hóa ở trạng thái nghỉ (Encryption at rest): Client-Side Encryption

Có 2 cách để làm:

- Console: Lựa chọn tùy chọn mã hóa trong S3 bucket của bạn. Cách dễ dàng nhất là chọn 1 checkbox trong S3 console.
- Bucket Policy: Bạn có thể thực thi mã hóa sử dụng một bucket policy.

### Enforcing Server-Side Encryption for S3 Uploads
**S3 Put Request**: Tại mỗi một thời điểm khi 1 file được tải lên S3 thì sẽ có 1 PUT Request được bắt đầu khởi tạo bởi trình duyệt web, request header thường có dạng như sau:

```
PUT /myFile HTTP/1.1
Host: myBucket.s3.amazonaws.com
Date: Wed, 25 Nov 2020 09:50:22 GMT
Authorization: authorization string
Content-Type: text/plain
Content-Length: 27364
x-amz-meta-author: Ryan
Expect: 100-continue
[27364 bytes of object data]
```

**x-amz-server-side-encryption**

Nếu file được mã hóa trong thời gian upload file, tham số `x-amz-server-side-encryption` sẽ được thêm vào header của request.

Có hai tùy chọn:

- X-amz-server-side-encryption: AES 256-bit (SSE-S3-S3-managed keys)
- X-amz-server-side-encryption: aws:kms

Khi tham số được bao gồm vào header của PUT request này, nó sẽ nói với S3 là sử dụng đúng phương pháp mã hóa để mã hóa object tại thời điểm upload.

```
PUT /myFile HTTP/1.1
Host: myBucket.s3.amazonaws.com
Date: Wed, 25 Nov 2020 09:50:22 GMT
Authorization: authorization string
Content-Type: text/plain
Content-Length: 27364
x-amz-meta-author: Ryan
Expect: 100-continue
x-amz-server-side-encryption: AES256 // <-- Tham số yêu cầu AWS mã hóa
[27364 bytes of object data]
```

Bạn có thể tạo một bucket policy, cho phép nó từ chối các S3 Put Request mà không bao gồm tham số `x-amz-server-side-encryption` trong header.