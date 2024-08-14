# Ghi chú cho bản thân

## 1. Giới thiệu về Cloud Computing

### Cloud Computing là gì?

- Cloud Computing là một mô hình cung cấp các dịch vụ tính toán, lưu trữ, mạng và ứng dụng thông qua mạng Internet. Thay vì phải tự quản lý và vận hành cơ sở hạ tầng máy chủ và hệ thống csdl, người dùng có thể thuê các tài nguyên máy chủ và lưu trữ từ các nhà cung cấp dịch vụ đám mây (Cloud Service Provider) và truy cập chúng thông qua Internet.
- Mô hình đám mây cung cấp cho người dùng sự linh hoạt và khả năng mở rộng dễ dàng, do đó giúp họ tiết kiệm chi phí và tối đa hóa hiệu quả hoạt động. Ngoài ra đám mây cũng cung cấp các dịch vụ về bảo mật và sao lưu dữ liệu trong trường hợp sự cố. Các ví dụ bao gồm: Amazon Web Services, Microsoft Azure, Digital Ocean và Google Cloud Platform.

### Phân biệt các loại hình Cloud

- On-Premise: hệ thống mà được cài đặt và vận hành trên nền tảng phần cứng và hạ tầng mạng nội bộ của tổ chức hoặc doanh nghiệp. Nói cách khác, "on-premise" đề cập đến việc triển khai và sử dụng hệ thống trên cơ sở vật chất của riêng mình, không phải trên môi trường Cloud hay máy chủ của bên thứ ba. Hệ thống On-premise được quản lý và bảo trì bởi đội ngũ IT của tổ chức đó.
  > Nghĩa là chúng ta sở hữu phần cứng, mua các thiết bị về mạng và tự xây dựng hạ tầng.
- Public Cloud: Đây là loại hình Cloud mà tài nguyên máy chủ và dịch vụ được cung cấp cho khách hàng từ một Cloud Provider. Khách hàng sử dụng tài nguyên đó thông qua Internet và trả tiền cho nhà cung cấp dịch vụ đám mây theo mô hình on-demand. Ví dụ cho public cloud là AWS, Azure, GCP.
- Private Cloud: Ngược lại với public cloud, đây là loại hình xây dựng riêng cho một tổ chức hoặc doanh nghiệp. Tài nguyên chỉ available cho các người dùng được ủy quyền. Private Cloud có thể được triển khai trên cơ sở hạ tầng của công ty hoặc trên các dịch vụ đám mây của các cloud provider, nhưng mô hình này thường có giá thành cao hơn nếu so với Public Cloud.
  > Tuy Amazon là Public Cloud, nhưng họ cho phép chúng ta thuê server phần cứng của họ và triển khai dự án. Họ sẽ cam kết các phần cứng này sẽ được đặt ở một vị trí nào đó.
- Hybrid Cloud: Đây là loại hình đám mây kết hợp giữa Public Cloud và Private Cloud (hoặc On-premise). Tổ chức có thể sử dụng Public Cloud để đáp ứng các nhu cầu tài nguyên động và sử dụng Private Cloud để đáp ứng các nhu cầu an ninh và quản lý. Mô hình này giúp tổ chức tối ưu hóa sự linh hoạt và tiết kiệm chi phí, đồng thời đảm bảo an ninh và tuân thủ quy định của chính phủ hoặc tiêu chuẩn ngành.

- Multi cloud: Sử dụng kết hợp nhiều hơn một Cloud Provider. Do đặc thù thế mạnh khác nhau của các provider, việc sử dụng kết hợp nhiều hơn một provider sẽ giúp khai thác tối đa thế mạnh của các cloud.

### Phân biệt IaaS, PaaS, SaaS

**1. Infrastructure as a Service (IaaS)** - Cơ sở hạ tầng như dịch vụ: IaaS cung cấp tài nguyên cơ bản của máy chủ và mạng để khách hàng có thể tự quản lý các ứng dụng và dữ liệu của họ trên đó. Khách hàng sử dụng IaaS để thuê các tài nguyên như Server, Storage, Networking, Security và quản lý nó như một nền tảng hạ tầng của riêng mình.

> Các tài nguyên này là tài nguyên ảo, chúng ta sẽ phải tự chịu trách nhiệm cho các con Server, Storage, Networking về mặt cấu hình.

**2. Platform as a Service (PaaS)** - Nền tảng dịch vụ: PaaS cung cấp một môi trường thực thi ứng dụng đầy đủ, bao gồm các dịch vụ phát triển ứng dụng, cơ sở dữ liệu và hệ thống mạng. PaaS cho phép khách hàng xây dựng, phát triển và triển khai các ứng dụng của họ trên nền tảng của một nhà cung cấp dịch vụ đám mây. Ví dụ cho PaaS bao gồm Microsoft Azure App Service, Google App Engine và Heroku.

> Với loại hình này, chúng ta có thể nhanh chóng deploy ứng dụng lên trên đó. Hầu hết khái niệm về ảo hóa như Server, Database đều đã được abstract, chúng ta chỉ tập trung vào việc phát triển ứng dụng.

**3. Software as a Service (SaaS)** - Phần mềm dưới dạng dịch vụ: SaaS cung cấp các ứng dụng đã được xây dựng và triển khai sẵn trên đám mây để khách hàng sử dụng thông qua Internet. Người dùng không cần phải quản lý hoặc bảo trì các ứng dụng đó, mà chỉ cần truy cập vào chúng thông qua một giao diện web hoặc ứng dụng di động. Ví dụ cho SaaS bao gồm Google Workspace, Microsoft Office 365, ...

Về cơ bản, AWS được xem như là một IaaS, tuy nhiên một số dịch vụ đặc biệt của nó thì hoạt động như PaaS hoặc SaaS. Ví dụ:

- EC2, S3, VPC được coi như là IaaS.
- Elastic Beanstalk, Lambda được coi như PaaS.
- Simple Email Service (SES) và Amazon WorkMail được coi như SaaS.

### So sánh Cloud và các dịch vụ Hosting

| Tiêu chí so sánh         | CloudProvider                                                              | Hosting Service                                                                             |
| ------------------------ | -------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------- |
| Pricing model            | On-demand. Trả tiền cho những gì mình sử dụng. Không cần cam kết trả trước | Cần hợp đồng thuê trước server theo cấu hình. VD thuê 1 server 1 CPU, 2GB RAM trong 3 tháng |
| Linh hoạt trong cấu hình | Thay đổi cấu hình tài nguyên một cách dễ dàng và nhanh chóng.              | Cần có sự can thiệp của bên provider, có thể cần thay đổi hợp đồng.                         |
| Khả năng scale           | Dễ dàng tăng/giảm số lượng tài nguyên khi cần để đáp ứng nhu cầu workload  | Gần như không thể tăng/giảm tài nguyên một cách tùy ý.                                      |
| Số lượng dịch vụ         | Đa dạng nhiều dịch vụ.                                                     | Cung cấp các dịch vụ cơ bản như Virtual server, Database, Storage,                          |
