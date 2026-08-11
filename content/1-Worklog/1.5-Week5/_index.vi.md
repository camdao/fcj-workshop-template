---
title: "Worklog Tuần 5"
date: 2024-01-29
weight: 5
chapter: false
pre: " <b> 1.5. </b> "
---

### Mục tiêu tuần 5:

* Phát triển ứng dụng web demo (frontend và backend).
* Container hóa các thành phần ứng dụng sử dụng Docker.
* Thiết lập Amazon ECR (Elastic Container Registry) để lưu trữ images.
* Triển khai ứng dụng container hóa trên Amazon ECS (Elastic Container Service).
* Cấu hình ECS task definitions và services.

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc                                                                                                                                                                                   | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu                            |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------ | --------------- | ----------------------------------------- |
| 1   | - Phát triển frontend: <br>&emsp; + Tạo ứng dụng React/Vue <br>&emsp; + Build UI components <br>&emsp; + Tích hợp với backend API <br>&emsp; + Test locally | 09/07/2026   | 09/07/2026      | Tài liệu React/Vue |
| 2   | - Phát triển backend API: <br>&emsp; + Tạo REST API endpoints <br>&emsp; + Triển khai business logic <br>&emsp; + Kết nối đến RDS và DynamoDB <br>&emsp; + Test API locally | 10/07/2026   | 10/07/2026      | Tài liệu Node.js/Python |
| 3   | - Container hóa ứng dụng: <br>&emsp; + Viết Dockerfiles <br>&emsp; + Tối ưu kích thước image <br>&emsp; + Test containers locally <br>&emsp; + Tạo docker-compose cho local dev | 11/07/2026   | 11/07/2026      | <https://docs.docker.com/> |
| 4   | - Thiết lập Amazon ECR và ECS: <br>&emsp; + Tạo ECR repositories <br>&emsp; + Push images lên ECR <br>&emsp; + Tạo ECS cluster <br>&emsp; + Cấu hình task definitions | 12/07/2026   | 12/07/2026      | <https://000048.awsstudygroup.com/> |
| 5   | - Triển khai lên ECS: <br>&emsp; + Tạo ECS services <br>&emsp; + Cấu hình load balancer integration <br>&emsp; + Thiết lập auto scaling <br>&emsp; + Test deployment | 13/07/2026   | 13/07/2026      | <https://000048.awsstudygroup.com/> |


### Kết quả đạt được tuần 5:

* **Phát triển Ứng dụng:**
  * Xây dựng React/Vue frontend hoạt động với responsive UI
  * Phát triển RESTful backend API với Node.js/Python
  * Triển khai authentication và authorization
  * Kết nối backend đến RDS (PostgreSQL) và DynamoDB
  * Tạo tài liệu API toàn diện

* **Container hóa:**
  * Tạo Dockerfiles tối ưu cho frontend và backend
  * Triển khai multi-stage builds để giảm kích thước image
  * Cấu hình environment variables và secrets management
  * Test containers locally với docker-compose
  * Chuẩn bị images cho production deployment

* **Thiết lập Amazon ECR:**
  * Tạo private ECR repositories cho application images
  * Cấu hình ECR lifecycle policies cho image retention
  * Push Docker images lên ECR thành công
  * Thiết lập ECR scanning cho vulnerabilities

* **Triển khai Amazon ECS:**
  * Tạo ECS Fargate cluster cho serverless containers
  * Định nghĩa ECS task definitions với resource allocation phù hợp
  * Cấu hình ECS services với desired count và placement strategies
  * Tích hợp ECS với Application Load Balancer từ Tuần 2
  * Thiết lập ECS service auto scaling dựa trên CPU/memory
  * Cấu hình CloudWatch Logs cho container logging
  * Triển khai ứng dụng lên production thành công

* **Thành tựu chính:**
  * Ứng dụng cloud-native hoạt động đầy đủ
  * Kiến trúc microservices được container hóa
  * Triển khai production trên ECS
  * Tích hợp với các dịch vụ AWS (RDS, DynamoDB, ALB)
  * Sẵn sàng cho staging environment và testing ở Tuần 6