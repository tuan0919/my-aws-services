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

## 2. Global infrastructure của AWS, giới thiệu các services chính

### Region là gì?

#### Khái niệm

Region là một khái niệm để mô tả một khu vực vật lý trên thế giới àm AWS cung cấp các dịch vụ điện toán đám mây. Mỗi AWS Region là một khu vực độc lập với cơ sở hạ tầng và các dịch vụ.

Mỗi Region sẽ bao gồm nhiều Availability Zone (AZ).

#### Lựa chọn Region

Việc lựa chọn region để triển khai hệ thống dựa trên:

- Tuân thủ theo compliance (tiêu chuẩn ngành, luật pháp v.v)
- Gần người dùng (giảm độ trễ).
- Dịch vụ cần sử dụng có ở region đó hay không?
- Giá cả của các dịch vụ.

### Availability Zone là gì?

Một Availability Zone (AZ) là một trung tâm dữ liệu hoặc một nhóm các trung tâm dữ liệu nằm trong cùng một khu vực vật lý, nhưng được phân bổ và vận hành hoàn toàn độc lập. Mỗi AZ có thể có các tài nguyên đám mây như máy chủ ảo, ổ cứng, network, security, các dịch vụ khác nhau, cùng với các tài nguyên hỗ trợ khác như hệ thống cấp điện.

Việc sử dụng nhiều AZ đảm bảo tính khả dụng cao cho ứng dụng, tăng tính bảo mật và đảm bảo dữ liệu được lưu trữ và xử lý an toàn. Nếu một AZ gặp sự cố hoặc ngừng hoạt động, các tài nguyên đám mây được triển khai tại các AZ khác vẫn có thể hoạt động bình thường, giúp đảm bảo rằng dịch vụ của chúng ta hoạt động một cách liên tục và đáng tin cậy.

Mỗi region của AWS thường sẽ có ít nhất 3 AZs.
VD: ở region Singapore(ap-southeast) sẽ có các zone:

- ap-southeast-1a
- ap-southeast-1b
- ap-southeast-1c
  > Giả sử nếu chúng ta triển khai theo dạng Cluster, chúng ta sẽ chọn nhiều zone thay vì một zone.

Hầu hết các service của AWS đều hỗ trợ triển khai trên Mutli-AZ để đảm bảo nâng cao High Availability của hệ thống.

### Edge Location là gì?

AWS Edge Location là một mạng lưới các điểm phân phối (Point of Present) trên thế giới, nơi các dịch vụ AWS, như Amazon CloudFront và Amazon Route 53, cung cấp các tính năng xử lý và phân phối nội dung (CDN) đến người dùng cuối.

Mỗi Edge Location là một trung tâm dữ liệu nhỏ và được quản lý bởi AWS, có khả năng đáp ứng các yêu cầu địa phương từ các máy khách của người dùng cuối. Edge Locations hoạt động như bộ đệm cho nội dung được phân phối bởi các dịch vụ AWS, giúp giảm thiểu độ trễ và tăng tốc độ truy cập cho người dùng cuối.

## 3. Computing Service - EC2

### Định nghĩa

EC2 là viết tắt của Amazon Elastic Computer Cloud là một service cung cấp tài nguyên server ảo theo yêu cầu.

Khi đối chiếu một số khái niệm giữa EC2 với PC/Laptop truyền thống thì chúng ta có thể dùng bảng dưới đây:

| EC2         | PC/Laptop     |
| ----------- | ------------- |
| RAM         | RAM           |
| CPU         | CPU           |
| GPU         | GPU           |
| EBS Volumes | SSD, HDD, USB |
| VPC/Subnet  | LAN           |
| Snapshot    | Ghost         |

### EC2 thuộc về layer nào

