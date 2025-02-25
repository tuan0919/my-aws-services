## Elastic Compute Cloud - EC2

- Giống như một Virtual Machine trong hệ thống datacenter, chỉ là nó chạy trong AWS.
- Được thiết kế để làm web-scale cloud computing dễ dàng sử dụng hơn cho kĩ sư phát triển phần mềm.
- Có thể thay đổi khi cần tăng / giảm dung lượng.
- Chúng ta có toàn quyền kiểm soát máy chủ EC2 của mình.

## Chi phí sử dụng EC2

Có 4 loại chi phí sử dụng EC2 bao gồm:

|Loại|Chi phí|
|---|---|
|On-Demand|Trả tiền tính theo giờ hoặc giây, phụ thuộc vào kiểu instance mà bạn sử dụng|
|Reserved|Trả tiền thuê trong 1 hoặc 3 năm, giảm giá đến 72% cho phí mỗi giờ|
|Spot|Mua dung lượng chưa sử dụng với mức chiết khấu lên đến 90%. Giá cả biến động theo cung và cầu.|
|Dedicated|Một máy chủ EC2 vật lý dành riêng cho bạn sử dụng. Chi phí cao nhất trong tất cả các loại hình|

### On-Demand Instance

- **Linh hoạt**: chi phí thấp và linh hoạt, không cần phải thanh toán trả trước hoặc cam kết sử dụng dài hạn.
- **Ngắn hạn**: dùng cho các ứng dụng có khối lượng công việc ngắn hạn, tăng đột biến không thể đoán trước và không thể gián đoạn trong hoạt động.
- **Testing**: các ứng dụng đang được phát triển và trong quá trình thử nghiệm.

### Reserved Instance

- **Nhu cầu sử dụng dự đoán trước**: các ứng dụng đã chạy ổn định và nhu cầu sử dụng đã được báo trước.
- **Yêu cầu năng lực cụ thể**: đã biết ứng dụng sẽ đòi hỏi nhu cầu dung lượng, cấu hình cụ thể.
- **Trả tiền trước**: trả tiền trước nên được giảm tổng chi phí khi thuê EC2.

### Spot Instance

- Các ứng dụng có khả năng linh hoạt về mặt thời gian và các dữ liệu của ứng dụng không quan trọng.
- Ứng dụng sẵn sàng với việc bị dừng đột ngột & bị mất dữ liệu.

### Dedicated Host

- **Tuân thủ**: khi người dùng cần triển khai hệ thống máy chủ nhưng phải tuân thủ các yêu cầu quy định có thể không hỗ trợ ảo hóa.
- **Bản quyền**: một số phần mềm bản quyền không hỗ trợ multi-tenancy hoặc triển khai trong môi trường cloud.