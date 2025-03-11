## Amazon S3 Introduction
### Bucket
S3 cho phép người dùng lưu trữ file (object) trong các "bucket". Tên của bucket phải là độc nhất trên phạm vi toàn cầu (trên toàn bộ các region), nhưng phạm vi hoạt động của một bucket thì chỉ là trong một region.
### Object
Object trong S3 là các file sẽ được lưu trữ, mỗi file sẽ có một Key.

Key là đường dẫn tuyệt đối đến tài nguyên đó:
 - s3://my-bucket/my_file.txt
 - s3://my-bucket/my_folder_1/another_folder/my_file.txt

Giá trị của một object là content chứa trong body của file được upload:
- Object size tối đa được upload là 5TB (5000 GB).
- Nếu file upload lớn hơn 5GB, cần phải sử dụng "multi-part upload".

Ngoài ra một Object còn có các thông tin như:
- Metadata (một cặp các key / value do hệ thống hoặc người dùng thiết lập).
- Tags. 
- Version ID (nếu versioning được bật).

## Amazon S3 Security
Có vài cách để thiết lập bảo mật cho một Amazon S3:
- **User-based**:
  - **IAM Policies** - Cho phép chỉ định một user cụ thể được phép dùng một API call nào đó bằng IAM.
- **Resource-based**:
  - **Bucket Policies** - Một JSON policy gán trực tiếp cho một S3 bucket để kiểm soát quyền truy cập đến bucket và các object bên trong.
  - **Object Access Control List (ACL)** - Kiểm soát quyền truy cập ở cấp độ object.
  - **Bucket Access Control List (ACL)** - Kiểm soát quyền truy cập ở cấp độ bucket. Ít phổ biến hơn.

>**Chú ý**: Một IAM principal có thể truy cập S3 Object nếu:
>- User IAM permisson cho phép HOẶC Resource policy cho phép.
>- VÀ không có DENY cụ thể nào.

- **Encryption**: có thể mã hóa object trong S3 bằng cách sử dụng một encryption key.

### S3 Bucket Policies
Là Policy được viết ở dạng JSON, ví dụ:

```js
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "PublicReadGetObject",
      "Effect": "Allow",
      "Principal": "*",
      "Action": "s3:GetObject",
      "Resource": "arn:aws:s3:::my-public-bucket/*"
    }
  ]
}
```
- `Resource:` bucket và object.
- `Effect:` Allow hoặc Deny.
- `Action:` Một tập các API call sẽ bị tác động.
- `Principal:` Tài khoản hoặc người dùng mà policy sẽ tác động đến.

Chúng ta sử dụng Bucket policy khi:
- Cấp public access đến bucket.
- Bắt buộc object cần phải bị mã hóa khi upload.
- Cấp access cho một account khác.
