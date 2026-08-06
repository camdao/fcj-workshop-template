---
title: "Worklog Tuần 5"
date: 2024-01-01
weight: 5
chapter: false
pre: " <b> 1.5. </b> "
---

### Mục tiêu tuần 5:

* Nắm vững các dịch vụ cơ sở dữ liệu AWS (RDS và DynamoDB).
* Hiểu về các khái niệm relational vs. NoSQL database.
* Tìm hiểu về backup, restore và high availability của database.
* Thực hành triển khai và quản lý databases trên AWS.

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc                                                                                                                                                                                   | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu                            |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------ | --------------- | ----------------------------------------- |
| 2   | - Tìm hiểu RDS Fundamentals: <br>&emsp; + Khái niệm và kiến trúc RDS <br>&emsp; + Các database engines được hỗ trợ <br>&emsp; + Các loại RDS instance <br>&emsp; + Multi-AZ deployments    | 09/07/2026   | 09/07/2026      | <https://cloudjourney.awsstudygroup.com/> |
| 3   | - Tìm hiểu RDS Operations: <br>&emsp; + Automated backups <br>&emsp; + Database snapshots <br>&emsp; + Read replicas <br>&emsp; + Parameter groups và option groups                        | 10/07/2026   | 10/07/2026      | <https://cloudjourney.awsstudygroup.com/> |
| 4   | - **Thực hành:** <br>&emsp; + Khởi tạo RDS instances <br>&emsp; + Cấu hình Multi-AZ <br>&emsp; + Tạo read replicas <br>&emsp; + Thực hiện backup và restore                               | 11/07/2026   | 11/07/2026      | <https://cloudjourney.awsstudygroup.com/> |
| 5   | - Tìm hiểu DynamoDB Fundamentals: <br>&emsp; + Khái niệm NoSQL <br>&emsp; + Tables, items và attributes <br>&emsp; + Primary keys và indexes <br>&emsp; + Capacity modes (On-Demand vs. Provisioned) | 12/07/2026   | 12/07/2026      | <https://cloudjourney.awsstudygroup.com/> |
| 6   | - **Thực hành:** <br>&emsp; + Tạo DynamoDB tables <br>&emsp; + Thực hiện CRUD operations <br>&emsp; + Cấu hình GSI và LSI <br>&emsp; + Thiết lập DynamoDB Streams                          | 13/07/2026   | 13/07/2026      | <https://cloudjourney.awsstudygroup.com/> |


### Kết quả đạt được tuần 5:

* Nắm vững kiến thức cơ bản về Amazon RDS:
  * Hiểu về dịch vụ relational database được quản lý
  * Các engines được hỗ trợ (MySQL, PostgreSQL, MariaDB, Oracle, SQL Server, Aurora)
  * Các class và loại storage của RDS instance
  * Multi-AZ deployments cho high availability

* Tìm hiểu các tác vụ vận hành RDS:
  * Automated backup và retention policies
  * Manual snapshots và restoration
  * Read replicas cho read scaling
  * Parameter groups cho cấu hình database
  * Option groups cho các tính năng bổ sung

* Thành công trong việc triển khai và quản lý RDS instances:
  * Khởi tạo RDS instances với cấu hình phù hợp
  * Cấu hình Multi-AZ cho automatic failover
  * Tạo read replicas qua các regions
  * Thực hiện các thao tác backup và restore
  * Giám sát hiệu suất database

* Hiểu về bảo mật RDS:
  * VPC security groups cho network access control
  * IAM database authentication
  * Mã hóa at rest và in transit
  * Enhanced monitoring và Performance Insights

* Nắm vững kiến thức cơ bản về DynamoDB:
  * Các khái niệm và use cases của NoSQL database
  * Kiến trúc và data model của DynamoDB
  * Tables, items, attributes và data types
  * Primary keys (partition key và sort key)

* Tìm hiểu về indexing trong DynamoDB:
  * Global Secondary Indexes (GSI)
  * Local Secondary Indexes (LSI)
  * Best practices cho thiết kế index
  * Query vs. Scan operations

* Thành công trong việc tạo và quản lý DynamoDB tables:
  * Tạo tables với thiết kế key phù hợp
  * Thực hiện CRUD operations qua Console và CLI
  * Cấu hình secondary indexes
  * Thiết lập DynamoDB Streams cho change capture

* Hiểu về các capacity modes của DynamoDB:
  * On-Demand capacity cho unpredictable workloads
  * Provisioned capacity với auto-scaling
  * Các chiến lược tối ưu chi phí
  * Read và write capacity units (RCU/WCU)

* Tìm hiểu các tính năng nâng cao của DynamoDB:
  * DynamoDB Streams cho event-driven architectures
  * Global Tables cho multi-region replication
  * Point-in-time recovery (PITR)
  * Time to Live (TTL) cho automatic data expiration

* Có kinh nghiệm thực tế với:
  * Lựa chọn giữa RDS và DynamoDB
  * Các chiến lược migration database
  * Performance tuning và monitoring
  * Lập kế hoạch backup và disaster recovery

* Xây dựng kiến thức nền tảng cho database best practices, tối ưu chi phí và tích hợp với kiến trúc ứng dụng.