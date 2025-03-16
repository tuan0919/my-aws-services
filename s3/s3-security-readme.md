# Amazon S3 Security

## I) Encryption object
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

## II) Encryption in Transit
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

## III) CORS

### CORS là gì?

- **CORS (Cross-Origin Resource Sharing)** là một cơ chế bảo mật của trình duyệt web.
- Nó kiểm soát việc một website có thể gửi request đến một server ở một **origin** khác hay không.
- **Origin** là tổ hợp của:
  - **Scheme (protocol)**: HTTP, HTTPS.
  - **Host (domain)**: example.com, api.example.com.
  - **Port**: 80 (HTTP), 443 (HTTPS), hoặc các port tùy chỉnh khác.

### Cách hoạt động của CORS

- Khi một trang web gửi request đến một server **khác origin**, trình duyệt sẽ kiểm tra **CORS policy**.
- Nếu server **cho phép** request từ origin đó, nó sẽ phản hồi với **CORS headers**, ví dụ:
  ```
  Access-Control-Allow-Origin: https://example.com
  ```
- Nếu không có header này hoặc giá trị không khớp, trình duyệt sẽ **chặn request**.

#### Ví dụ về cùng origin & khác origin

- **Cùng origin:**
  - `http://example.com/app1`
  - `http://example.com/app2`
- **Khác origin:**
  - `http://www.example.com` (khác `example.com` do có `www`)
  - `http://other.example.com` (khác do subdomain khác nhau)

### CORS trong Amazon S3

- Khi sử dụng **Amazon S3** để lưu trữ tài nguyên tĩnh (ảnh, video, JSON...), bạn có thể cần **bật CORS** nếu dữ liệu được truy cập từ các website khác.
- Ví dụ, nếu một trang web **https://mywebsite.com** muốn tải ảnh từ **S3 bucket**, thì S3 cần có **CORS policy** cho phép domain đó.
- Một policy mẫu cho phép mọi nguồn truy cập:
  ```xml
  <CORSConfiguration>
    <CORSRule>
      <AllowedOrigin>*</AllowedOrigin>
      <AllowedMethod>GET</AllowedMethod>
      <AllowedHeader>*</AllowedHeader>
    </CORSRule>
  </CORSConfiguration>
  ```
  - `AllowedOrigin`: Cho phép tất cả origin (`*`).
  - `AllowedMethod`: Chỉ cho phép phương thức **GET**.
  - `AllowedHeader`: Chấp nhận tất cả header trong request.

> ⚠ **Lưu ý:** Không nên dùng `*` cho **production** nếu không cần thiết, thay vào đó hãy chỉ định domain cụ thể để bảo mật.

## IV) MFA Delete
MFA (Multi-factor Authentication) - yêu cầu người dùng phải generate một đoạn mã trên thiết bị khác (thường là điện thoại hoặc phần cứng chuyên biệt nào đó) trước khi thực hiện một thao tác quan trọng nào đó trên S3.

MFA sẽ cần thiết khi:
- Xóa vĩnh viễn một object version nào đó.
- Tạm dừng Versioning trên một bucket.

MFA sẽ không cần thiết khi:
- Bật Versioning.
- Liệt kê các object version bị xóa.

Để có thể sử dụng MFA Delete, Versioning phải được bật trên bucket.

Chỉ có chủ bucket (root) mới có thể bật/tắt tính năng MFA Delete.

## V) Access Logs
- Để phục vụ cho việc kiểm kê, chúng ta có thể sẽ muốn log lại toàn bộ truy cập đến S3 bucket.
- Bất kì request nào đến S3, từ bất kì account nào, được cho phép hay từ chối đều sẽ được log tại một S3 bucket khác.
- Các dữ liệu này có thể được sử dụng để phân tích, kiểm kê, ... bằng các tool phân tích dữ liệu khác nhau.
- Bucket logging phải ở cùng region với bucket nguồn.

## VI) Pre-Signed URLs
- Các Pre-signed URLs có thể được tạo ra với S3 Console, AWS CLI hoặc SDK.
- Thời hạn sử dụng URL:
  - S3 Console - 12 giờ.
  - AWS CLI - 168 giờ.
- Với Pre-signed URLs, một user có thể được kế thừa quyền của user khác đã tạo pre-signed URL đó.

## VII) S3 Glacier Vault Lock & Object Lock
### Glacier Vault Lock
- Khi muốn thực thi mô hình WORM (Write Once Read Many).
- Tạo ra một Vault Lock Policy.
- Khóa Policy này lại và ngăn bất kì hành động chỉnh sửa hay xóa đối với policy này.
### Object Lock
- Versioning bắt buộc phải được bật.
- Cũng dùng để thực thi mô hình WORM.
- Chặn hành vi xóa một object version nào đó trong một khoảng thời gian nhất định.
- Có hai dạng retention mode: Compliance và Governance.
#### Compliance
- Object version không thể bị ghi đè hay xóa bởi bất kì ai, kể cả root.
- Retention mode của object không thể bị thay đổi, không thể bị rút ngắn.
#### Governance
- Đa số người dùng sẽ không có quyền ghi đè hay xóa một object version cũng như không thể thay đổi lock settings của nó.
- Một vài user có quyền đặc biệt sẽ có thể thay đổi retention mode hay thậm chí là xóa object.

Bất kể là ở mode nào, đều phải thiết lập **Rention Period** - khoảng thời gian mà object được bảo vệ, có thể được mở rộng ra.

#### Legal Hold
- Dạng lock đặc biệt, bảo vệ object một cách riêng biệt, không chịu ảnh hưởng của Rentention Mode.
- Có thể tự do đặt và xóa trên một object nếu có quyền IAM `s3:PutObjectLegalHold`.

## VIII) S3 Access Point
- Access Point giúp đơn giản hóa quá trình bảo mật cho S3 Bucket.
- Mỗi Access Point sẽ có:
  - DNS name riêng biệt (Internet Origin hoặc VPC Origin).
  - Một Access Point Policy (Tương tự như bucket policy) - quản lý bảo mật ở phạm vi nhất định.

![img](../images/Screenshot%202025-03-16%20164405.png)

### Access Point - VPC Origin
- Chúng ta có thể khai báo cho một Access Point chỉ có thể được phép truy cập thông qua VPC.
- Cần phải tạo một **VPC Endpoint** để truy cập đến **Access Point** (Gateway hoặc Internet endpoint).
- VPC Endpoint cần phải có Policy cho phép truy cập đến Access Endpoint đích.

![img](../images/Screenshot%202025-03-16%20164832.png)

## IX) S3 Object Lambda
- Sử dụng AWS Lambda Function để thay đổi object trước khi gửi đến chương trình người gọi.
- Chỉ cần dùng một S3 Bucket, nhưng thay vào đó cần sử dụng thêm **S3 Access Point** và **S3 Object Lambda Access Point**.
- Use case:
  - Thay đổi data format, chẳng hạn thay đổi từ định dạng XML sang JSON.
  - Thay đổi kích thước tài nguyên trước khi gửi đến client.
  - Đính kèm watermark bản quyền lên object.