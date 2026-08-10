---
title : "Tạo ECS Cluster và Service"
date : 2024-01-01
weight : 8
chapter : false
pre : " <b> 5.4.8. </b> "
---

Sau khi hoàn thành phần này, hệ thống sẽ đáp ứng các yêu cầu sau:

- Tạo thành công ECS Cluster sử dụng **AWS Fargate**
- Cấu hình ECS Service sử dụng các Subnet thuộc **2 Availability Zones (AZ1, AZ2)** để tăng tính sẵn sàng
- Tạo Task Definition cho Backend với CPU **256** và RAM **512 MB**
- Cấu hình CloudWatch Logs cho Container
- Thiết lập biến môi trường và Secrets cho ứng dụng
- Cấu hình IAM Task Execution Role để ECS pull Docker Image từ Amazon ECR và ghi log lên CloudWatch
- Kiểm tra Task khởi chạy và hoạt động bình thường

---

### Các bước thực hiện

#### Bước 1. Tạo ECS Cluster sử dụng AWS Fargate

1. Truy cập **AWS Management Console**
2. Tìm kiếm và chọn dịch vụ **Amazon ECS**
3. Trong menu bên trái, chọn **Clusters**
4. Chọn **Create cluster**
5. Tại **Cluster name**, nhập tên Cluster:

```text
neonfoodmap-cluster
```

6. Tại phần **Infrastructure**, chọn:

```text
AWS Fargate (serverless)
```

7. Kiểm tra lại thông tin Cluster
8. Chọn **Create** để tạo Cluster
9. Sau khi tạo thành công, Cluster sẽ xuất hiện trong danh sách

> **Lưu ý:** ECS Cluster là tài nguyên logic nên không được gán trực tiếp vào AZ1 hoặc AZ2. Việc chạy trên nhiều Availability Zone được cấu hình khi tạo ECS Service bằng cách lựa chọn các Subnet thuộc AZ1 và AZ2.

![](/images/5-Workshop/5.4-Neon-Deployment/image010.png)
![](/images/5-Workshop/5.4-Neon-Deployment/image011.png)
![](/images/5-Workshop/5.4-Neon-Deployment/image012.png)
![](/images/5-Workshop/5.4-Neon-Deployment/image013.png)
![](/images/5-Workshop/5.4-Neon-Deployment/image014.png)
![](/images/5-Workshop/5.4-Neon-Deployment/image015.png)

---

#### Bước 2. Tạo Task Definition cho Backend với CPU 256 và RAM 512 MB

Task Definition xác định cách ECS khởi chạy Backend Container, bao gồm Docker Image, CPU, RAM, Port, Environment Variables và Log Configuration.

1. Trong Amazon ECS, chọn **Task definitions**
2. Chọn **Create new task definition**
3. Nhập tên Task Definition:

```text
neonfoodmap-backend
```

4. Tại **Infrastructure requirements**, chọn:

```text
AWS Fargate
```

5. Cấu hình tài nguyên:

```text
CPU: 0.25 vCPU
Memory: 0.5 GB
```

Tương ứng:

```text
CPU: 256
RAM: 512 MiB
```

6. Tại **Task execution role**, chọn IAM Role dành cho ECS Task Execution:

```text
NeonFoodmap-TaskExecution-Role
```

7. Tại **Task role**, chọn IAM Role cho phép container truy cập AWS services:

```text
NeonFoodmap-ECS-Backend-Role
```

8. Tại phần **Container**, chọn **Add container**
9. Nhập tên Container:

```text
backend
```

10. Tại **Image URI**, nhập Docker Image Backend được lưu trên Amazon ECR:

```text
<AWS_ACCOUNT_ID>.dkr.ecr.ap-southeast-1.amazonaws.com/neonfoodmap-backend:latest
```

11. Cấu hình **Port mapping**:

```text
Container port: 8000
Protocol: TCP
App protocol: HTTP
```

12. Cấu hình **Environment variables** cần thiết cho ứng dụng:

```text
DJANGO_SETTINGS_MODULE=config.settings
DEBUG=False
ALLOWED_HOSTS=<DOMAIN>
AWS_REGION=ap-southeast-1
AWS_STORAGE_BUCKET_NAME=<S3_BUCKET_NAME>
```

13. Cấu hình **Secrets** cho thông tin nhạy cảm:

```text
DB_HOST: <RDS_ENDPOINT>
DB_NAME: <DATABASE_NAME>
DB_USER: <DATABASE_USER>
DB_PASSWORD: ValueFrom AWS Secrets Manager
```

14. Cấu hình Container Logs sử dụng **Amazon CloudWatch Logs**:

```text
Log driver: awslogs
Log Group: /ecs/neonfoodmap-backend
Region: ap-southeast-1
Stream prefix: ecs
```

15. Kiểm tra lại cấu hình và chọn **Create**

