## Amazon ElastiCache

Là dịch vụ lưu trữ dữ liệu trong bộ nhớ (in-memory) được quản lý bởi AWS, giúp tăng tốc hiệu suất của các ứng dụng bằng cách lưu trữ tạm thời (cache) các dữ liệu thường xuyên truy cập.

- Cung cấp hai loại engine phổ biến: **Redis** và **Memcached**.
- Giúp xây dựng chương trình theo hướng stateless bằng cách lưu trữ dữ liệu của session vào bên trong ElastiCache.
- AWS sẽ đảm nhiệm bảo trì OS, vá lỗi, tối ưu hóa, backup, ...

**Lưu ý**: sử dụng ElastiCache trên chương trình đã xây dựng sẵn sẽ yêu cầu thay đổi nhiều về code.

## Một số giải pháp kiến trúc sử dụng ElastiCache

Ví dụ 1: 

Sử dụng ElastiCache để lưu trữ các dữ liệu thường xuyên truy cập (caching dữ liệu). 

- Khi chương trình query ElastiCache, nếu dữ liệu không tồn tại thì mới query đến RDS, sau đó ghi dữ liệu mới vào ElastiCache.
- Giúp giảm tải cho RDS.
- Bộ nhớ cache cần phải có một chiến lược invalidate nào đó để đảm bảo chỉ data mới nhất mới nằm trong cache.

![img](../images/Screenshot%202025-03-05%20202334.png)

Ví dụ 2:

Sử dụng ElastiCache để lưu trữ session data, cho phép thiết kế chương trình theo hướng stateless.

- Khi người dùng đăng nhập vào chương trình, lấy dữ liệu bên trong session của họ lưu trữ vào ElastiCache.

- Khi người dùng bị re-direct sang một instance khác của chương trình, instance đó sẽ lấy data session từ ElastiCache và vẫn duy trì được trạng thái đăng nhập của họ.

![img](../images/Screenshot%202025-03-05%20204203.png)

## Redis vs MemCached

|Tiêu chí| Redis | Memcached |
|--------|-------|-----------|
|Persistent Data|Có (Snapshot, AOF)|Không|
|Multi-threading|Không (single threading)|Có|
|Replication|Hỗ trợ (Primary-Replica)|Không|
|Cluster Support	|Có (Redis Cluster)	|Không|
|Auto Discovery	|Không|	Có|
|TTL (Time-To-Live)|	Có|	Có|
|Encryption|	Hỗ trợ (TLS, Encryption at Rest)|	Không hỗ trợ|
|Use Case|	Session storage, leaderboards, message queue, cache|	Cache đơn giản, phân tán dữ liệu tạm thời|

## Security

- Hỗ trợ IAM Authentication cho Redis.
- Các chính sách IAM trên ElastiCache chỉ dùng để thiết lập bảo mật cho API AWS.
- Redis AUTH:
  - Chúng ta có thể thiết lập "password/token" khi tạo một Redis cluster.
  - Đây là một lớp bảo mật được thêm vào cho bộ nhớ cache bên cạnh security group.
  - Hỗ trợ inflight encryption với SSL.
- Memcached:
  - Hỗ trợ SASL-based authentication. (nâng cao)