- EC2 là máy chủ ảo chạy trên Hypervisor (Trình ảo hóa) của AWS, bên dưới là các phần cứng
- Về cơ bản người dùng chỉ có thể quản lí EC2 từ cấp độ OS trở lên.
- AWS sẽ không can thiệp vào dữ liệu từ tầng OS trở lên của một EC2.
- Về cơ bản tất cả các EC2 Instance đều hoạt động như một máy chủ độc lập và không thể access nếu như không có quyền.
- Tất cả trách nhiệm từ phía OS đều do người dùng quản lí, AWS không chịu trách nhiệm về bảo mật hay bảo toàn dữ liệu.

![image](images/Screenshot%20from%202024-08-15%2020-30-25.png)

### Một số khái niệm cơ bản của EC2

- **AMI**: Amazon Machine Image. Giống như một file ISO/Ghost chứa toàn bộ thông tin của hệ điều hành. EC2 được khởi động lên từ 1 AMI tương tự như việc cài win lần đầu cho PC/Laptop.
- **EBS Volume**: Ổ cứng ảo hóa được cấp phát dữ liệu bởi Amazon. Chỉ có thể đọc được dữ liệu khi được gắn vào một instance.
- **Snapshot**: Ảnh chụp của một **EBS Volume** tại 1 thời điểm. Có thể sử dụng để phục hồi dữ liệu khi có sự cố.
- **Instance**: 1 Máy chủ ảo được cấp phát tài nguyên, CPU, RAM, GPU, ... tùy theo dòng instance mà sẽ có một số giới hạn nhất định.

### Security Group là gì

Để giới hạn truy cập tới EC2 và từ EC2 đi ra ngoài, AWS cung cấp một khái niệm gọi là Security Group (_Đây là kiến thức thuộc về **Networking** nhưng cần thiết đề cập đến tại đây_)

![alt text](images/Screenshot%20from%202024-08-15%2020-47-15.png)

**Chú ý**:

- Rule của một security group là stateful, một request đến sẽ tự nhận được response mà không phải định nghĩa 1 cách tường minh cho phép đi ra.
- Default nếu như không có yêu cầu gì đặc biệt thì outbound rule sẽ mặc định là mở cho all.
- Rule của security group chỉ có Allow, không có Deny.
- Một EC2 có thể gắn nhiều hơn một security group.

### User-data và Meta-data

EC2 cung cấp cơ chế cho phép chạy script tại thời điểm launch gọi là **user data**
Có thể sử dụng user data để thực thi một số hành động

- Install software.
- Download source code/artifact.
- Customize settings.
  Lưu ý là không nên để các thông tin nhạy cảm như DB username/password vào trong user data.

Mỗi EC2 có một bộ thông tin được nạp lên sau khi khởi động gọi là **meta data**.
Thông tin bao gồm địa chỉ IP public/private, security group, AMI-ID, Role,... phục vụ truy xuất khi cần thiết.
Metada được lưu tại địa chỉ: http://169.254.169.254/latest/meta-data (cố định cho cả Windows và Linux)

### Use case của EC2

EC2 là dịch vụ rất mạnh mẽ của AWS, xuất hiện trong hầu hết các hệ thống. Ngoài ra EC2 còn là nền tảng cơ bản của các dịch vụ như ECS và EKS (k8s).

**User case cơ bản**:

- Lift and shift: Migrate 1:1 các ứng dụng đang chạy trên On-premise của công ty, không có nhu cầu tái cấu trúc.
- Chạy các website cơ bản all in one.
- Compute cluster: dùng cho các ứng dụng chạy xử lý data như Hadoop, Spark,...
- Dùng làm database trong trường hợp không muốn xài dịch vụ database sẵn của AWS.
- Dùng làm node của cluster K8S.

### Elastic Block Storage (EBS)

#### Đặc trưng

- Là một cơ chế lưu trữ dạng block.
- Đơn vị quản lí là các EBS Volume.
- Chỉ có thể access data khi được gắn vào một EC2 instance (dùng làm ổ root, C: hoặc ổ data).
- Một số loại EBS đặc biệt cho phép gắn vào nhiều hơn 1 EC2 Instance (Multi attach)
- Có thể tăng size một cách dễ dàng ngay cả khi server đang chạy.

