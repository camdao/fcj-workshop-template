---
title: "Worklog Tuần 1"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 1.1. </b> "
---

### Mục tiêu tuần 1:

* Kết nối, làm quen với các thành viên trong First Cloud Journey - AWS Study Group.
* Hiểu nền tảng AWS và các nhóm dịch vụ cốt lõi.
* Nắm vững IAM (Identity and Access Management) để kiểm soát truy cập an toàn.
* Tìm hiểu AWS Budgets để quản lý và giám sát chi phí.
* Hiểu các kiến thức cơ bản về mạng VPC bao gồm subnets, security groups và routing.

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc                                                                                                                                                                                   | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu                            |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------ | --------------- | ----------------------------------------- |
| 1   | - Làm quen với các thành viên FCAJ <br> - Đọc và lưu ý các nội quy, quy định tại đơn vị thực tập                                                                                             | 11/06/2026   | 11/06/2026      |
| 2   | - Tìm hiểu AWS và các nhóm dịch vụ <br>&emsp; + Compute (EC2, Lambda, ECS) <br>&emsp; + Storage (S3, EBS, EFS) <br>&emsp; + Networking (VPC, Route 53, CloudFront) <br>&emsp; + Database (RDS, DynamoDB) <br> - Tạo AWS Free Tier account <br> - Cài đặt & cấu hình AWS CLI | 12/06/2026   | 12/06/2026      | <https://cloudjourney.awsstudygroup.com/> |
| 3   | - Tìm hiểu sâu về IAM: <br>&emsp; + Users, Groups, Roles <br>&emsp; + Policies và Permissions (managed vs inline) <br>&emsp; + MFA (Multi-Factor Authentication) <br>&emsp; + Best practices và least privilege <br> - **Thực hành:** <br>&emsp; + Tạo IAM users và groups <br>&emsp; + Gán policies <br>&emsp; + Thiết lập MFA <br>&emsp; + Tạo service roles | 13/06/2026   | 13/06/2026      | <https://000007.awsstudygroup.com/> |
| 4   | - Tìm hiểu AWS Budgets: <br>&emsp; + Thiết lập cảnh báo chi phí <br>&emsp; + Các loại ngân sách (Cost, Usage, Reservation) <br>&emsp; + Giám sát sử dụng và dự báo <br> - **Thực hành:** <br>&emsp; + Tạo budget hàng tháng <br>&emsp; + Cấu hình cảnh báo budget <br>&emsp; + Thiết lập billing alarms | 14/06/2026   | 14/06/2026      | <https://000002.awsstudygroup.com/> |
| 5   | - Tìm hiểu VPC cơ bản: <br>&emsp; + Khái niệm VPC và CIDR blocks <br>&emsp; + Public vs Private subnets <br>&emsp; + Internet Gateway và NAT Gateway <br>&emsp; + Route Tables <br>&emsp; + Security Groups vs NACLs <br> - **Thực hành:** <br>&emsp; + Tạo custom VPC <br>&emsp; + Cấu hình subnets <br>&emsp; + Thiết lập routing | 15/06/2026   | 15/06/2026      | <https://000003.awsstudygroup.com/> |


### Kết quả đạt được tuần 1:

* Đã kết nối và làm quen với các thành viên First Cloud Journey và hiểu mục tiêu thực tập.

* **Nền tảng AWS:**
  * Hiểu về hạ tầng toàn cầu AWS (Regions, Availability Zones)
  * Học các nhóm dịch vụ cốt lõi:
    * Compute (EC2, Lambda, ECS, Fargate)
    * Storage (S3, EBS, EFS, Glacier)
    * Networking (VPC, Route 53, CloudFront, Direct Connect)
    * Database (RDS, DynamoDB, Aurora, ElastiCache)
    * Management & Governance (CloudWatch, CloudTrail, CloudFormation)
    * Security, Identity & Compliance (IAM, KMS, Secrets Manager)

* **Thiết lập tài khoản:**
  * Đã tạo và cấu hình AWS Free Tier account thành công
  * Làm quen với điều hướng AWS Management Console
  * Cài đặt và cấu hình AWS CLI:
    * Cấu hình Access Key và Secret Key
    * Thiết lập Region mặc định (ví dụ: us-east-1)
    * Cấu hình định dạng output (json/yaml/table)
  * Xác minh chức năng CLI với các lệnh cơ bản (`aws sts get-caller-identity`)

