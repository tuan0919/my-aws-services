## Amazon RDS Proxy

- Là dịch vụ được quản lý hoàn toàn bởi AWS.
- Tối ưu hóa các kết nối giữa ứng dụng và RDS / Aurora.
- Cải thiện tính sẵn sàng, khả năng mở rộng và hiệu suất của ứng dụng.
- Gần như không yêu cầu thay đổi code trong chương trình.


### Tại sao cần Proxy
Trong các ứng dụng hiện đại, đặc biệt là serverless hoặc microservices, việc quản lý kết nối database có thể gây ra các vấn đề như:

- Số lượng kết nối đồng thời lớn (Connection Pooling).
- Thời gian phục hồi lâu khi failover.
- Cơ sở dữ liệu quá tải khi có quá nhiều kết nối mở cùng lúc.

### Cách hoạt động
RDS Proxy hoạt động như một lớp trung gian giữa ứng dụng và cơ sở dữ liệu, thực hiện các nhiệm vụ:
- Connection Pooling: Gom các kết nối vào một nhóm dùng chung, giảm tải cho cơ sở dữ liệu.
- Connection Multiplexing: Tái sử dụng các kết nối có sẵn thay vì mở kết nối mới.
- Automatic Failover: Tự động chuyển đổi kết nối sang phiên bản standby khi có sự cố.
- IAM Authentication: Tích hợp xác thực với AWS IAM.
- Encryption: Hỗ trợ mã hóa SSL trong quá trình truyền tải.

Lưu ý: RDS Proxy **không bao giờ** có thể được truy cập từ bên ngoài, mà luôn luôn phải truy cập từ VPC (nội bộ bên trong).

Ví dụ: hệ thống có hiện thực một số chức năng bằng cách sử dụng **AWS Lambda Function**:

- Dịch vụ này về cơ bản sẽ tạo và destroy instance liên tục mỗi khi có request.
- Nếu Lambda Function mở kết nối đến RDS / Aurora để hoàn thành request, một Lambda Function sẽ cần mở một request đến RDS/Aurora.
- Giả sử có rất nhiều request đồng thời => nhiều Lambda instance xuất hiện đồng thời => nhiều connection được mở cùng một lúc.
- Trong trường hợp này, nên thiết lập một Proxy để cho các Lambda instance kết nối đến RDS, từ đó hạn chế số lượng connection mở ra đồng thời hay tái sử dụng được connection đang trống thay vì mở ra connection mới.

![img](../images/Screenshot%202025-03-04%20205722.png)