![](/images/5-Workshop/5.4-Neon-Deployment/image016.png)
![](/images/5-Workshop/5.4-Neon-Deployment/image017.png)
![](/images/5-Workshop/5.4-Neon-Deployment/image018.png)
![](/images/5-Workshop/5.4-Neon-Deployment/image019.png)
![](/images/5-Workshop/5.4-Neon-Deployment/image020.png)
![](/images/5-Workshop/5.4-Neon-Deployment/image021.png)
![](/images/5-Workshop/5.4-Neon-Deployment/image022.png)
![](/images/5-Workshop/5.4-Neon-Deployment/image023.png)
![](/images/5-Workshop/5.4-Neon-Deployment/image024.png)

---

#### Bước 3. Cấu hình CloudWatch Log Group cho Backend

CloudWatch Logs được sử dụng để tập trung log từ Backend Container, phục vụ việc theo dõi hoạt động và xử lý sự cố.

1. Truy cập dịch vụ **Amazon CloudWatch**
2. Chọn **Logs → Log groups**
3. Chọn **Create log group**
4. Tạo Log Group cho Backend:

```text
/ecs/neonfoodmap-backend
```

5. Chọn **Create**
6. Kiểm tra Log Group đã xuất hiện
7. Đối chiếu tên Log Group trong Task Definition với Log Group đã tạo

> Khi ECS Task khởi chạy, log của Container sẽ được gửi đến Log Group thông qua cấu hình `awslogs`.

---

#### Bước 4. Thiết lập biến môi trường và Secrets

##### 4.1. Cấu hình Environment Variables

Trong Task Definition Backend, các biến cấu hình không chứa thông tin nhạy cảm:

```text
DJANGO_SETTINGS_MODULE=config.settings
DEBUG=False
ALLOWED_HOSTS=api.neonfoodmap.example.com
AWS_REGION=ap-southeast-1
AWS_STORAGE_BUCKET_NAME=neonfoodmap-media
```

##### 4.2. Cấu hình Secrets cho RDS

Thông tin kết nối Database nhạy cảm được lưu trong **AWS Secrets Manager**:

1. Mở phần **Secrets** của Container Backend
2. Chọn **Add secret**
3. Cấu hình:

```text
Name: DB_PASSWORD
ValueFrom: arn:aws:secretsmanager:ap-southeast-1:<ACCOUNT_ID>:secret:rds-credentials
```

##### 4.3. Cấu hình API Keys

Đối với các API Key của dịch vụ bên ngoài:

```text
Name: GOOGLE_TTS_API_KEY
ValueFrom: arn:aws:secretsmanager:ap-southeast-1:<ACCOUNT_ID>:secret:google-tts-key
```

> Task cần được cấp quyền để truy cập Secret từ AWS Secrets Manager thông qua Task Execution Role.

---

#### Bước 5. Cấu hình Task Execution Role

Task Execution Role cho phép ECS thực hiện các thao tác cần thiết trong quá trình khởi chạy Task.

1. Truy cập **AWS Console → IAM**
2. Chọn **Roles**
3. Tìm Role:

```text
NeonFoodmap-TaskExecution-Role
```

4. Kiểm tra Role có các quyền:
   - Pull Docker Image từ Amazon ECR
   - Ghi Container Logs vào CloudWatch Logs
   - Truy cập Secret từ AWS Secrets Manager

5. Managed policies cần có:
   - `AmazonECSTaskExecutionRolePolicy`
   - Custom policy cho Secrets Manager (nếu sử dụng Secrets)

6. Quay lại Task Definition và xác nhận đang sử dụng Role này

---

### Kiểm tra kết quả

Sau khi hoàn thành các bước trên, kiểm tra lại cấu hình:

| Thành phần | Kết quả mong đợi |
|------------|------------------|
| ECS Cluster | Đã tạo và ở trạng thái `ACTIVE` |
| Backend Task Definition | Đã tạo, CPU 256 và RAM 512 MiB |
| Backend Image | Trỏ đến Repository Backend trên ECR |
| CloudWatch Logs | Có `/ecs/neonfoodmap-backend` |
| Environment Variables | Đã cấu hình |
| Secrets | Đã cấu hình thông qua Secrets Manager |
| Task Execution Role | Đã gán cho Backend Task Definition |
| Task Role | Đã gán cho Backend (S3 access) |
| ECR Permission | Cho phép ECS pull Image |

Sau khi các cấu hình trên hoàn tất, hệ thống đã sẵn sàng để tạo **ECS Service** và triển khai Task trên các Subnet thuộc **AZ1 và AZ2**.

![](/images/5-Workshop/5.4-Neon-Deployment/image039.png)
![](/images/5-Workshop/5.4-Neon-Deployment/image040.png)
![](/images/5-Workshop/5.4-Neon-Deployment/image041.png)
![](/images/5-Workshop/5.4-Neon-Deployment/image042.png)