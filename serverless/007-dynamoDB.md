# Amazon DynamoDB
- Là một dịch vụ được quản lý toàn diện, độ sẵn sàng cao với nhiều bản replica trải dài trên nhiều AZ.
- Là cơ sở dữ liệu NoSQL - có hỗ trợ transaction.
- Có thể scale với workload khổng lồ vì dạng database được phân phối sẵn.
- Rất nhanh và ổn định về hiệu năng (1 chữ số mili giây).
- Tích hợp với IAM cho bảo mật, phân quyền và quản trị.
- Không bảo bảo trì hay vá lỗi, luôn luôn có sẵn để sử dụng.
- Chi phí thấp với khả năng tự động mở rộng.
- Có hai class table là **Standard** và **Infrequently Access (IA)**.

## Cơ bản
- DynamoDB được cấu thành nên từ các bảng.
- Mỗi bảng có một khóa chính (phải xác định khi tạo bảng).
- Mỗi bảng có thể có vô hạn item (bản ghi) bên trong nó.
- Mỗi item sẽ có nhiều thuộc tính (có thể thay đổi theo thời gian và cũng có thể null).
- Kích thước tối đa của item là 400KB.
- Kiểu dữ liệu được hỗ trợ:
    - Kiểu nguyên thủy - String, Number, Binary, Boolean, Null.
    - Kiểu document - List, Map.
    - Kiểu set - String Set, Number Set, Binary Set.
- Vì thế nên, trong DynamoDB bạn có thể liên tục thay đổi schema của nó.

## Read/Write Capacity Mode
- Chúng ta có thể kiểm soát capacity của bảng (thay đổi throughput của read/write).
- Provisioned Mode (Mặc định)
    - Chúng ta chỉ định rõ bao nhiêu read/write mỗi giây mà mình cần.
    - Chúng ta phải dự liệu capacity từ trước.
    - Trả tiền dựa theo Read Capacity Unit (RCU) và Write Capacity Unit (WCU) đã dự tính.
    - Có thể thêm chế độ auto-scaling để thay đổi RCU và WCU.
- On-Demand Mode
    - Read/Write Capacity tự động scale theo workload của bạn.
    - Không cần dự tính trước capacity sẽ sử dụng.
    - Trả chính xác theo những gì mà bạn sử dụng, sẽ đắt đỏ hơn.