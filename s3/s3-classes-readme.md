## Các lớp S3 khác nhau

![image](../images/Screenshot%202025-02-24%20181257.png)

### S3 Express One Zone

- Lưu trữ hiệu năng cao cho dữ liệu được truy cập thường xuyên nhất.
- Độ trễ yêu cầu nhất quán chưa đến 10 mili giây.
- Cải thiện tốc độ truy cập gấp 10 lần và giảm 50% chi phí yêu cầu so với S3 Standard.
- Hiệu năng cao.

### S3 Standard

- Tính sẵn sàng cao và bền vững, dữ liệu được lưu trữ dự phòng trong nhiều datacenter (>= 3 AZs).
- Được thiết kế cho việc thường xuyên truy cập
- Là lớp mặc định của S3.
- Các trường hợp lưu trữ bao gồm: Website, phân phối nội dung, các ứng dụng điện thoại, trò chơi và big data.

### S3 Standard - Infrequent Access

- Sử dụng cho loại dữ liệu ít được truy cập thường xuyên.
- Nhưng khi truy cập thì yêu cầu tốc độ truy xuất nhanh.
- Có giá và phí lưu trữ trên mỗi GB truy xuất thấp.
- Backup dữ liệu lâu dài.
- Lưu trữ đề phòng mất dữ liệu khi có thảm họa xảy ra.

### S3 One Zone - Infrequent Access

Giống S3 Standard-IA, nhưng dữ liệu chỉ được lưu trữ trên một AZ duy nhất.

### S3 Intelligent

- Tự động giảm chi phí lưu trữ của bạn bằng cách tự động di chuyển dữ liệu sang bậc truy cập tiết kiệm chi phí nhất dựa trên tần suất truy cập.
- Dùng cho loại dữ liệu không dự đoán được tần suất truy cập.

### S3 Glacier - Instant Retrieval

Cung cấp lưu trữ dài hạn với thời gian lấy lại dữ liệu ngay.

### S3 Glacier - Flexible Retrieval

- Không đòi hỏi truy cập ngay lập tức.
- Nhưng cần sự linh hoạt để lấy dữ liệu lớn mà không mất chi phí, như trường hợp cần backup hoặc hồi phục dữ liệu sau thảm họa.

### S3 Glacier - Deep Retrieval

- Rẻ nhất.
- Lưu trữ dữ liệu trong 7 - 10 năm hoặc lâu hơn. 
- Tiêu chuẩn thời gian lấy lại dữ liệu trong 12 giờ, nếu truy xuất dữ liệu lớn là 48 giờ.

### Bảng thống kê loại S3 theo nhu cầu sử dụng

|Nhu cầu sử dụng | Loại|
|-------|-----|
|Đa dụng| S3 Standard|
|Hiệu năng cao|S3 Express One Zone|
|Truy cập không thường xuyên|S3 Standard-IA, S3 OneZone-IA|
|Lưu trữ|Các lớp S3 Glacier|
