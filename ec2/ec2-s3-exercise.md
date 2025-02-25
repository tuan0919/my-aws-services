## Bài thực hành cấu hình IAM role cho máy chủ ảo hóa EC2 - 01
### Yêu cầu
- Tạo 4 bucket trong S3 và upload file vào 4 bucket này.
- Chỉ cấp quyền cho EC2 instance đc phép truy cập vào 2 trong số 4 bucket.
- Không đăng nhập dưới tư cách người dùng có thẩm quyền, làm sao để EC2 có thể tương tác được với 2 bucket vừa chọn.
### Cách làm
1. Tạo 4 bucket `nqat0919-devcom-01`; `nqat0919-devcom-02`; `nqat0919-devcom-03`; `nqat0919-devcom-04`.
2. Tạo một Policy **S3_Custom_Read_Access** với nội dung cho phép list file và list vị trí bucket cho hai bucket `03` và `04`

```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "AllowUserToSeeBucketListInTheConsole",
            "Action": [
                "s3:ListAllMyBuckets",
                "s3:GetBucketLocation"
            ],
            "Effect": "Allow",
            "Resource": [
                "arn:aws:s3:::*"
            ]
        },
        {
            "Effect": "Allow",
            "Action": [
                "s3:Get*",
                "s3:List*"
            ],
            "Resource": [
                "arn:aws:s3:::nqat0919-devcom-03",
                "arn:aws:s3:::nqat0919-devcom-04"
            ]
        }
    ]
}
```
3. Tạo role **S3_Custom_Read_Access_Role** rồi gắn policy **S3_Custom_Read_Access** vừa tạo vào role này.
4. Gắn **S3_Custom_Read_Access_Role** cho EC2.

Giờ đây, EC2 có quyền list tất cả file bên trong bucket 03 và 04 mà không cần phải đăng nhập bằng một user có quyền vs các bucket này.
