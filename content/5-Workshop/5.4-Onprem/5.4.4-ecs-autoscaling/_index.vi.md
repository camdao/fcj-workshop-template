---
title: "ECS Fargate và ALB"
date: 2026-08-03
weight: 4
chapter: false
pre: " <b> 5.4.4. </b> "
---
Sau khi pipeline GitHub Actions đã sẵn sàng, mục này triển khai **NeonFoodMap backend** trên Amazon ECS Fargate. Backend chạy trong private subnet; Application Load Balancer (ALB) nhận lưu lượng Internet, thực hiện health check và định tuyến request API đến backend service.

## Tạo ECS Cluster và Task Definition

NeonFoodMap sử dụng **Amazon ECS Fargate** để chạy backend Django API, do đó đội dự án chỉ quản lý container và cấu hình task, không phải vận hành EC2 host. Frontend React SPA được build tĩnh và phân phối qua S3/CloudFront (xem [mục 5.4.5](../5.4.5-cloudfront-delivery/)).


### Tạo ECS Cluster

1. Mở **Amazon ECS Console**, chọn **Clusters** ở thanh điều hướng bên trái và nhấn **Create cluster**.
2. Nhập tên cluster `NeonFoodmap-cluster`; chọn hạ tầng serverless **AWS Fargate**.

![picCreateCluster1](images/picCreateCluster1.jpg)

![picCreateCluster2](images/picCreateCluster2.jpg)

### Tạo Backend Task Definition

1. Trong ECS, chọn **Task definitions → Create new task definition**.
2. Chọn **AWS Fargate**, *Operating system/Architecture* là **Linux/X86_64**. Nhập *Task definition family* là `neonfoodmap-task-be`.  ![picCreateNewTaskDefinition12](images/picCreateNewTaskDefinition12.jpg)
3. Chọn **Task CPU** `256` và **Task memory** `512 MiB`. Gán `NeonFoodmap-ECS-TaskExecution-Role` tại *Task execution role* để ECS pull image từ ECR và ghi log; gán `NeonFoodmap-ECS-Backend-Role` tại *Task role* cho quyền mà ứng dụng backend cần sử dụng.
4. Thêm container backend, chọn image từ ECR repository `neonfoodmap-backend` và khai báo *Container port* `8000` với protocol TCP. ![picCreateNewTaskDefinition4](images/picCreateNewTaskDefinition4.jpg) ![picCreateNewTaskDefinition42](images/picCreateNewTaskDefinition42.jpg)
5. Khai báo các biến cần thiết cho task definition. Với thông tin password quan trọng chọn ValueFrom để đọc từ AWS Secrets Manager. ![picCreateNewTaskDefinition5](images/picCreateNewTaskDefinition5.jpg)
6. Trong phần logging, chọn CloudWatch Logs, tạo/chọn log group `/ecs/neonfoodmap-backend` và region `ap-southeast-1`. Thiết lập log retention theo chính sách dự án. ![picCreateNewTaskDefinition6](images/picCreateNewTaskDefinition6.jpg)
7. Nhấn **Create** để đăng ký revision.

![FinalBakend1](images/FinalBakend1.jpg)

![FinalBakend2](images/FinalBakend2.jpg)

## Tạo Application Load Balancer

ALB được đặt trong hai public subnet, nhận lưu lượng Internet và chỉ chuyển tiếp request API vào backend ECS task trong private subnet. Lớp phân tách này giúp backend không nhận truy cập trực tiếp từ Internet.

### Tạo Security Group cho ALB

1. Mở **EC2 Console → Security Groups → Create security group**.
2. Đặt tên `alb-sg`, mô tả *Security Group cho Public Application Load Balancer* và chọn VPC của dự án.
3. Thêm hai inbound rule: **HTTP / 80 / Anywhere-IPv4 (`0.0.0.0/0`)** và **HTTPS / 443 / Anywhere-IPv4 (`0.0.0.0/0`)**. ![picALBSecutiryGroup](images/picALBSecutiryGroup.jpg)
4. Giữ outbound rule mặc định để ALB có thể gửi request tới ECS task, sau đó chọn **Create security group**. ![picALBSGOutbound](images/picALBSGOutbound.jpg)

