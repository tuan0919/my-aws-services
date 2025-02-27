## AMI

- AMI = Amazon Machine Image.
- AMI là một bản cài đặt của EC2:

  - Có thể được cài thêm trước các phần mềm, hệ điều hành, vv...
  - Khởi động nhanh hơn bởi vì các phần mềm được đóng gói sẵn từ trước.

- AMI bị giới hạn trong một region cụ thể (nhưng có thể sao chép qua nhiều region).
- Chúng ta có thể tạo EC2 instance từ:

  - Public AMI: do AWS cung cấp.
  - AMI tự custom: do chúng ta tự custom và bảo trì.
  - Một bản AMI được bán trên AWS AMI Marketplace.

## AMI Process
- Tạo một EC2 instance và custom nó lại.
- Stop instance (để đồng bộ data).
- Tạo một AMI - điều này cũng đồng thời tạo ra một [EBS Snapshot](./ebs-introduction-readme.md#esb-snapshot).
