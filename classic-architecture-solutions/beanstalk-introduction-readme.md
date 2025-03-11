## Vấn đề khi phát triển ứng dụng trên AWS
Developer khi muốn phát triển hệ thống trên AWS thường phải:
- Quản lý cơ sở hạ tầng.
- Deploy code.
- Cài đặt database, Load Balancer, ...
- Các vấn đề liên quan đến mở rộng ứng dụng.

Trong khi đó, hầu hết các ứng dụng web đều có chung cơ sở hạ tầng bên dưới. Developer chỉ nên quan tâm đến việc chạy code của mình.

## Elastic Beanstalk 
- Elastic Beanstalk là một trung tâm để theo dõi quá trình deploy một ứng dụng trên AWS.
- Từ một giao diện duy nhất, Beanstalk sẽ tái sử dụng toàn bộ các thành phần phổ biến khác như EC2, ASG, ELB, RDS, ...
- Là một service được quản lý sẵn:
  - Tự động xử lý load balancing, scaling, theo dõi sức khỏe cho hệ thống, cài đặt instance, ...
  - Nhiệm vụ của Developer chỉ là phần code sẽ chạy trong hệ thống.
- Người dùng vẫn có toàn quyền chỉnh sửa lại nếu muốn.
- Các thành phần được tập trung tại một giao diện duy nhất để tiện quản lý.
- Beanstalk miễn phí, nhưng các service bên dưới nó vẫn phải trả phí nếu có.

### Các thành phần trong Beanstalk
- **Application**: Tập hợp các thành phần của Elastic Beanstalk (enviroments, version, configuration, ...)
- **Application version**: phiên bản của chương trình hiện tại.
- **Enviroment**:
  - Tập hợp các tài nguyên AWS đang chạy phiên bản hiện tại của ứng dụng (chỉ được có 1 phiên bản tại một thời điểm).
  - **Tiers**: Web Server Enviroment Tier và Worker Enviroment Tier.
  - Chúng ta có thể tạo nhiều môi trường (dev, test, prod, ...)

### Web Server Tier vs. Worker Tier

**Web Server** - Có cấu trúc mà chúng ta đã quen thuộc, bao gồm:
- Một ELB sẽ gửi traffic đến ASG.
- Bên trong ASG sẽ có nhiều EC2 instance.

**Worker** - Client không truy cập trực tiếp, bao gồm:
- Một SQS Queue đóng vai trò là message queue.
- Các EC2 instance sẽ đóng vai trò worker, pull các message từ SQS để xử lý.

![img](../images/Screenshot%202025-03-11%20133957.png)