Security group của ECS task cấu hình theo chiều ngược lại: chỉ cho phép port `8000` của backend có source là `alb-sg`; không mở port này cho `0.0.0.0/0`. ![picECS_SG](images/picECS_SG.jpg)

### Tạo Target Group và Health Check

ECS Fargate cấp private IP cho task, vì vậy target group phải dùng **Target type: IP addresses**. Không cần đăng ký IP thủ công vì ECS service sẽ tự đăng ký/deregister task khi deploy.

1. Vào **EC2 Console → Target Groups → Create target group** và tạo target group backend với cấu hình sau. ![picTG_HC1](images/picTG_HC1.jpg)

| Trường                      | Giá trị backend      |
| ----------------------------- | ---------------------- |
| Target group name             | `TG-NeonFoodMap-BE`  |
| Target type                   | **IP addresses** |
| Protocol / Port               | HTTP /`8000`         |
| Health check path             | `/api/health/`       |
| Healthy / Unhealthy threshold | `2` / `2`          |
| Health check interval         | `30 seconds`         |

2. Chọn **Next**, bỏ qua bước đăng ký target IP và chọn **Create target group**. ![picTG_HC2](images/picTG_HC2.jpg)

![picTG_HC_Final](images/picTG_HC_Final.jpg)

### Tạo ALB và Listener

1. Vào **EC2 Console → Load Balancers → Create load balancer**, chọn **Application Load Balancer**.
2. Nhập tên `ALB-NeonFoodMap`, chọn *Scheme* **Internet-facing** và *IP address type* **IPv4**. ![picALBCreate1](images/picALBCreate1.jpg)
3. Chọn VPC của dự án. Trong *Network mapping*, chọn đủ hai Availability Zone và hai **public subnet** có route đến Internet Gateway. ![picALBCreate2](images/picALBCreate2.jpg)
4. Bỏ chọn default security group, sau đó chọ `alb-sg` đã tạo.
5. Tạo listener **HTTP : 80**. Ở *Default action*, chọn **Forward to** `TG-NeonFoodMap-BE`, rồi nhấn **Create load balancer**. ![picALBCreate3](images/picALBCreate3.jpg)

![picALBCreate4](images/picALBCreate4.jpg)

ALB được cấu hình với default action forward tới backend target group. Tất cả request API được chuyển đến backend service trong ECS. Frontend được phân phối qua CloudFront/S3, không qua ALB. Khi triển khai HTTPS, thêm listener `443` gắn ACM certificate và chuyển hướng listener `80` sang HTTPS.

![picALBFinal2](images/picALBFinal2.jpg)

![picALBFinal3](images/picALBFinal3.jpg)

## Tạo ECS Service và liên kết Target Group

Sau khi có backend task definition, target group và ALB, tạo ECS service để ECS tự quản lý vòng đời task và đăng ký private IP vào target group.

### Tạo Backend Service

1. Mở **ECS → Clusters → NeonFoodmap-cluster → Create service**.
2. Chọn task definition family `neonfoodmap-task-be`, đặt service name `svc-neonfoodmap-be` và chọn **Task definition revision latest**. ![picCreateECS12](images/picCreateECS12.jpg)
3. Trong phần networking, chọn VPC và các **private subnet** của ứng dụng, chọn ECS task security group. ![picCreateECS3](images/picCreateECS3.jpg)
4. **Load balancing**, chọn **Application Load Balancer** `ALB-NeonFoodMap`; chọn existing listener `80:HTTP`, container backend port `8000` và existing target group `TG-NeonFoodMap-BE`. ![picCreateECS4](images/picCreateECS4.jpg)
5. Kiểm tra cấu hình, chọn **Create**. ECS sẽ tự tạo task và đăng ký IP task vào backend target group. ![picCreateECS5](images/picCreateECS5.jpg)

Sau khi tạo, ECS thực hiện rolling deployment. Trong thời gian này, giữ task đủ `Healthy` để ALB không chuyển request vào task chưa sẵn sàng.

![picCreateECS6](images/picCreateECS6.jpg)
