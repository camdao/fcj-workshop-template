---
title : "Giới thiệu"
date : 2024-01-01 
weight : 1
chapter : false
pre : " <b> 5.1. </b> "
---

# 5.1. Tổng quan
# Bài toán Cloud & DevOps: Đưa hệ thống lên AWS Cloud, xây dựng luồng CI/CD tự động

Nhằm đáp ứng yêu cầu về khả năng triển khai linh hoạt, tự động hóa quy trình phát hành phần mềm và nâng cao tính sẵn sàng của hệ thống, đề tài thực hiện triển khai ứng dụng trên nền tảng Amazon Web Services (AWS) và xây dựng quy trình CI/CD (Continuous Integration/Continuous Deployment) theo mô hình tự động hóa hoàn toàn. Kiến trúc Cloud & DevOps của hệ thống được tổ chức thành ba luồng xử lý chính, bao gồm: luồng CI/CD, luồng xử lý yêu cầu người dùng và luồng giám sát – quản lý chi phí.

## 5.1.1. Luồng CI/CD (Pipeline Flow)
Quy trình tích hợp và triển khai liên tục được thiết kế nhằm tự động hóa toàn bộ quá trình từ khi lập trình viên cập nhật mã nguồn đến khi phiên bản mới của ứng dụng được triển khai trên môi trường vận hành.	Cụ thể, khi Developer thực hiện thao tác push code lên kho mã nguồn GitHub, GitHub Actions sẽ được kích hoạt để khởi chạy pipeline. Pipeline sử dụng cơ chế xác thực OIDC (OpenID Connect) để liên kết với AWS Security Token Service (STS) và cấp phát thông tin xác thực tạm thời (temporary credentials), thay thế cho việc sử dụng Access Key/Secret Key tĩnh nhằm mục đích tăng cường mức độ an toàn bảo mật. Sau khi xác thực thành công, pipeline tiến hành build Docker image của ứng dụng và đẩy image lên Amazon Elastic Container Registry (ECR). Tiếp theo, dịch vụ Amazon ECS Fargate sẽ tự động pull image mới nhất từ ECR và thực hiện triển khai phiên bản mới của ứng dụng mà không cần can thiệp thủ công. Luồng xử lý được mô tả như sau:
Developer → GitHub → GitHub Actions → OIDC Authentication → AWS STS → Amazon ECR → Amazon ECS Fargate.

## 5.1.2. Luồng User (Request Flow)
Luồng xử lý yêu cầu được xây dựng theo mô hình phân phối nội dung và cân bằng tải nhằm đảm bảo hiệu năng truy cập và khả năng chịu lỗi của hệ thống.
Khi người dùng (User) gửi yêu cầu truy cập, yêu cầu trước tiên được tiếp nhận bởi Amazon CloudFront – mạng phân phối nội dung (CDN) của AWS. Đối với các tài nguyên tĩnh của giao diện người dùng, CloudFront sẽ truy xuất trực tiếp từ Amazon S3 Frontend Bucket. Đối với các yêu cầu động, CloudFront chuyển tiếp yêu cầu đến Application Load Balancer (ALB). ALB có nhiệm vụ phân phối lưu lượng truy cập đến các tác vụ ECS Fargate đang chạy trên hai Availability Zone (AZ) khác nhau nhằm đảm bảo tính sẵn sàng cao (High Availability). Các container ứng dụng kết nối đến Amazon RDS Primary đặt tại Zone A để thực hiện thao tác đọc/ghi dữ liệu. Đồng thời, dữ liệu được đồng bộ liên tục sang RDS Standby tại Zone B theo cơ chế Multi-AZ, giúp hệ thống có khả năng chuyển đổi dự phòng khi xảy ra sự cố.
Ngoài ra, các container ECS truy cập S3 Media Bucket thông qua VPC Endpoint, cho phép truyền dữ liệu nội bộ trong mạng AWS mà không cần đi qua Internet công cộng, từ đó tăng cường bảo mật và tối ưu chi phí truyền tải dữ liệu. Luồng xử lý được mô tả như sau:
User → CloudFront → (S3 Frontend hoặc ALB) → ECS Fargate (2 AZ) → RDS Primary (Zone A) → RDS Standby (Zone B)

## 5.1.3. Luồng Giám sát & Chi phí (Observability & Billing)
Để đảm bảo hệ thống vận hành ổn định và kiểm soát hiệu quả chi phí sử dụng tài nguyên đám mây, đề tài triển khai cơ chế giám sát và cảnh báo tự động dựa trên các dịch vụ quản trị của AWS. Toàn bộ nhật ký hệ thống (logs), bao gồm VPC Flow Logs và Application Logs, được thu thập và tập trung tại Amazon CloudWatch để phục vụ việc theo dõi, phân tích và xử lý sự cố. Hệ thống đồng thời được cấu hình Auto Scaling cho dịch vụ ECS, cho phép tự động mở rộng số lượng tác vụ khi mức sử dụng CPU hoặc Memory vượt quá 70%, qua đó duy trì hiệu năng trong điều kiện tải tăng cao.
Về quản lý chi phí, hệ thống sử dụng AWS Budgets với ngân sách được thiết lập ở mức 15 USD/tháng. Các ngưỡng cảnh báo được cấu hình tại 50%, 70% và 90% ngân sách. Khi chi phí đạt đến các ngưỡng này hoặc xuất hiện dấu hiệu gia tăng chi phí bất thường, AWS Budgets sẽ tự động kích hoạt Amazon SNS (Simple Notification Service) để gửi email cảnh báo đến quản trị viên, hỗ trợ phát hiện sớm rủi ro và đưa ra biện pháp xử lý kịp thời. Luồng giám sát và cảnh báo được mô tả như sau:
CloudWatch (Logs & Metrics) → Auto Scaling → AWS Budgets → Amazon SNS → Email Alert