* **Thành thạo IAM Security:**
  * Hiểu sâu về các thành phần IAM:
    * Users (danh tính cá nhân với credentials dài hạn)
    * Groups (tập hợp users có quyền chung)
    * Roles (credentials tạm thời cho services/applications)
    * Policies (tài liệu JSON định nghĩa quyền hạn)
  * Học các loại policy:
    * AWS Managed Policies (được xây dựng sẵn bởi AWS)
    * Customer Managed Policies (policies tùy chỉnh)
    * Inline Policies (gắn trực tiếp vào user/group/role)
  * Hiểu logic đánh giá quyền hạn và cấu trúc policy
  * Triển khai Multi-Factor Authentication (MFA) để tăng cường bảo mật
  * Áp dụng security best practices:
    * Nguyên tắc least privilege
    * Luân chuyển credentials định kỳ
    * Không sử dụng root account cho công việc hàng ngày
    * IAM users riêng lẻ thay vì credentials dùng chung
  * Tạo các tài nguyên IAM thực tế:
    * Admin user với MFA được kích hoạt
    * Developer group với quyền phù hợp
    * EC2 service role để sử dụng trong tương lai

* **Quản lý Chi phí với AWS Budgets:**
  * Học các loại budget và trường hợp sử dụng:
    * Cost budgets (theo dõi chi tiêu)
    * Usage budgets (theo dõi sử dụng dịch vụ)
    * Reservation budgets (theo dõi sử dụng RI)
    * Savings Plans budgets
  * Thiết lập giám sát chi phí toàn diện:
    * Tạo budget hàng tháng với cảnh báo ngưỡng (ví dụ: $10/tháng)
    * Cấu hình thông báo email ở 50%, 80%, và 100% ngưỡng
    * Thiết lập CloudWatch billing alarms
  * Hiểu về AWS Cost Explorer và cost allocation tags
  * Học các chiến lược tối ưu hóa chi phí:
    * Right-sizing tài nguyên
    * Sử dụng Reserved Instances cho workload dự đoán được
    * Triển khai auto-scaling
    * Tận dụng S3 lifecycle policies

* **VPC Networking Cơ bản:**
  * Hiểu các khái niệm VPC:
    * Mạng riêng ảo trong AWS cloud
    * CIDR notation và quy hoạch địa chỉ IP
    * Best practices về kích thước VPC (ví dụ: /16 cho production)
  * Học thiết kế subnet:
    * Public subnets (với route tới Internet Gateway)
    * Private subnets (cho tài nguyên backend)
    * Kích thước subnet và phân bổ availability zone
  * Thành thạo các thành phần networking:
    * Internet Gateway (IGW) - cho truy cập internet công cộng
    * NAT Gateway - cho private subnet truy cập outbound
    * Route Tables - điều hướng lưu lượng mạng
    * Security Groups - firewall stateful cấp instance
    * Network ACLs - firewall stateless cấp subnet
  * Tạo kiến trúc VPC thực hành:
    * Custom VPC với CIDR block 10.0.0.0/16
    * Public subnet (10.0.1.0/24) trong us-east-1a
    * Private subnet (10.0.2.0/24) trong us-east-1b
    * Cấu hình Internet Gateway và NAT Gateway
    * Thiết lập route tables cho public và private subnets
    * Tạo security groups với inbound/outbound rules phù hợp
  * Hiểu VPC best practices:
    * Triển khai Multi-AZ cho high availability
    * Tách subnets cho các tiers khác nhau (web, app, database)
    * Quy tắc security group tối thiểu (nguyên tắc least privilege)
    * Sử dụng VPC Flow Logs để giám sát mạng

* **Điểm chính rút ra:**
  * Có kiến thức nền tảng để quản lý tài nguyên AWS an toàn
  * Hiểu cách triển khai defense-in-depth security với IAM và network controls
  * Có thể giám sát và kiểm soát chi phí AWS hiệu quả
  * Sẵn sàng triển khai tài nguyên trong môi trường VPC được thiết kế đúng cách
  * Chuẩn bị cho các dịch vụ compute tuần tới với nền tảng networking vững chắc