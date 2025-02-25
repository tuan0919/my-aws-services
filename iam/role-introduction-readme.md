## IAM Role
- Role là một loại danh tính có thể được tạo trong IAM và có thể phân quyền cụ thể.
- Role tương tự như một user, như là một AWS identity với các chính sách phân quyền.
- Role dùng để định rõ danh tính (identity) nào có thể hay không truy cập vào một dịch vụ và tài nguyên cụ thể trong AWS.
## Role là tạm thời
- Role không có các thông tin xác thực (credentials) dài hạn tiêu chuẩn giống như password.
- Thay vào đó, khi đảm nhận một role, bạn sẽ được cung cấp một credientials tạm thời cho session của mình.
## Role có thể làm gì khác
- Role có thể được đảm nhận bởi người dùng, kiến trúc AWS hoặc các cấp độ account trong hệ thống.
- Role cho phép khả năng truy cập chéo giữa các account. Cho phép một AWS account này có thể tương tác với tài nguyên của một AWS account khác.