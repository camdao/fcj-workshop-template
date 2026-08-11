---
title: "Worklog Tuần 3"
date: 2024-01-15
weight: 3
chapter: false
pre: " <b> 1.3. </b> "
---

### Mục tiêu tuần 3:

* Thành thạo Amazon S3 cho object storage và static website hosting.
* Hiểu S3 versioning, lifecycle policies và các tính năng bảo mật.
* Học Amazon RDS để quản lý relational database (PostgreSQL/MySQL).
* Hiểu Amazon DynamoDB cho yêu cầu NoSQL database.
* Triển khai chiến lược backup và disaster recovery.

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc                                                                                                                                                                                   | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu                            |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------ | --------------- | ----------------------------------------- |
| 1   | - Học S3 cơ bản: <br>&emsp; + Buckets và objects <br>&emsp; + Storage classes (Standard, IA, Glacier) <br>&emsp; + S3 security (bucket policies, ACLs) <br>&emsp; + Static website hosting <br> - **Thực hành:** <br>&emsp; + Tạo S3 buckets <br>&emsp; + Upload objects <br>&emsp; + Cấu hình bucket policies <br>&emsp; + Host static website | 25/06/2026   | 25/06/2026      | <https://000009.awsstudygroup.com/> |
| 2   | - Học S3 tính năng nâng cao: <br>&emsp; + Versioning <br>&emsp; + Lifecycle policies <br>&emsp; + Cross-region replication <br>&emsp; + S3 Transfer Acceleration <br> - **Thực hành:** <br>&emsp; + Bật versioning <br>&emsp; + Tạo lifecycle rules <br>&emsp; + Thiết lập replication | 26/06/2026   | 26/06/2026      | <https://000010.awsstudygroup.com/> |
| 3   | - Học Amazon RDS: <br>&emsp; + RDS engines (PostgreSQL, MySQL, Aurora) <br>&emsp; + Multi-AZ deployments <br>&emsp; + Read replicas <br>&emsp; + Automated backups <br> - **Thực hành:** <br>&emsp; + Khởi chạy RDS instance <br>&emsp; + Cấu hình security groups <br>&emsp; + Kết nối từ EC2 <br>&emsp; + Tạo snapshots | 27/06/2026   | 27/06/2026      | <https://000024.awsstudygroup.com/> |
| 4   | - Học DynamoDB: <br>&emsp; + Tables, items, attributes <br>&emsp; + Primary keys (partition & sort) <br>&emsp; + Indexes (GSI, LSI) <br>&emsp; + Read/write capacity modes <br> - **Thực hành:** <br>&emsp; + Tạo DynamoDB table <br>&emsp; + Put/get items <br>&emsp; + Tạo GSI <br>&emsp; + Test queries | 28/06/2026   | 28/06/2026      | <https://000025.awsstudygroup.com/> |
| 5   | - Học chiến lược backup: <br>&emsp; + RDS automated backups <br>&emsp; + Manual snapshots <br>&emsp; + DynamoDB on-demand backups <br>&emsp; + Point-in-time recovery <br> - **Thực hành:** <br>&emsp; + Cấu hình backup retention <br>&emsp; + Restore từ snapshot <br>&emsp; + Test PITR | 29/06/2026   | 29/06/2026      | <https://000026.awsstudygroup.com/> |


### Kết quả đạt được tuần 3:

* **Thành thạo Amazon S3:**
  * Hiểu các khái niệm cơ bản và use cases của S3
  * Thành thạo các storage classes và tối ưu hóa chi phí
  * Triển khai security best practices
  * Cấu hình versioning và lifecycle policies
  * Thành công host static websites trên S3

* **Triển khai Amazon RDS:**
  * Deploy PostgreSQL và MySQL RDS instances
  * Cấu hình Multi-AZ cho high availability
  * Thiết lập read replicas cho read-heavy workloads
  * Triển khai chiến lược automated backup
  * Kết nối applications an toàn đến RDS

* **DynamoDB NoSQL Database:**
  * Hiểu DynamoDB data modeling
  * Tạo tables với primary keys phù hợp
  * Triển khai Global Secondary Indexes
  * Cấu hình on-demand và provisioned capacity
  * Test query và scan operations

* **Backup & Disaster Recovery:**
  * Triển khai chiến lược backup toàn diện
  * Test restore procedures cho RDS và DynamoDB
  * Cấu hình point-in-time recovery
  * Hiểu yêu cầu RPO và RTO
  * Sẵn sàng tích hợp storage và databases vào kiến trúc dự án