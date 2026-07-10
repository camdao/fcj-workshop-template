---
title: "Worklog Tuần 2"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 1.2. </b> "
---
<!-- {{% notice warning %}}
⚠️ **Lưu ý:** Các thông tin dưới đây chỉ nhằm mục đích tham khảo, vui lòng **không sao chép nguyên văn** cho bài báo cáo của bạn kể cả warning này.
{{% /notice %}} -->


### Mục tiêu tuần 2:

* Nắm vững kiến thức cơ bản về Amazon EC2 (Elastic Compute Cloud) và compute fundamentals.
* Tìm hiểu instance profiling với IAM Roles cho EC2.
* Hiểu về EC2 instance types, AMI, storage và networking.

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc                                                                                                                                                                                   | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu                            |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------ | --------------- | ----------------------------------------- |
| 2   | - Tìm hiểu EC2 Compute Essentials: <br>&emsp; + Các loại và họ EC2 instance <br>&emsp; + Vòng đời và trạng thái instance <br>&emsp; + Các mô hình giá (On-Demand, Reserved, Spot) <br>&emsp; + AMI (Amazon Machine Images) | 18/06/2026   | 18/06/2026      | <https://cloudjourney.awsstudygroup.com/> |
| 3   | - Tìm hiểu EC2 Storage & Networking: <br>&emsp; + EBS (Elastic Block Store) <br>&emsp; + Các loại EBS volume <br>&emsp; + Security Groups <br>&emsp; + Key pairs <br>&emsp; + Elastic IP  | 19/06/2026   | 19/06/2026      | <https://cloudjourney.awsstudygroup.com/> |
| 4   | - **Thực hành:** <br>&emsp; + Khởi tạo EC2 instances <br>&emsp; + Cấu hình Security Groups <br>&emsp; + Kết nối qua SSH <br>&emsp; + Gắn và quản lý EBS volumes                           | 20/06/2026   | 20/06/2026      | <https://cloudjourney.awsstudygroup.com/> |
| 5   | - Tìm hiểu IAM Roles cho EC2: <br>&emsp; + Instance profiles <br>&emsp; + Gắn IAM roles vào EC2 <br>&emsp; + Quản lý AWS credentials <br>&emsp; + Best practices cho EC2 security          | 21/06/2026   | 21/06/2026      | <https://cloudjourney.awsstudygroup.com/> |
| 6   | - **Thực hành:** <br>&emsp; + Tạo IAM roles cho EC2 <br>&emsp; + Gắn roles vào instances <br>&emsp; + Kiểm tra permissions <br>&emsp; + Truy cập AWS services từ EC2 sử dụng IAM roles    | 22/06/2026   | 22/06/2026      | <https://cloudjourney.awsstudygroup.com/> |


### Kết quả đạt được tuần 2:

* Nắm vững kiến thức cơ bản về Amazon EC2:
  * Các loại và họ EC2 instance (General Purpose, Compute Optimized, Memory Optimized, v.v.)
  * Vòng đời và trạng thái instance (pending, running, stopped, terminated)
  * Các mô hình giá (On-Demand, Reserved Instances, Spot Instances, Savings Plans)
  * Hiểu khi nào nên sử dụng các loại instance khác nhau

* Tìm hiểu về Amazon Machine Images (AMI):
  * Các loại và nguồn AMI
  * Tạo custom AMIs
  * Chia sẻ và sao chép AMI qua các regions

* Hiểu về các tùy chọn storage của EC2:
  * Các loại EBS (Elastic Block Store) volume (gp3, gp2, io2, st1, sc1)
  * Chiến lược EBS snapshots và backup
  * Instance store vs. EBS
  * Gắn và tháo volumes

* Nắm vững kiến thức cơ bản về EC2 networking:
  * Cấu hình Security Groups và rules
  * Network interfaces (ENI)
  * Elastic IP addresses
  * Quản lý SSH key pairs

* Thành công trong việc khởi tạo và quản lý EC2 instances:
  * Tạo instances với các cấu hình khác nhau
  * Kết nối đến instances qua SSH
  * Cấu hình Security Groups cho kiểm soát truy cập phù hợp
  * Gắn và quản lý EBS volumes

* Tìm hiểu Instance Profiling với IAM Roles cho EC2:
  * Hiểu về instance profiles
  * Tạo IAM roles cho EC2 instances
  * Gắn IAM roles vào running instances
  * Best practices cho EC2 security và permissions

* Thực hành triển khai IAM Roles:
  * Tạo IAM roles với các policies phù hợp
  * Gắn roles vào EC2 instances
  * Kiểm tra quyền truy cập AWS services từ EC2 sử dụng roles
  * Loại bỏ nhu cầu hardcode credentials

* Hiểu các best practices về EC2 security:
  * Nguyên tắc least privilege cho IAM roles
  * Quản lý Security Group rules
  * Quản lý SSH keys
  * Cập nhật và vá lỗi thường xuyên

* Có kinh nghiệm thực tế với EC2 automation và quản lý qua Console và CLI.