#### Tính tiền

- Dung lượng của volume ($/GB/Month), không xài hết cũng sẽ mất tiền 100% trên dung lượng vì đã cấp phát rồi.
- IOPS: Tốc độ đọc ghi càng cao, càng phát sinh phí.
- Dung lượng của các bản snapshot của ổ cứng ($/GB/Month) tuy nhiên giá rẻ hơn lưu trữ.

#### Các loại thường dùng

- **General purpose** (default) - gp2, gp3: Phù hợp cho hầu hết các mục đích sử dụng.
- **IOPS Provisioned** - io1, io2: Phù hợp cho các ứng dụng đòi hỏi tốc độ đọc ghi cao.
- **Throughput optimized HDD**: Dùng cho các hệ thống về Bigdata, Data warehouse, cần throughput cao.
- **Cold HDD**: Lưu trữ giá rẻ cho các file ít khi được access (VD File server của công ty).
- **Magnetic**: Thế hệ trước của HDD, ít được sử dụng.

# Misc.

- <details>
  <summary>
  <b>Identity and Access Management (IAM)</b>
  </summary>

  IAM dùng để định danh và phân quyền, quản lí ai (who) và cái gì (what) có thể được access như thế nào tới các resource trên AWS, quản lí một cách tập trung các quyền chi tiết, phân tích truy cập để tinh chỉnh quyền.

  - <details>
    <summary>
    <b>Use case</b>
    </summary>

    - Áp dụng quyền chi tiết và mở rộng quy mô với khả năng kiểm soát truy cập dựa trên thuộc tính. Vd: phòng ban, job role, tên nhóm.
    - Quản lý truy cập theo từng tài khoản hoặc mở rộng quy mô truy cập trên các tài khoản và ứng dụng AWS.
    - Thiết lập quy tắc bảo vệ & phòng ngừa cho toàn tổ chức.
    - Thiết lập, xác minh và điều chỉnh quy mô quyền đối với đặc quyền tối thiểu. 
    > (Nghĩa là với IAM, có thể thiết lập một set role cung cấp vừa đủ cho một thực thể để thực hiện một chức năng nào đó mà không cần cấp dư quyền.)
    </details>

  - <details>
    <summary>
    <b>IAM Basic Concepts</b>
    </summary>

    Để có thể thiết kế & xây dựng hệ thống trên AWS đảm bảo tiêu chí về  Security cũng như không gặp trouble, chúng ta cần nắm vững các **concept cơ bản** (*các concepts dưới đây không phải tất cả*):
    - User
    - Group
    - Role
    - Permission (Policy)
    </details>

  - <details>
    <summary>
    <b>Policy</b>
    </summary>

    Quy định việc ai/cái gì có thể hoặc không thể làm gì.
    
    Một policy thường bao gồm nhiều `Statement` quy định `Allow/Deny` hành động trên một resource dựa trên condition nào đó.

    Mỗi statement cần định nghĩa các thông tin:

    - Effect: có hai loại là Allow & Deny. *Deny được ưu tiên hơn.
    - Action: tập hợp các action cho phép thực thi.
    - Resource: tập hợp các Resource cho phép tương tác.
    - [Condition]: Điều kiện kèm theo để apply statement này.

    Policy có thể gắn vào Role/Group/User.

    Policy có hai loại là **Inline Policy** và **Managed Policy**:

    - Inline Policy: được đính trực tiếp trên Role/Group/User và không thể tái sử dụng ở Role/Group/User khác.
    - Managed Policy: Được tạo riêng và có thể gắn vào nhiều Role/Group/User.

    Managed Policy lại được chia thành hai loại là AWS Managed và User Managed.

    Việc lựa chọn giữa Inline vs Managed phải được tính toán dựa trên các yếu tố như: tính tái sử dụng, quản lý thay đổi tập trung, versioning & rollback.

    ![img](images/Screenshot%20from%202024-08-18%2023-46-31.png)
    </details>
  </details>
