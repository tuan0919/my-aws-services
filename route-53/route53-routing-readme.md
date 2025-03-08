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

- Route traffic đến một resource nào đó, có thể khai báo nhiều giá trị cho cùng một bản ghi, trong trường hợp này thì phía client sẽ **chọn ngẫu nhiên** một trong số nhiều bản ghi đó.

- **Không thể kết hợp** với Health Check.

## Weighted Routing

- Route traffic đến các resource theo một tỉ lệ hay trọng số (weight) nào đó, các DNS records phải có cùng tên và loại

- Hỗ trợ Health Check.

## Latency-based Routing

Chuyển hướng đến resource có độ trễ ít nhất, hữu ích trong trường hợp muốn ưu tiên độ trễ thấp cho người dùng.

Latency (độ trễ) có thể dựa vào khoảng cách giữa user và AWS region.

Hỗ trợ Health Check.

## Failover Routing (Active - Passive)

Route traffic đến một Resource dự phòng khi resource Primary bị lỗi (failover).

Khi Primary hoạt động lại, traffic sẽ quay trở về nó.

Dựa trên Health Check để hoạt động.

## Geolocation Routing

Khác với Lantency-based, loại Routing này hoạt động dựa trên vị trí của người dùng, cụ thể là vị trí địa lý. Nếu người dùng ở vị trí không được chỉ định thì sẽ được route đến "Default" record.

TH Sử dụng: nội địa hóa cho chương trình, giới hạn phân phối nội dung, cân bằng tải, ...

Có thể kết hợp với Health Check.
