---
title: "Worklog Tuần 7"
date: 2024-01-01
weight: 7
chapter: false
pre: " <b> 1.7. </b> "
---

### Mục tiêu tuần 7:

* Nắm vững AWS CloudFormation cho Infrastructure as Code.
* Hiểu về cấu trúc template và quản lý tài nguyên.
* Tìm hiểu về stack operations và change sets.
* Thực hành tự động hóa triển khai infrastructure.

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc                                                                                                                                                                                   | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu                            |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------ | --------------- | ----------------------------------------- |
| 2   | - Tìm hiểu CloudFormation Fundamentals: <br>&emsp; + Các khái niệm Infrastructure as Code <br>&emsp; + Cấu trúc template (YAML/JSON) <br>&emsp; + Resources, parameters, outputs <br>&emsp; + Intrinsic functions | 23/07/2026   | 23/07/2026      | <https://cloudjourney.awsstudygroup.com/> |
| 3   | - Tìm hiểu Stack Management: <br>&emsp; + Tạo và cập nhật stacks <br>&emsp; + Change sets <br>&emsp; + Stack policies <br>&emsp; + Drift detection                                        | 24/07/2026   | 24/07/2026      | <https://cloudjourney.awsstudygroup.com/> |
| 4   | - **Thực hành:** <br>&emsp; + Viết CloudFormation templates <br>&emsp; + Tạo stacks từ templates <br>&emsp; + Sử dụng parameters và mappings <br>&emsp; + Cấu hình outputs                 | 25/07/2026   | 25/07/2026      | <https://cloudjourney.awsstudygroup.com/> |
| 5   | - Tìm hiểu Advanced Features: <br>&emsp; + Nested stacks <br>&emsp; + Cross-stack references <br>&emsp; + Custom resources <br>&emsp; + StackSets cho multi-account/region                | 26/07/2026   | 26/07/2026      | <https://cloudjourney.awsstudygroup.com/> |
| 6   | - **Thực hành:** <br>&emsp; + Tạo nested stacks <br>&emsp; + Triển khai cross-stack references <br>&emsp; + Sử dụng change sets <br>&emsp; + Deploy ứng dụng multi-tier                   | 27/07/2026   | 27/07/2026      | <https://cloudjourney.awsstudygroup.com/> |


### Kết quả đạt được tuần 7:

* Nắm vững các khái niệm Infrastructure as Code:
  * Hiểu lợi ích của IaC (version control, repeatability, automation)
  * CloudFormation vs. các IaC tools khác
  * Phương pháp declarative vs. imperative
  * Quản lý infrastructure theo template

* Tìm hiểu cấu trúc CloudFormation template:
  * Cú pháp YAML và JSON
  * Các phần của template (Parameters, Resources, Outputs, Mappings, Conditions)
  * Khai báo resource và properties
  * Intrinsic functions (Ref, GetAtt, Sub, Join, Select)

* Thành công trong việc tạo CloudFormation templates:
  * Viết templates cho VPC, subnets và security groups
  * Tạo templates cho EC2 instances với user data
  * Định nghĩa S3 buckets, IAM roles và policies
  * Sử dụng parameters cho templates tái sử dụng

* Hiểu về stack operations:
  * Tạo stacks từ templates
  * Cập nhật stacks với change sets
  * Rolling back các updates thất bại
  * Xóa stacks và dọn dẹp resources

* Tìm hiểu về change management:
  * Change sets để preview updates
  * Stack policies để bảo vệ resources
  * Drift detection cho configuration compliance
  * Update behaviors (No Interrupt, Some Interrupt, Replacement)

* Nắm vững các tính năng CloudFormation:
  * Conditions cho conditional resource creation
  * Mappings cho environment-specific values
  * Outputs để export values
  * DependsOn cho explicit resource dependencies

* Thành công trong việc triển khai advanced patterns:
  * Nested stacks cho modular templates
  * Cross-stack references với exports/imports
  * Custom resources với Lambda
  * Stack termination protection

* Có kinh nghiệm thực tế với:
  * Version controlling CloudFormation templates
  * Tự động hóa infrastructure deployment
  * Quản lý nhiều environments (dev, staging, prod)
  * Troubleshooting stack creation failures

* Hiểu các best practices về CloudFormation:
  * Tổ chức templates để tái sử dụng
  * Parameter validation và constraints
  * Sử dụng AWS Systems Manager Parameter Store
  * Ước tính chi phí trước khi deploy

* Xây dựng kiến thức nền tảng cho các khái niệm IaC nâng cao, tích hợp CI/CD và multi-account/multi-region deployments với StackSets.