## 5.1.4. Kế hoạch triển khai
#### Dự Án: NeonFoodmap - AWS Multi-AZ Deployment, CI/CD Pipeline

Timeline: 3 Sprints / 3 tuần (Ngày 1-20)
Team: 5 thành viên
1. Diệp Thụy An - 3122410001 
2. Trương Gia Hào - 3122410100 
3. Lương Tuấn Giai - 3122410092
4. Lương Cẩm Đào - 3122410067 
5. Bùi Bảo Long - 3122410214 

#### Chi tiết kế hoạch triển khai
#### Sprint 1 – Foundation

Mục tiêu:

- Thiết lập hạ tầng AWS.

Bao gồm:

- IAM
- VPC
- S3
- RDS
- ECR

---

#### Sprint 2 – Deployment

Mục tiêu:

Triển khai ứng dụng.

Bao gồm:

- GitHub Actions
- ECS Cluster
- Backend
- Frontend
- CI/CD Pipeline

---

#### Sprint 3 – Operation

Mục tiêu:

Hoàn thiện môi trường Production.

Bao gồm:

- Logging
- Monitoring
- Alert
- Auto Scaling
- Documentation

---

## 5.1.5 Kiến trúc hệ thống

### Kiến trúc tổng thể

![](/images/2-Proposal/diagram1.png)

Kiến trúc hệ thống được chia thành năm lớp chính:

#### CI/CD Layer

- GitHub Repository
- GitHub Actions
- Docker Build
- AWS STS
- Amazon ECR

Đây là lớp chịu trách nhiệm tự động hóa toàn bộ quy trình triển khai.

Sau mỗi lần Push lên nhánh chính:

1. Source Code được Build.
2. Docker Image được tạo.
3. GitHub sử dụng OIDC để xác thực.
4. AWS STS cấp Temporary Credential.
5. Image được Push lên Amazon ECR.
6. ECS Service thực hiện Rolling Deployment.

---

#### Presentation Layer

Bao gồm:

- Amazon CloudFront
- Amazon S3 Static Website

Frontend được lưu trữ trên Amazon S3 và phân phối thông qua CloudFront nhằm:

- giảm độ trễ
- tăng tốc truy cập
- giảm tải Backend

---

#### Application Layer

Bao gồm:

- Application Load Balancer
- Amazon ECS Cluster
- Backend Service
- Frontend Service

Ứng dụng được triển khai trên ECS Fargate giúp loại bỏ việc quản lý EC2.

Các Service hoạt động độc lập giúp:

- mở rộng riêng từng thành phần
- Rolling Update
- tự động khởi động lại khi lỗi

---

#### Data Layer

Bao gồm:

- Amazon RDS MySQL
- Multi-AZ Deployment

Database được triển khai trong Private Database Subnet.

Việc sử dụng Multi-AZ giúp:

- tăng khả năng chịu lỗi
- tự động Failover
- giảm thời gian gián đoạn dịch vụ

---

#### Monitoring Layer

Bao gồm:

- Amazon CloudWatch
- Amazon SNS

CloudWatch thu thập:

- ECS Logs
- Container Logs
- Metrics
- Application Logs

SNS chịu trách nhiệm gửi Email Alert khi phát hiện bất thường.

---

### Kiến trúc triển khai ECS

![](/images/2-Proposal/diagram2.png)

Hệ thống sử dụng một ECS Cluster gồm hai dịch vụ:

#### Backend Service

Triển khai:

- Django REST API
- Docker Container
- ECS Fargate

Backend chịu trách nhiệm:

- Authentication
- Business Logic
- Database Access
- Upload Media

---

#### Frontend Service

Triển khai:

- React Application
- Docker Container
- ECS Fargate

Frontend giao tiếp với Backend thông qua ALB.

---

#### Service Discovery

AWS Cloud Map được sử dụng để quản lý Service Discovery giữa các Container trong ECS Cluster.

---

#### Load Balancing

Application Load Balancer tiếp nhận:

- HTTP Request
- HTTPS Request

Sau đó định tuyến đến Backend Service.

---

## 5.1.6. Thành phần AWS sử dụng

| Dịch vụ | Mục đích |
|----------|----------|
| IAM | Quản lý phân quyền |
| STS | Temporary Credential |
| VPC | Mạng riêng |
| Public / Private Subnet | Phân tách vùng mạng |
| NAT Gateway | Internet cho Private Subnet |
| Internet Gateway | Truy cập Internet |
| ECS Fargate | Chạy Container |
| ECR | Lưu Docker Image |
| RDS MySQL | Database |
| S3 | Static Website, Media, Logs |
| CloudFront | CDN |
| ALB | Load Balancer |
| CloudWatch | Monitoring |
| SNS | Notification |
| Secrets Manager | Quản lý Secret |

---

## 5.1.6 Quy trình triển khai

Quy trình triển khai của hệ thống như sau:

1. Developer Push Source Code.
2. GitHub Actions Trigger Workflow.
3. Build Docker Image.
4. Authenticate thông qua AWS STS.
5. Push Image lên Amazon ECR.
6. ECS Pull Image.
7. ECS Rolling Update.
8. ALB chuyển tiếp Request.
9. Backend truy cập RDS.
10. Media Upload tới Amazon S3.
11. CloudWatch thu thập Logs.
12. SNS gửi Email khi xảy ra sự cố.

---