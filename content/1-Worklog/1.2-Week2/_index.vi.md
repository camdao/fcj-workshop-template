---
title: "Worklog Tuần 2"
date: 2024-01-08
weight: 2
chapter: false
pre: " <b> 1.2. </b> "
---

### Mục tiêu tuần 2:

* Thành thạo kiến thức cơ bản về Amazon EC2 và quản lý instances.
* Hiểu IAM roles cho EC2 và áp dụng nguyên tắc least privilege.
* Học khái niệm load balancing với Application Load Balancer (ALB) và Network Load Balancer (NLB).
* Triển khai Auto Scaling Groups cho high availability và elasticity.
* Thiết lập giám sát và cảnh báo toàn diện với CloudWatch.

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc                                                                                                                                                                                   | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu                            |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------ | --------------- | ----------------------------------------- |
| 1   | - Học EC2 cơ bản: <br>&emsp; + Các loại instance và families (t3, m5, c5, r5, etc.) <br>&emsp; + AMI (Amazon Machine Images) <br>&emsp; + Tùy chọn lưu trữ (EBS volumes, instance store) <br>&emsp; + Key pairs và SSH access <br> - **Thực hành:** <br>&emsp; + Khởi chạy EC2 instances <br>&emsp; + Kết nối qua SSH <br>&emsp; + Quản lý EBS volumes | 18/06/2026   | 18/06/2026      | <https://000004.awsstudygroup.com/> |
| 2   | - Học IAM Roles cho EC2: <br>&emsp; + Service roles vs user roles <br>&emsp; + EC2 instance profiles <br>&emsp; + Temporary credentials qua metadata service <br>&emsp; + Best practices cho service access <br> - **Thực hành:** <br>&emsp; + Tạo IAM role cho EC2 <br>&emsp; + Gắn role vào instance <br>&emsp; + Test AWS CLI từ instance không cần access keys | 19/06/2026   | 19/06/2026      | <https://000008.awsstudygroup.com/> |
| 3   | - Học về Load Balancers: <br>&emsp; + Application Load Balancer (ALB) - Layer 7 <br>&emsp; + Network Load Balancer (NLB) - Layer 4 <br>&emsp; + Target groups và health checks <br>&emsp; + Listener rules và routing <br> - **Thực hành:** <br>&emsp; + Tạo ALB <br>&emsp; + Cấu hình target group <br>&emsp; + Thiết lập health checks <br>&emsp; + Test phân phối tải | 20/06/2026   | 20/06/2026      | <https://000045.awsstudygroup.com/> |
| 4   | - Học Auto Scaling: <br>&emsp; + Launch templates <br>&emsp; + Auto Scaling Groups (ASG) <br>&emsp; + Scaling policies (target tracking, step, simple) <br>&emsp; + Desired, minimum, maximum capacity <br> - **Thực hành:** <br>&emsp; + Tạo launch template <br>&emsp; + Thiết lập Auto Scaling Group <br>&emsp; + Cấu hình scaling policies <br>&emsp; + Test scale-out và scale-in | 21/06/2026   | 21/06/2026      | <https://000047.awsstudygroup.com/> |
| 5   | - Học CloudWatch monitoring: <br>&emsp; + Metrics (built-in và custom) <br>&emsp; + Logs và log groups <br>&emsp; + Alarms và notifications <br>&emsp; + Dashboards <br>&emsp; + CloudWatch Agent <br> - **Thực hành:** <br>&emsp; + Thiết lập CloudWatch alarms <br>&emsp; + Tạo custom metrics <br>&emsp; + Cấu hình log aggregation <br>&emsp; + Xây dựng monitoring dashboard | 22/06/2026   | 22/06/2026      | <https://000051.awsstudygroup.com/> |


### Kết quả đạt được tuần 2:

