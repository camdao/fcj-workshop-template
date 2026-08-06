---
title: "Worklog Tuần 4"
date: 2024-01-01
weight: 4
chapter: false
pre: " <b> 1.4. </b> "
---

### Mục tiêu tuần 4:

* Nắm vững kiến thức cơ bản về Amazon S3 (Simple Storage Service).
* Hiểu về các storage classes và lifecycle policies của S3.
* Tìm hiểu về bảo mật S3, versioning và replication.
* Thực hành xây dựng các giải pháp lưu trữ có khả năng mở rộng.

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc                                                                                                                                                                                   | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu                            |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------ | --------------- | ----------------------------------------- |
| 2   | - Tìm hiểu S3 Fundamentals: <br>&emsp; + Các khái niệm S3 (buckets, objects, keys) <br>&emsp; + Kiến trúc lưu trữ S3 <br>&emsp; + Đặt tên bucket và regions <br>&emsp; + Mô hình consistency của S3 | 02/07/2026   | 02/07/2026      | <https://cloudjourney.awsstudygroup.com/> |
| 3   | - Tìm hiểu S3 Storage Classes: <br>&emsp; + S3 Standard <br>&emsp; + S3 Intelligent-Tiering <br>&emsp; + S3 Glacier & Glacier Deep Archive <br>&emsp; + So sánh các storage classes          | 03/07/2026   | 03/07/2026      | <https://cloudjourney.awsstudygroup.com/> |
| 4   | - **Thực hành:** <br>&emsp; + Tạo S3 buckets <br>&emsp; + Upload và quản lý objects <br>&emsp; + Cấu hình storage classes <br>&emsp; + Thiết lập lifecycle policies                        | 04/07/2026   | 04/07/2026      | <https://cloudjourney.awsstudygroup.com/> |
| 5   | - Tìm hiểu S3 Security & Access Control: <br>&emsp; + Bucket policies <br>&emsp; + IAM policies cho S3 <br>&emsp; + S3 Access Control Lists (ACLs) <br>&emsp; + Encryption (SSE-S3, SSE-KMS, SSE-C) | 05/07/2026   | 05/07/2026      | <https://cloudjourney.awsstudygroup.com/> |
| 6   | - **Thực hành:** <br>&emsp; + Cấu hình bucket policies <br>&emsp; + Bật versioning <br>&emsp; + Thiết lập cross-region replication <br>&emsp; + Bật encryption và MFA delete                | 06/07/2026   | 06/07/2026      | <https://cloudjourney.awsstudygroup.com/> |


### Kết quả đạt được tuần 4:

* Nắm vững kiến thức cơ bản về Amazon S3:
  * Hiểu kiến trúc và các khái niệm lưu trữ S3
  * Phân cấp bucket và object
  * Quy ước đặt tên S3 và best practices
  * Mô hình strong consistency và ý nghĩa

* Tìm hiểu về các S3 storage classes:
  * S3 Standard cho dữ liệu truy cập thường xuyên
  * S3 Intelligent-Tiering cho tối ưu chi phí tự động
  * S3 Standard-IA và One Zone-IA cho truy cập không thường xuyên
  * S3 Glacier và Glacier Deep Archive cho lưu trữ dài hạn
  * Đánh đổi giữa chi phí và hiệu suất

* Hiểu về quản lý lifecycle của S3:
  * Tạo lifecycle policies
  * Chuyển đổi objects giữa các storage classes
  * Tự động xóa objects hết hạn
  * Tối ưu hóa chi phí lưu trữ

* Thành công trong việc tạo và cấu hình S3 buckets:
  * Tạo buckets với tên phù hợp
  * Upload và tổ chức objects
  * Cấu hình storage classes dựa trên mô hình truy cập
  * Thiết lập lifecycle policies để tối ưu chi phí

* Nắm vững các cơ chế bảo mật S3:
  * Bucket policies cho resource-based access control
  * IAM policies cho identity-based access control
  * Access Control Lists (ACLs) - phương pháp cũ
  * Cài đặt Block Public Access
  * Hiểu logic đánh giá policy

* Triển khai mã hóa S3:
  * Server-Side Encryption với S3 (SSE-S3)
  * Server-Side Encryption với KMS (SSE-KMS)
  * Server-Side Encryption với Customer keys (SSE-C)
  * Mã hóa trong quá trình truyền (HTTPS/TLS)

* Tìm hiểu về versioning và replication của S3:
  * Bật và quản lý versioning
  * Bảo vệ chống xóa nhầm
  * Cross-Region Replication (CRR) cho disaster recovery
  * Same-Region Replication (SRR) cho compliance

* Có kinh nghiệm thực tế với:
  * S3 static website hosting
  * Pre-signed URLs cho truy cập tạm thời
  * S3 event notifications
  * S3 access logging và monitoring

* Hiểu về tối ưu hóa hiệu suất S3:
  * Multipart uploads cho objects lớn
  * Transfer Acceleration
  * Hiệu suất request rate
  * Best practices cho đặt tên keys

* Xây dựng kiến thức nền tảng cho các tính năng S3 nâng cao như S3 Select, S3 Batch Operations và tích hợp với các dịch vụ AWS khác.