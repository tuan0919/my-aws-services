
# Một số giới hạn của AWS Lambda
- Về quá trình chạy:
    - Cấp phát bộ nhớ: 128MB - 10GB. (Mỗi lần tăng 1MB)
    - Thời gian chạy tối đa là 900 giây hay 15 phút.
    - 4KB lưu trữ cho biến môi trường.
    - Dung lượng đĩa trong "function container" (cụ thể là ở /tmp) là 512MB - 10GB.
    - 1000 tính toán đồng thời (có thể tăng lên nếu muốn)
- Về việc triển khai:
    - Kích thước để triển khai lambda function khi nén thành file .zip là 50MB.
    - Kích thước để triển khai lambda function khi giải nén là 250MB.
    - Có thể sử dụng thư mục /tmp để tải một số file khác khi khởi động.
    - 4KB cho biến môi trường.