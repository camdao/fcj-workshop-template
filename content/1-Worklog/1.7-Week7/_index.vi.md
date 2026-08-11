---
title: "Worklog Tuần 7"
date: 2024-02-12
weight: 7
chapter: false
pre: " <b> 1.7. </b> "
---

### Mục tiêu tuần 7:

* Xây dựng và cấu hình CI/CD pipeline cho automated deployments.
* Triển khai CloudFront CDN cho frontend content delivery.
* Triển khai Infrastructure as Code với CloudFormation.
* Tạo tài liệu và runbooks toàn diện.
* Hoàn thiện deployment automation.

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc                                                                                                                                                                                   | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu                            |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------ | --------------- | ----------------------------------------- |
| 1   | - Thiết lập CI/CD pipeline: <br>&emsp; + Cấu hình GitHub Actions workflow <br>&emsp; + Thiết lập build và test stages <br>&emsp; + Cấu hình deployment stages <br>&emsp; + Thêm approval gates | 23/07/2026   | 23/07/2026      | <https://docs.github.com/actions> |
| 2   | - Triển khai automated testing trong pipeline: <br>&emsp; + Unit tests <br>&emsp; + Integration tests <br>&emsp; + Security scans <br>&emsp; + Code quality checks | 24/07/2026   | 24/07/2026      | CI/CD best practices |
| 3   | - Triển khai CloudFront CDN: <br>&emsp; + Tạo CloudFront distribution <br>&emsp; + Cấu hình S3 là origin <br>&emsp; + Thiết lập SSL certificate <br>&emsp; + Cấu hình caching policies <br>&emsp; + Thêm custom domain | 25/07/2026   | 25/07/2026      | <https://000011.awsstudygroup.com/> |
| 4   | - Infrastructure as Code: <br>&emsp; + Viết CloudFormation templates <br>&emsp; + Parameterize templates <br>&emsp; + Tạo stacks cho tất cả resources <br>&emsp; + Version control IaC | 26/07/2026   | 26/07/2026      | <https://000040.awsstudygroup.com/> |
| 5   | - Tài liệu và runbooks: <br>&emsp; + Tài liệu kiến trúc <br>&emsp; + Deployment procedures <br>&emsp; + Troubleshooting guides <br>&emsp; + Operational runbooks | 27/07/2026   | 27/07/2026      | Documentation standards |


### Kết quả đạt được tuần 7:

* **Triển khai CI/CD Pipeline:**
  * Xây dựng GitHub Actions pipeline hoàn chỉnh
  * Cấu hình multi-stage workflow (build, test, deploy)
  * Triển khai automated testing ở mỗi stage
  * Thêm manual approval gates cho production
  * Tích hợp với ECR và ECS cho deployments
  * Thiết lập rollback mechanisms
  * Đạt được zero-downtime deployments

* **Automated Testing trong Pipeline:**
  * Tích hợp unit tests với coverage reporting
  * Thêm integration tests cho tất cả APIs
  * Cấu hình security scanning (SAST/DAST)
  * Triển khai code quality gates (linting, formatting)
  * Thiết lập container vulnerability scanning
  * Thêm performance regression tests

* **Triển khai CloudFront CDN:**
  * Tạo CloudFront distribution cho S3 frontend
  * Cấu hình SSL/TLS với ACM certificate
  * Thiết lập custom domain với Route 53
  * Tối ưu caching policies cho performance
  * Cấu hình cache invalidation on deployments
  * Bật compression và HTTP/2
  * Đạt được global content delivery với low latency

* **Infrastructure as Code:**
  * Tạo CloudFormation templates toàn diện
  * Modularize infrastructure thành nested stacks
  * Parameterize cho multi-environment deployment
  * Version control tất cả IaC trong Git
  * Tài liệu hóa stack dependencies
  * Triển khai change sets cho safe updates
  * Có thể recreate entire infrastructure từ code

* **Tài liệu & Runbooks:**
  * Hoàn thành tài liệu kiến trúc với diagrams
  * Viết deployment procedures và checklists
  * Tạo troubleshooting guides cho common issues
  * Tài liệu hóa operational procedures
  * Tạo runbooks cho incident response
  * Tài liệu hóa disaster recovery procedures
  * Thiết lập knowledge base cho team

* **Kết quả chính:**
  * CI/CD pipeline tự động hoàn toàn
  * CloudFront CDN phục vụ frontend globally
  * Infrastructure as Code hoàn chỉnh
  * Tài liệu toàn diện
  * Operational runbooks
  * Sẵn sàng cho final review và optimization ở Tuần 8