* **Thành thạo Amazon EC2:**
  * Hiểu các loại EC2 instance và tiêu chí lựa chọn:
    * General Purpose (t3, t3a, m5) - cân bằng compute, memory, network
    * Compute Optimized (c5, c6i) - bộ xử lý hiệu suất cao
    * Memory Optimized (r5, r6i) - cho ứng dụng tiêu tốn memory
    * Storage Optimized (i3, d2) - IOPS và throughput cao
  * Học vòng đời EC2 instance:
    * Launch, start, stop, terminate, reboot
    * Các trạng thái instance và ảnh hưởng đến billing
  * Thành thạo các tùy chọn lưu trữ:
    * EBS volumes (gp3, gp2, io2, st1, sc1)
    * Instance store (ephemeral storage)
    * EBS snapshots và chiến lược backup
  * Thực hành quản lý instance:
    * Khởi chạy nhiều EC2 instances trong VPC từ Tuần 1
    * Cấu hình security groups cho web và app tiers
    * Tạo và quản lý SSH key pairs
    * Kết nối đến instances sử dụng SSH và Session Manager
    * Gắn và mount EBS volumes
    * Tạo EBS snapshots để backup
  * Hiểu khái niệm AMI:
    * AMIs công khai, riêng tư và được chia sẻ
    * Tạo custom AMIs từ instances
    * Vòng đời AMI và deregistration

* **IAM Roles cho EC2:**
  * Hiểu sâu về service roles:
    * Khác biệt giữa IAM users và IAM roles
    * Cách EC2 lấy temporary credentials qua instance metadata
    * Instance profiles (container cho IAM role)
  * Best practices cho EC2 security:
    * Không bao giờ hardcode credentials trong applications
    * Sử dụng IAM roles cho mọi AWS API access
    * Tự động rotate credentials
    * Nguyên tắc least privilege cho role policies
  * Triển khai thực tế:
    * Tạo IAM role với S3 read-only access
    * Tạo IAM role với CloudWatch logging permissions
    * Gắn roles vào running instances
    * Test AWS CLI commands mà không cần cấu hình credentials
    * Xác minh temporary credentials qua metadata endpoint
  * Hiểu trust policies và permissions boundaries

* **Kiến trúc Load Balancing:**
  * Học các loại load balancer và use cases:
    * **Application Load Balancer (ALB):**
      * Layer 7 (HTTP/HTTPS) routing
      * Path-based và host-based routing
      * Hỗ trợ WebSocket và HTTP/2
      * Tích hợp với WAF cho bảo mật
    * **Network Load Balancer (NLB):**
      * Layer 4 (TCP/UDP) routing
      * Độ trễ cực thấp và throughput cao
      * Static IP addresses và hỗ trợ Elastic IP
      * Tích hợp PrivateLink
  * Hiểu các thành phần load balancer:
    * Listeners (cấu hình protocol và port)
    * Target groups (instances, IPs, Lambda functions)
    * Health checks (interval, timeout, threshold)
    * Routing rules và conditions
  * Triển khai load balancing thực tế:
    * Tạo ALB trong public subnets
    * Cấu hình target group với nhiều EC2 instances
    * Thiết lập health checks (HTTP GET /health)
    * Cấu hình listener rules cho các paths khác nhau
    * Test phân phối traffic giữa các instances
    * Giám sát target health trong console
  * Hiểu các tính năng nâng cao:
    * SSL/TLS termination
    * Sticky sessions (session affinity)
    * Connection draining
    * Cross-zone load balancing

