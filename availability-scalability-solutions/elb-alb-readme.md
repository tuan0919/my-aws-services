## Application Load Balancer

- Hoạt động ở Layer 7 (Application Layer) của mô hình OSI.
- Cân bằng tải HTTP cho các chương trình.
- Hỗ trợ host-based routing, path-based routing.
- Phù hợp cho microservices & container-based application.

![img](../images/Screenshot%202025-02-27%20171630.png)

### Target Groups

Một target group có thể là một tập hợp:

- Instance EC2.
- Task ECS
- Lambda function đơn lẻ.
- IP address khác nhau.

ALB có thể route đến nhiều target group. Health Check được thực hiện ở cấp độ target group.

*Ví dụ - cân bằng tải dựa vào query string*

![img](../images/Screenshot%202025-02-27%20173405.png)

### Client không tương tác trực tiếp với application

Một điểm đáng phải lưu ý khi thực hiện cân bằng tải với ALB là bản thân ALB sẽ gửi request đến service đích chứ không phải client.

- Service sẽ không thấy được IP của client nằm trong request, thay vào đó là IP của Load Balancer.
- IP thực tế của client được đính kèm vào header dưới param `X-Forwarded-For`.
- Port thực tế được đính kèm vào header dưới param `X-Forwarded-Proto`.

![img](../images/Screenshot%202025-02-27%20173931.png)