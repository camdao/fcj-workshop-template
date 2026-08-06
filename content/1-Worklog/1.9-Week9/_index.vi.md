---
title: "Worklog Tuần 9"
date: 2024-01-01
weight: 9
chapter: false
pre: " <b> 1.9. </b> "
---

### Mục tiêu tuần 9:

* Nắm vững AWS Lambda và serverless computing.
* Hiểu về API Gateway cho building APIs.
* Tìm hiểu các mẫu event-driven architecture.
* Thực hành xây dựng serverless applications.

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc                                                                                                                                                                                   | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu                            |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------ | --------------- | ----------------------------------------- |
| 2   | - Tìm hiểu Lambda Fundamentals: <br>&emsp; + Các khái niệm Serverless <br>&emsp; + Lambda functions và runtimes <br>&emsp; + Execution model và pricing <br>&emsp; + Cold starts và warm starts | 06/08/2026   | 06/08/2026      | <https://cloudjourney.awsstudygroup.com/> |
| 3   | - Tìm hiểu Lambda Features: <br>&emsp; + Environment variables <br>&emsp; + Layers và dependencies <br>&emsp; + Concurrency và scaling <br>&emsp; + Error handling và retries             | 07/08/2026   | 07/08/2026      | <https://cloudjourney.awsstudygroup.com/> |
| 4   | - **Thực hành:** <br>&emsp; + Tạo Lambda functions <br>&emsp; + Cấu hình triggers <br>&emsp; + Triển khai error handling <br>&emsp; + Test và debug functions                             | 08/08/2026   | 08/08/2026      | <https://cloudjourney.awsstudygroup.com/> |
| 5   | - Tìm hiểu API Gateway: <br>&emsp; + REST vs. HTTP APIs <br>&emsp; + API design và resources <br>&emsp; + Authorization và authentication <br>&emsp; + API stages và deployments          | 09/08/2026   | 09/08/2026      | <https://cloudjourney.awsstudygroup.com/> |
| 6   | - **Thực hành:** <br>&emsp; + Xây dựng REST API với API Gateway <br>&emsp; + Tích hợp với Lambda <br>&emsp; + Cấu hình CORS <br>&emsp; + Triển khai API authentication                    | 10/08/2026   | 10/08/2026      | <https://cloudjourney.awsstudygroup.com/> |


### Kết quả đạt được tuần 9:

* Nắm vững kiến thức cơ bản về AWS Lambda:
  * Hiểu lợi ích của serverless computing
  * Lambda execution model và lifecycle
  * Các runtimes được hỗ trợ (Node.js, Python, Java, Go, v.v.)
  * Mô hình giá pay-per-use

* Tìm hiểu về Lambda configuration:
  * Function code và handler
  * Cài đặt memory và timeout
  * Environment variables cho configuration
  * IAM execution roles và permissions

* Thành công trong việc tạo Lambda functions:
  * Viết functions với nhiều runtimes
  * Cấu hình triggers (S3, DynamoDB, EventBridge, v.v.)
  * Triển khai error handling và retries
  * Sử dụng Lambda Layers cho shared code

* Hiểu về Lambda performance:
  * Cold starts vs. warm starts
  * Provisioned concurrency
  * Reserved concurrency cho throttling
  * Các kỹ thuật optimization

* Nắm vững kiến thức cơ bản về API Gateway:
  * So sánh REST API vs. HTTP API
  * Nguyên tắc thiết kế API
  * Resources, methods và stages
  * API deployment và versioning

* Tìm hiểu về API Gateway features:
  * Request/response transformations
  * API keys và usage plans
  * Request validation
  * Caching và throttling

* Thành công trong việc xây dựng serverless APIs:
  * Tạo REST APIs với nhiều endpoints
  * Tích hợp với Lambda functions
  * Cấu hình CORS cho web applications
  * Triển khai authentication (IAM, Cognito, Lambda authorizers)

* Hiểu về event-driven architecture:
  * Event sources và triggers
  * Asynchronous vs. synchronous invocation
  * EventBridge cho event routing
  * Step Functions cho workflow orchestration

* Có kinh nghiệm thực tế với:
  * Serverless application development
  * API design và implementation
  * Performance optimization
  * Cost management cho serverless

* Tìm hiểu các best practices về serverless:
  * Nguyên tắc single responsibility
  * Idempotency cho reliability
  * Monitoring và logging
  * Security và least privilege

* Xây dựng kiến thức nền tảng cho việc xây dựng serverless applications có khả năng mở rộng và cost-effective trên AWS.