* **Triển khai Auto Scaling:**
  * Thành thạo các khái niệm Auto Scaling:
    * Nguyên tắc elasticity và scalability
    * Horizontal scaling vs vertical scaling
    * Launch templates vs launch configurations
  * Học các thành phần scaling:
    * Launch template (AMI, instance type, user data, security groups)
    * Auto Scaling Group (desired, min, max capacity)
    * Scaling policies (khi nào và cách scale)
    * Cooldown periods
  * Hiểu các loại scaling policy:
    * Target tracking scaling (duy trì metric ở target value)
    * Step scaling (scale dựa trên kích thước breach metric)
    * Simple scaling (scale theo số lượng cố định)
    * Scheduled scaling (các patterns có thể dự đoán)
  * Triển khai Auto Scaling production-ready:
    * Tạo launch template với web application
    * Cấu hình Auto Scaling Group với min=2, max=6, desired=2
    * Thiết lập target tracking policy (CPU utilization ở 70%)
    * Tích hợp ASG với ALB target group
    * Cấu hình health checks (EC2 + ELB)
    * Test tự động scale-out dưới tải
    * Test tự động scale-in sau khi tải giảm
    * Xác minh zero-downtime trong quá trình scaling
  * Hiểu ASG best practices:
    * Phân phối Multi-AZ cho high availability
    * Sử dụng nhiều instance types để tối ưu chi phí
    * Health check grace period phù hợp
    * Instance protection cho updates có kiểm soát

* **CloudWatch Monitoring & Observability:**
  * Học các thành phần CloudWatch:
    * **Metrics:** Điểm dữ liệu time-series
      * Default EC2 metrics (CPU, Network, Disk)
      * Custom metrics qua PutMetricData API
      * Metric resolution (standard 5-phút, high-resolution 1-giây)
    * **Logs:** Tập hợp log tập trung
      * Log groups và log streams
      * Log retention policies
      * Log Insights để query
    * **Alarms:** Thông báo tự động
      * Metric alarms (dựa trên ngưỡng)
      * Composite alarms (kết hợp nhiều alarms)
      * Alarm actions (SNS, Auto Scaling, EC2 actions)
    * **Dashboards:** Biểu diễn trực quan metrics
  * Triển khai monitoring toàn diện:
    * Tạo CloudWatch alarms cho các metrics quan trọng:
      * CPU utilization cao (>80% trong 5 phút)
      * Memory available thấp (custom metric)
      * Disk usage cao
      * ALB unhealthy target count
      * ALB 5XX errors
    * Thiết lập SNS topics cho alarm notifications
    * Subscribe email addresses vào SNS topics
    * Cài đặt CloudWatch Agent trên EC2 instances
    * Cấu hình agent thu thập:
      * Memory utilization
      * Disk space utilization
      * Custom application metrics
    * Thiết lập log aggregation:
      * Application logs vào CloudWatch Logs
      * System logs (syslog, auth.log)
      * Web server access và error logs
    * Tạo CloudWatch dashboard hiển thị:
      * EC2 instance metrics
      * ALB metrics
      * ASG metrics
      * Custom application metrics
    * Sử dụng CloudWatch Logs Insights để phân tích log
  * Hiểu CloudWatch best practices:
    * Thiết lập ngưỡng alarm phù hợp
    * Sử dụng composite alarms để giảm nhiễu
    * Triển khai log retention policies
    * Tag resources để phân bổ chi phí

* **Thành tựu Kiến trúc Tích hợp:**
  * Xây dựng thành công compute tier hoàn chỉnh, production-ready:
    * Triển khai Multi-AZ với Auto Scaling
    * Application Load Balancer phân phối traffic
    * Health checks đảm bảo chỉ healthy instances phục vụ traffic
    * Tự động scaling dựa trên demand
    * Monitoring và alerting toàn diện
    * Truy cập an toàn sử dụng IAM roles (không có hardcoded credentials)
  * Test chức năng end-to-end:
    * Deploy sample web application
    * Xác minh load balancing giữa các instances
    * Mô phỏng high load để trigger scale-out
    * Xác minh instances mới tự động thêm vào ALB
    * Xác nhận alarms kích hoạt đúng cách
    * Test instance failure và tự động replacement

* **Điểm chính rút ra:**
  * Có thể thiết kế và triển khai ứng dụng highly available, auto-scaling
  * Hiểu cách bảo mật EC2 instances đúng cách sử dụng IAM roles
  * Biết cách triển khai chiến lược load balancing hiệu quả
  * Có thể thiết lập monitoring và alerting production-grade
  * Sẵn sàng xây dựng ứng dụng resilient xử lý traffic biến đổi
  * Chuẩn bị cho các dịch vụ storage và database tuần tới