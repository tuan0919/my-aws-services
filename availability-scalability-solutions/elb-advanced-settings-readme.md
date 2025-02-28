## Một số thiết lập nâng cao của ELB

### Sticky Session (Session Affinity)

Cho phép một client luôn luôn được redirect đến một instance cụ thể nằm sau load balancer. 

Đối với mỗi request, ELB sẽ sử dụng cookie để nhận diện mỗi user khi họ request đến, điều này cho phép user không bị mất "session" của mình sau khi request đến một server.

Thiết lập này có thể được áp dụng cho CLB, ALB và NLB.

Lưu ý là việc áp dụng sticky session có thể làm mất cân bằng trong Load Balancer.

![img](../images/Screenshot%202025-03-01%20001029.png)

### Cross-Zone Load Balancing

Tùy chọn này cho phép ELB phân phối traffic cho các instance kể cả khi chúng khác AZ (Cross-Zone).

![img](../images/Screenshot%202025-03-01%20002934.png)

**ALB**
- Mặc định bật (có thể tắt ở cấp độ Target Group).
- Không tốn phí cho inter AZ.

**NLB & GWLB**
- Mặc định tắt.
- Trả phí nếu sử dụng.

### SSL Certificates

#### SSL / TLS Basic

Chứng chỉ SSL cho phép traffic giữa client và load balancer được mã hóa trong quá trình truyền tải (in-flight encryption).

SSL - viết tắt của Secure Socket Layer, đã từng dùng để mã hóa kết nối.

TLS - viết tắt của Transport Layer Security, là phiên bản mới hơn

Ngày nay, người ta dùng TLS là chủ yếu nhưng **vẫn sử dụng thuật ngữ SSL** để chỉ quá trình này.

Các chứng chỉ public SSL sẽ chỉ được cấp bởi các cơ quan có thẩm quyền - Certificate Authories (CA).
- Comodo, Symantec, GoDaddy, GlobalSign, Digicert, Letsencrypt, ...

Sử dụng public SSL gắn vào ELB sẽ cho phép Load Balancer mã hóa traffic giữa client và Load Balancer.

#### Flow

![img](../images/Screenshot%202025-03-01%20004219.png)

Quy trình như sau:

- User request đến Load Balancer thông qua HTTPS.
- Load Balancer thực hiện quá trình gọi là **SSL Certificate Termination**.
- Tại Back-End, Load Balancer có thể giao tiếp trực tiếp với EC2 bằng cách sử dụng HTTP, nhưng traffic sẽ đi qua VPC (private traffic network) cho nên kết nối vẫn được bảo mật.

Load Balancer sử dụng chứng chỉ X.509.

- Chúng ta có thể quản lý các chứng chỉ thông qua ACM (AWS Certificate Manager).
- Có thể tự upload chứng chỉ của riêng mình để thay thế nếu cần.
- Khi chúng ta thiết lập HTTPS Listener thì:
  - Cần chỉ định một chứng chỉ mặc định.
  - Một danh sách các chứng chỉ để hỗ trợ nhiều domain khác nhau.
  - Sau đó, client có thể sử dụng **SNI (Server Name Indication)** để khai báo hostname mà họ muốn kết nối.

#### Server Name Indication - SNI

SNI giúp giải quyết vấn đề tải nhiều chứng chỉ SSL lên một web server. (để hỗ trợ nhiều website khác nhau).

Là một giao thức mới hơn, yêu cầu client phải chỉ định hostname của server đích sẽ thực hiện SSL handshake.
- Về cơ bản, client sẽ bảo "tôi muốn kết nối đến website xyz" và server sẽ biết nên load chứng chỉ nào cho phù hợp.

Tính năng này chỉ hỗ trợ ALB & NLB cũng như Cloudfront.

![img](../images/Screenshot%202025-03-01%20005547.png)

### Connection Draining / Deregistration Delay

Connection Draining giúp đảm bảo rằng các request hiện tại được xử lý hoàn tất trước khi instance bị loại khỏi target group hoặc bị đánh dấu là unhealthy.

**Cách hoạt động**

- Khi một instance:
  - Bị xóa khỏi target group.
  - Được đưa vào chế độ bảo trì (maintenance).
  - Bị đánh dấu là không khỏe mạnh trong quá trình kiểm tra sức khỏe (Health Check).
-  Connection Draining cho phép load balancer tiếp tục chuyển các request hiện tại đến instance đó cho đến khi các request này được xử lý xong hoặc hết thời gian timeout.

**Ví dụ**
1. Một instance đang phục vụ 10 request.
2. Instance đó bị đánh dấu là unhealthy hoặc chuẩn bị được xóa.
3. Connection Draining giúp 10 request hiện tại được xử lý hoàn tất trước khi load balancer không gửi thêm request mới.

![img](../images/Screenshot%202025-03-01%20010319.png)