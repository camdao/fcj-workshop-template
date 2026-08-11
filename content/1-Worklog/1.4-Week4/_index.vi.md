---
title: "Worklog Tuần 4"
date: 2024-01-22
weight: 4
chapter: false
pre: " <b> 1.4. </b> "
---

### Mục tiêu tuần 4:

* Lập kế hoạch kiến trúc và yêu cầu cho capstone project.
* Học kiến thức cơ bản về Docker và nguyên tắc containerization.
* Hiểu khái niệm CI/CD và pipelines.
* Nghiên cứu AWS security best practices và compliance.
* Thiết kế hạ tầng dự án và tech stack.

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc                                                                                                                                                                                   | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu                            |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------ | --------------- | ----------------------------------------- |
| 1   | - Định nghĩa yêu cầu dự án: <br>&emsp; + Tính năng ứng dụng <br>&emsp; + Ràng buộc kỹ thuật <br>&emsp; + Yêu cầu hiệu suất <br> - Thiết kế kiến trúc: <br>&emsp; + Frontend (React/Vue trên S3) <br>&emsp; + Backend (Node.js/Python trên ECS) <br>&emsp; + Database layer (RDS + DynamoDB) | 02/07/2026   | 02/07/2026      | Tài liệu lập kế hoạch dự án |
| 2   | - Học Docker cơ bản: <br>&emsp; + Khái niệm Docker (images, containers) <br>&emsp; + Cú pháp Dockerfile <br>&emsp; + Lệnh Docker <br> - **Thực hành:** <br>&emsp; + Cài đặt Docker <br>&emsp; + Tạo Dockerfile <br>&emsp; + Build và chạy containers | 03/07/2026   | 03/07/2026      | <https://docs.docker.com/> |
| 3   | - Học CI/CD cơ bản: <br>&emsp; + Khái niệm CI/CD pipeline <br>&emsp; + GitHub Actions cơ bản <br>&emsp; + AWS CodePipeline <br>&emsp; + Automated testing <br> - **Thực hành:** <br>&emsp; + Tạo simple pipeline <br>&emsp; + Cấu hình build steps | 04/07/2026   | 04/07/2026      | <https://docs.github.com/actions> |
| 4   | - Học AWS security: <br>&emsp; + CloudTrail cho auditing <br>&emsp; + AWS Config <br>&emsp; + Secrets Manager <br>&emsp; + KMS encryption <br> - **Thực hành:** <br>&emsp; + Bật CloudTrail <br>&emsp; + Lưu secrets trong Secrets Manager <br>&emsp; + Cấu hình encryption | 05/07/2026   | 05/07/2026      | <https://000052.awsstudygroup.com/> |
| 5   | - Hoàn thiện kế hoạch dự án: <br>&emsp; + Tài liệu hóa kiến trúc <br>&emsp; + Định nghĩa milestones <br>&emsp; + Tạo task breakdown <br>&emsp; + Thiết lập project repository | 06/07/2026   | 06/07/2026      | Tài liệu kiến trúc |


### Kết quả đạt được tuần 4:

* **Lập kế hoạch & Kiến trúc Dự án:**
  * Định nghĩa yêu cầu và phạm vi dự án toàn diện
  * Thiết kế kiến trúc cloud-native microservices
  * Lựa chọn tech stack phù hợp (React, Node.js/Python, PostgreSQL, DynamoDB)
  * Tạo sơ đồ kiến trúc và tài liệu
  * Thiết lập milestones và timeline dự án

* **Docker Cơ bản:**
  * Hiểu khái niệm và lợi ích của containerization
  * Học cú pháp và best practices của Dockerfile
  * Thực hành build và chạy containers locally
  * Hiểu image layers và caching
  * Chuẩn bị cho container deployment trên ECS

* **Khái niệm CI/CD:**
  * Học nguyên tắc continuous integration và deployment
  * Hiểu GitHub Actions workflows
  * Khám phá AWS CodePipeline và CodeBuild
  * Thiết kế chiến lược automated testing
  * Lập kế hoạch kiến trúc deployment pipeline

* **AWS Security Best Practices:**
  * Bật CloudTrail cho comprehensive auditing
  * Cấu hình AWS Secrets Manager cho credentials
  * Học KMS cho encryption at rest
  * Hiểu compliance frameworks (PCI-DSS, HIPAA)
  * Triển khai security monitoring và alerts

* **Kết quả chính:**
  * Tài liệu kiến trúc dự án
  * Sơ đồ hạ tầng
  * Lựa chọn technology stack
  * Lộ trình phát triển
  * Checklist bảo mật và compliance
  * Sẵn sàng bắt đầu phát triển ứng dụng ở Tuần 5