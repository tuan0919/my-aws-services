## Route 53 - Routing Policies

Routing Policy sẽ dùng để định nghĩa cách mà Route 53 phản hồi lại với các yêu cầu truy vấn DNS.

Nên phân biệt được từ "routing" trong Route 53, không giống như Load Balancer, Route 53 không định hướng traffic, mà chỉ phản hồi lại yêu cầu truy vấn DNS.

Hiện tại, Route 53 hỗ trợ các loại policy sau:

- Simple.
- Weighted.
- Failover.
- Latency based.
- Geolocation.
- Multi-value answer.
- Geoproximity.

## Simple Routing

Route traffic đến một resource nào đó, có thể khai báo nhiều giá trị cho cùng một bản ghi, trong trường hợp này thì phía client sẽ **chọn ngẫu nhiên** một trong số nhiều bản ghi đó.

Ngoài ra, Simple Routing **không thể kết hợp** với Health Check.

## Weighted Routing

Route traffic đến các resource theo một tỉ lệ hay trọng số (weight) nào đó, các DNS records phải có cùng tên và loại

Weighted Routing hỗ trợ Health Check.