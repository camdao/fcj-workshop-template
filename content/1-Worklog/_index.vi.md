---
title: "Nhật ký công việc"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 1. </b> "
---

**Trang này** ghi lại toàn bộ nhật ký công việc trong 8 tuần thực tập AWS tại First Cloud Journey - AWS Study Group. Chương trình thực tập tập trung kết hợp học tập lý thuyết với phát triển dự án thực tế, bao quát các dịch vụ AWS thiết yếu và các phương pháp DevOps hiện đại.

Thực tập tập trung vào việc xây dựng **Ứng dụng Web Cloud-Native** sử dụng các dịch vụ AWS, triển khai các best practices về bảo mật, khả năng mở rộng và tối ưu hóa chi phí.

## Tổng quan các tuần

**Tuần 1:** [Nền tảng AWS, Bảo mật & Mạng](1.1-week1/)
- Tổng quan nền tảng AWS, bảo mật IAM, quản lý chi phí AWS Budgets
- Mạng VPC, subnets, security groups và routing cơ bản

**Tuần 2:** [Dịch vụ Compute, Giám sát & Khả năng mở rộng](1.2-week2/)
- Amazon EC2 instances và IAM roles
- Load balancing (ALB/NLB), Auto Scaling Groups
- Giám sát và cảnh báo CloudWatch

**Tuần 3:** [Dịch vụ Lưu trữ & Cơ sở dữ liệu](1.3-week3/)
- Lưu trữ Amazon S3, versioning và lifecycle policies
- Cơ sở dữ liệu quan hệ RDS (PostgreSQL/MySQL)
- DynamoDB NoSQL và chiến lược sao lưu

**Tuần 4:** [Lập kế hoạch Dự án, Docker & CI/CD cơ bản](1.4-week4/)
- Thiết kế và lập kế hoạch kiến trúc dự án
- Cơ bản về container hóa Docker
- Khái niệm CI/CD pipeline và best practices bảo mật AWS

**Tuần 5:** [Phát triển Ứng dụng & Triển khai Container](1.5-week5/)
- Phát triển ứng dụng web demo với backend API
- Tạo Dockerfiles và container images
- Triển khai lên Amazon ECS sử dụng ECR

**Tuần 6:** [Môi trường Staging & Kiểm thử Hệ thống](1.6-week6/)
- Thiết lập môi trường staging
- Giám sát CloudWatch nâng cao (logs, metrics, alarms)
- Kiểm thử ứng dụng và load testing

**Tuần 7:** [CI/CD Pipeline & Phân phối Nội dung](1.7-week7/)
- Xây dựng CI/CD pipeline tự động (GitHub Actions/CodePipeline)
- Triển khai CloudFront CDN
- Infrastructure as Code với CloudFormation
- Tài liệu và runbooks

**Tuần 8:** [Rà soát Hệ thống & Hoàn thiện Dự án](1.8-week8/)
- Rà soát và tối ưu hóa hệ thống toàn diện
- Phân tích và tối ưu hóa chi phí
- Kiểm thử cuối cùng và đảm bảo chất lượng
- Trình bày dự án và chuyển giao kiến thức

## Dự án Capstone

Trong suốt thời gian thực tập, công việc tập trung vào xây dựng **Ứng dụng Web Microservices Cloud-Native** minh họa:

- **Frontend**: Website tĩnh (React/Vue) host trên S3 với CloudFront CDN
- **Backend**: Microservices được container hóa chạy trên Amazon ECS
- **Database**: RDS cho dữ liệu quan hệ + DynamoDB cho sessions/caching
- **CI/CD**: Pipeline triển khai tự động với các giai đoạn testing
- **Monitoring**: Dashboards và alerting CloudWatch toàn diện
- **Security**: IAM roles, security groups, mã hóa SSL/TLS và AWS best practices
- **Quản lý Chi phí**: Cảnh báo ngân sách và tối ưu hóa tài nguyên

Dự án thực hành này tích hợp tất cả các khái niệm đã học vào kiến trúc ứng dụng production-ready.