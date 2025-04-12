# Lambda Snapstart
- Là tính năng giúp cho việc thực thi hàm nhanh hơn gấp 10 lần với đới Java 11 trở lên.
- Khi tính năng này được bật, hàm được gọi từ trạng thái "được khởi tạo trước" (không cần phải khởi tạo hàm).
- Khi chúng ta xuất bản một phiên bản mới:
    - Lambda khởi tạo hàm.
    - Lưu trữ lại một bản snapshot của hàm, bộ nhớ và trạng thái ổ đĩa.
    - Bản snapshot này được cache để có thể truy cập với độ trễ thấp.
