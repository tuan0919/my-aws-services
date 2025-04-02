# Amazon ECS
- ECS là viết tắt cho cụm từ **Elastic Container Service**
- Việc khởi động một Docker Container trên AWS nghĩa là khởi động một task ECS trên cụm ECS.

## Khởi động theo kiểu EC2

Chúng ta sẽ cần phải ước lượng và bảo trì hạ tầng (mà cụ thể là các EC2 instance).

- Mỗi EC2 Instance sẽ có một ECS Agent chạy bên trong nó và sẽ đăng ký với ECS.
- AWS lúc này sẽ quản lý việc khởi động / tắt các container bên trong EC2.

![img](../images/image.png)

## Khởi động theo kiểu Fargate

- Khởi động Docker container trên AWS.
- Chúng ta không cần phải biết truớc hạ tầng (vì sẽ không chạy trên EC2).
- Serverless.
- Chúng ta chỉ cần đơn giản là đưa một image và AWS sẽ tự động chạy container với CPU / RAM mà chúng ta cần.
- Để scale thì chỉ đơn giản là tăng thêm số lượng task.

![alt text](image.png)

## IAM Role cho ECS

- IAM Role cho bản thân EC2 Instance (đối với loại khởi động bằng EC2):

  - Sẽ được sử dụng bởi ECS agent bên trong EC2.
  - Có thể gọi API đến các dịch vụ ECS khác.
  - Gửi logs của container đến CloudWatch Logs.
  - Pull Docker Image từ ECR.

- IAM Role cho mỗi Task ECS:
  - Cho phép mỗi taks có một role cụ thể.
  - Cho phép chung ta sử dụng nhiều role khác nhau cho các dịch vụ ECS2 khác nhau.
  - Task Role sẽ được định nghĩa tại task definition.

![alt text](image-1.png)

## Tích hợp Load Balancer

ECS và Fargate có thể tích hợp thoải mái với ALB trong hầu hết các trường hợp.

Ngoài ra còn có thể tích hợp với NLB, nhưng chỉ khuyến khích khi chúng ta cần throughput cao / hiệu suất cao.

## Data Volumes (EFS) trên ECS

- Chúng ta có thể mount EFS file system vào ECS task.
- Hỗ trợ cho cả hai loại khởi động EC2 và Fargate.
- Các task đang chạy ở nhiều AZ khác nhau sẽ chia sẻ dữ liệu bên trong EFS file system.
- Fargate + EFS = Serverless.
- TH Sử dụng: cung cấp một nơi lưu trữ đa vùng bền vững cho các container.
- Lưu ý: Amazon S3 không thể được mount như file system.


