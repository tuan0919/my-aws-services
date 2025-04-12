
## Lambda trong VPC

Theo mặc định, Lambda sẽ được khởi động bên ngoài VPC của chúng ta, nhưng vẫn sẽ nằm trong VPC của AWS.

Do đó, trong trường hợp này Lambda sẽ không thể truy cập vào các tài nguyên bên trong mạng VPC của chúng ta nếu có (như RDS, EstiCache, ELB nội bộ, ...)

![alt text](image-1.png)

Để có thể sử dụng các tài nguyên này, chúng ta phải khởi động Lambda bên trong VPC bằng cách:
- Khai báo VPC ID, Subnet và Security groups cho Lambda.
- Sau đó, Lambda sẽ tạo ra một ENI (Elastic Network Interface) bên trong subnet đó.
- Và nhờ vậy, nó có thể truy cập đến các tài nguyên bên trong VPC thông qua ENI này.

![alt text](image-2.png)

Trường hợp phổ biến nhất là khi chúng ta sử dụng Lambda với RDS Proxy.
- Việc có RDS Proxy sẽ giúp hệ thống giảm tải số lượng kết nối đồng thời đến RDS bên dưới cũng như cung cấp thêm một lớp bảo mật cho RDS.
- Thế nhưng RDS Proxy thường sẽ nằm trong một VPC nội bộ và KHÔNG public ra ngoài.
- Bằng cách sử dụng ENI như phía trên, chúng ta có thể cho phép Lambda Function phối hợp với RDS Proxy để truy vấn RDS.

![alt text](image-3.png)
