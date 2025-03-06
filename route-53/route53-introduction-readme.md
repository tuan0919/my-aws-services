## Route 53
AWS Route 53 là dịch vụ DNS do AWS cung cấp, giúp quản lý các tên miền, định tuyến lưu lượng mạng và kiểm tra sức khỏe hệ thống.

### Cách hoạt động
- Người dùng truy cập vào tên miền (ví dụ: example.com).
- Trình duyệt gửi request đến máy chủ DNS.
- Route 53 trả về địa chỉ IP của server tương ứng.
- Trình duyệt kết nối đến server để lấy dữ liệu.

![img](../images/Screenshot%202025-03-06%20210649.png)

### Records
Các bản ghi sẽ giúp chúng ta định nghĩa cách để định tuyến traffic đến một tên miền cụ thể nào đó.

Mỗi bản ghi chứa các thông tin sau:
- Domain / Subdomain Name.
- Loại bản ghi.
- Địa chỉ IP.
- Routing Policy - cách mà Route 53 sẽ truy vấn tên miền này.
- TTL - thời gian mà bản ghi sẽ được cache tại DNS Resolver.

Các loại bản ghi:
- (phải biết) A / AAAA / CNAME / NS.
- (nâng cao) CAA / DS / MX / NAPTR / PTR / SOA / TXT / SPF / SRV.

- **A** - map hostname thành IPv4.
- **AAAA** - map hostname thành IPv6.
- **CNAME** - map hostname thành một hostname khác.
  - Hostname đích là loại bản ghi A hoặc AAAA.
  - Không thể tạo CNAME cho DNS namespace đầu tiên (Zone Apex), ví dụ: có thể tạo CNAME cho example.com nhưng không thể tạo CNAME cho www.example.com.
- **NS** - Name server của Hosted Zone.
  - Điều chỉnh cách mà traffic được điều hướng đến một domain.

### Hosted Zone
Là một container chứa các bản ghi khác nhau để định hướng traffic đến một domain và subdomain nào đó.

Có hai loại Hosted Zone:
- **Public Hosted Zone** - chứa các bản ghi sẽ định hướng traffic trên Internet (public domain name).
  - Ví dụ: application1.mypublicdomain.com
- **Private Hosted Zone** - chứa các bản ghi sẽ định hướng traffic bên trong một hoặc nhiều VPCs (private domain name).
  - Ví dụ: application1.company.internal

Về cơ bản, Private Hosted Zone và Public Hosted Zone hoạt động giống hệt nhau, chỉ là một bên sẽ là dành cho các domain public trên internet còn một bên là dành cho các domain private để sử dụng nội bộ.

Chúng ta cần trả 0.5$ mỗi tháng cho mỗi Hosted Zone.

![img](../images/Screenshot%202025-03-06%20212716.png)
