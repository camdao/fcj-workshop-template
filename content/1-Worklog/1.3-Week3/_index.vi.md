---
title: "Worklog Tuần 3"
date: 2024-01-01
weight: 3
chapter: false
pre: " <b> 1.3. </b> "
---

### Mục tiêu tuần 3:

* Nắm vững kiến thức cơ bản về VPC (Virtual Private Cloud) và các khái niệm về mạng.
* Hiểu về subnets, route tables và internet gateways.
* Tìm hiểu về Network ACLs và bảo mật VPC.
* Thực hành xây dựng kiến trúc mạng an toàn.

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc                                                                                                                                                                                   | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu                            |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------ | --------------- | ----------------------------------------- |
| 2   | - Tìm hiểu VPC Fundamentals: <br>&emsp; + Khái niệm và thành phần VPC <br>&emsp; + CIDR blocks và địa chỉ IP <br>&emsp; + Default vs. Custom VPC <br>&emsp; + Giới hạn và quota của VPC  | 25/06/2026   | 25/06/2026      | <https://cloudjourney.awsstudygroup.com/> |
| 3   | - Tìm hiểu Subnets & Route Tables: <br>&emsp; + Public vs. Private subnets <br>&emsp; + Cấu hình route table <br>&emsp; + Internet Gateway (IGW) <br>&emsp; + NAT Gateway vs. NAT Instance | 26/06/2026   | 26/06/2026      | <https://cloudjourney.awsstudygroup.com/> |
| 4   | - **Thực hành:** <br>&emsp; + Tạo custom VPC <br>&emsp; + Cấu hình subnets qua các AZs <br>&emsp; + Thiết lập route tables <br>&emsp; + Gắn Internet Gateway                              | 27/06/2026   | 27/06/2026      | <https://cloudjourney.awsstudygroup.com/> |
| 5   | - Tìm hiểu VPC Security: <br>&emsp; + Network ACLs (NACLs) <br>&emsp; + Security Groups vs. NACLs <br>&emsp; + VPC Flow Logs <br>&emsp; + Best practices cho network security              | 28/06/2026   | 28/06/2026      | <https://cloudjourney.awsstudygroup.com/> |
| 6   | - **Thực hành:** <br>&emsp; + Cấu hình Network ACLs <br>&emsp; + Thiết lập VPC Flow Logs <br>&emsp; + Triển khai kiến trúc multi-tier <br>&emsp; + Kiểm tra connectivity và security      | 29/06/2026   | 29/06/2026      | <https://cloudjourney.awsstudygroup.com/> |


### Kết quả đạt được tuần 3:

* Nắm vững kiến thức cơ bản về VPC:
  * Hiểu các khái niệm và kiến trúc VPC
  * Lập kế hoạch CIDR block và quản lý địa chỉ IP
  * Các thành phần VPC và mối quan hệ giữa chúng
  * Sự khác biệt giữa Default và Custom VPC

* Tìm hiểu về subnets và availability zones:
  * Cấu hình Public subnet cho các tài nguyên hướng internet
  * Cấu hình Private subnet cho các tài nguyên backend
  * Triển khai Multi-AZ cho high availability
  * Phân chia subnet và phân bổ địa chỉ

* Hiểu các khái niệm về routing:
  * Tạo và liên kết route table
  * Internet Gateway (IGW) cho kết nối internet
  * NAT Gateway cho private subnet truy cập internet
  * Độ ưu tiên route table và đánh giá route

* Nắm vững cơ chế bảo mật VPC:
  * Network ACLs (stateless firewall)
  * So sánh giữa Security Groups và NACLs
  * Cấu hình inbound và outbound rules
  * Chiến lược defense in depth

* Thành công trong việc tạo và cấu hình custom VPC:
  * Thiết kế VPC với CIDR blocks phù hợp
  * Tạo public và private subnets qua nhiều AZs
  * Cấu hình route tables cho các loại subnet khác nhau
  * Gắn và cấu hình Internet Gateway

* Triển khai các best practices về VPC security:
  * Cấu hình Network ACLs cho bảo mật ở tầng subnet
  * Thiết lập VPC Flow Logs để giám sát
  * Triển khai least privilege access
  * Tài liệu hóa kiến trúc mạng

* Có kinh nghiệm thực tế với:
  * Thiết kế kiến trúc multi-tier (web, app, database tiers)
  * Kiểm tra kết nối giữa các subnets
  * Khắc phục sự cố mạng
  * Các khái niệm VPC peering

* Xây dựng kiến thức nền tảng cho các chủ đề networking nâng cao như VPC Peering, Transit Gateway và PrivateLink.