## Stateful Web app: MyClothes.com
- MyClothes.com cho phép người dùng mua quần áo trực tuyến.
- Có shopping cart.
- Phục vụ đến hàng trăm người dùng đồng thời.
- Cần duy trì và mở rộng theo chiều ngang.
- Giữ cho web application stateless nhất có thể.
- Người dùng không mất dữ liệu trong shopping cart.
- Người dùng có thông tin chi tiết (địa chỉ nhà, họ tên, vv) bên trong database.

### Giải pháp 1
**Ý tưởng**:
- Cài đặt Stickiness Session tại ELB, điều này đảm bảo session của khách hàng sẽ được duy trì bằng cách chuyển hướng traffic của đến đúng instance mà session được tạo ra.
- Các instance được đặt trong một ASG để có thể mở rộng dễ dàng.
- Có một Route 53 để quản lý DNS cho tên miền.

![img](../images/Screenshot%202025-03-09%20175323.png)

**Vấn đề gặp phải**:
- Nếu instance bị down, session vẫn sẽ mất.

### Giải pháp 2
**Ý tưởng**:
- Thử thay đổi dữ liệu của shopping cart nằm tại web cookie của client.
- Khi client gửi request, sẽ gửi đồng thời cả cookie chứa dữ liệu shopping cart.
- Hệ thống sẽ dựa vào dữ liệu này để tái tạo lại dữ liệu của giỏ hàng.
- Với cách tiếp cận này, hệ thống không cần đến session vì dữ liệu của mỗi user sẽ nằm tại web cookie của họ => stateless application.

![img](../images/Screenshot%202025-03-09%20180837.png)

**Vấn đề gặp phải**:
- HTTP Request nặng nề hơn do chứa cả dữ liệu giỏ hàng.
- Rủi ro về bảo mật (cookie có thể bị thay đổi).
- Server cần có thêm một lớp bảo mật để xác minh dữ liệu cookie người dùng.
- Cookie không nên có kích thước quá lớn, thường thì không quá 4KB.

### Giải pháp 3
**Ý tưởng**:
- Thay về gửi toàn bộ dữ liệu session (trong trường hợp này là dữ liệu về toàn bộ giỏ hàng), chúng ta chỉ gửi session_id vào Web Cookies người dùng.
- Sử dụng thêm dịch vụ ElastiCache.
- EC2 instance sẽ lưu và truy vấn session data tương ứng với session_id ở ElastiCache.

![img](../images/Screenshot%202025-03-09%20181524.png)

**Vấn đề gặp phải**:
- Hệ thống chưa giải quyết được vấn đề lưu thông tin cá nhân người dùng.

### Giải pháp 4
**Ý tưởng**:
- Các dữ liệu cá nhân người dùng sẽ được lưu trữ tại RDS instance.
- Vì hệ thống của hàng trăm người dùng đồng thời, và có khả năng sẽ mở rộng trong tương lai, chúng ta sẽ xây dựng một RDS Master instance và nhiều RDS Replica để tăng hiệu suất đọc.

![img](../images/Screenshot%202025-03-09%20182934.png)