---
title: "Worklog Tuần 6"
date: 2024-01-01
weight: 6
chapter: false
pre: " <b> 1.6. </b> "
---

### Mục tiêu tuần 6:

* Nắm vững các khái niệm và loại Elastic Load Balancing (ELB).
* Hiểu về Auto Scaling cho quản lý tài nguyên động.
* Tìm hiểu các mẫu high availability và fault tolerance.
* Thực hành xây dựng kiến trúc có khả năng mở rộng và bền vững.

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc                                                                                                                                                                                   | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu                            |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------ | --------------- | ----------------------------------------- |
| 2   | - Tìm hiểu ELB Fundamentals: <br>&emsp; + Các khái niệm load balancing <br>&emsp; + Application Load Balancer (ALB) <br>&emsp; + Network Load Balancer (NLB) <br>&emsp; + Gateway Load Balancer (GWLB) | 16/07/2026   | 16/07/2026      | <https://cloudjourney.awsstudygroup.com/> |
| 3   | - Tìm hiểu ELB Features: <br>&emsp; + Target groups <br>&emsp; + Health checks <br>&emsp; + Listener rules và routing <br>&emsp; + SSL/TLS termination                                    | 17/07/2026   | 17/07/2026      | <https://cloudjourney.awsstudygroup.com/> |
| 4   | - **Thực hành:** <br>&emsp; + Tạo ALB và NLB <br>&emsp; + Cấu hình target groups <br>&emsp; + Thiết lập health checks <br>&emsp; + Cấu hình routing rules                                 | 18/07/2026   | 18/07/2026      | <https://cloudjourney.awsstudygroup.com/> |
| 5   | - Tìm hiểu Auto Scaling: <br>&emsp; + Auto Scaling Groups (ASG) <br>&emsp; + Launch templates <br>&emsp; + Scaling policies (target tracking, step, scheduled) <br>&emsp; + Lifecycle hooks | 19/07/2026   | 19/07/2026      | <https://cloudjourney.awsstudygroup.com/> |
| 6   | - **Thực hành:** <br>&emsp; + Tạo Auto Scaling Groups <br>&emsp; + Cấu hình scaling policies <br>&emsp; + Tích hợp với Load Balancers <br>&emsp; + Kiểm tra scaling behavior               | 20/07/2026   | 20/07/2026      | <https://cloudjourney.awsstudygroup.com/> |


### Kết quả đạt được tuần 6:

* Nắm vững kiến thức cơ bản về Elastic Load Balancing:
  * Hiểu các khái niệm và lợi ích của load balancing
  * Application Load Balancer (Layer 7) cho HTTP/HTTPS traffic
  * Network Load Balancer (Layer 4) cho TCP/UDP traffic
  * Gateway Load Balancer cho third-party virtual appliances
  * Lựa chọn loại load balancer phù hợp

* Tìm hiểu các thành phần và tính năng của ELB:
  * Target groups cho routing traffic đến instances
  * Health checks để giám sát target health
  * Listener rules cho routing dựa trên điều kiện
  * SSL/TLS termination và quản lý certificate
  * Cross-Zone load balancing

* Thành công trong việc cấu hình load balancers:
  * Tạo Application Load Balancers với nhiều target groups
  * Thiết lập Network Load Balancers cho high-performance workloads
  * Cấu hình health checks với ngưỡng phù hợp
  * Triển khai path-based và host-based routing
  * Thiết lập SSL/TLS certificates với ACM

* Hiểu về bảo mật load balancer:
  * Security groups cho load balancers
  * Tích hợp AWS WAF cho application protection
  * Access logs cho auditing và troubleshooting
  * Connection draining và deregistration delay

* Nắm vững kiến thức cơ bản về Auto Scaling:
  * Các khái niệm Auto Scaling Groups (ASG)
  * Launch templates và launch configurations
  * Desired, minimum và maximum capacity
  * Phân bổ instance qua các Availability Zones

* Tìm hiểu về Auto Scaling policies:
  * Target tracking scaling (duy trì metric ở mức target)
  * Step scaling (scale dựa trên CloudWatch alarms)
  * Scheduled scaling (predictable load patterns)
  * Predictive scaling (ML-based forecasting)

* Thành công trong việc triển khai Auto Scaling:
  * Tạo Auto Scaling Groups với launch templates
  * Cấu hình target tracking policies cho CPU utilization
  * Thiết lập step scaling policies với CloudWatch alarms
  * Tích hợp ASG với load balancers
  * Triển khai lifecycle hooks cho custom actions

* Có kinh nghiệm thực tế với:
  * Thiết kế kiến trúc high availability
  * Các mẫu fault tolerance và resilience
  * Tối ưu chi phí thông qua dynamic scaling
  * Load testing và performance validation

* Hiểu các best practices về scaling:
  * Warm-up và cooldown periods
  * Health check grace period
  * Instance protection trong maintenance
  * Lựa chọn scaling metrics

* Xây dựng kiến thức nền tảng cho việc xây dựng ứng dụng có tính sẵn sàng cao, fault-tolerant và cost-effective trên AWS.