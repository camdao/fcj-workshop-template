---
title : "Tạo ECS cluster và service"
date : 2024-01-01
weight : 8
chapter : false
pre : " <b> 5.4.8. </b> "
---

### 5.4.8. Tạo ECS Cluster và Service

Sau khi hoàn thành phần này, hệ thống sẽ đáp ứng các yêu cầu sau:

- ✓ Tạo thành công ECS Cluster sử dụng **AWS Fargate**
- ✓ Triển khai Cluster trên **2 Availability Zones (AZ1, AZ2)** nhằm tăng tính sẵn sàng
- ✓ Tạo Task Definition cho Backend và Frontend
- ✓ Cấu hình CloudWatch Logs cho các Container
- ✓ Thiết lập biến môi trường và Secrets cho ứng dụng
- ✓ Cấu hình IAM Task Execution Role có quyền truy cập Amazon ECR
- ✓ Kiểm tra Task khởi chạy và hoạt động bình thường

---

## Các bước thực hiện

### Bước 1. Tạo ECS Cluster sử dụng AWS Fargate

1. Đăng nhập **AWS Management Console**.
2. Truy cập dịch vụ **Amazon ECS**.
3. Chọn **Clusters**.
4. Nhấn **Create Cluster**.
5. Chọn loại triển khai **Networking only (AWS Fargate)** hoặc **Amazon ECS Managed Instances** (tùy giao diện mới).
6. Đặt tên Cluster, ví dụ:

```
neonfoodmap-cluster
```

7. Chọn VPC đã tạo ở các bước trước.
8. Chọn hai Public Subnet hoặc Private Subnet thuộc:
   - Availability Zone 1 (AZ1)
   - Availability Zone 2 (AZ2)
9. Kiểm tra cấu hình.
10. Nhấn **Create** để hoàn tất.

---



### Bước 2. Tạo Task Definition cho Backend

1. Trong Amazon ECS, chọn **Task Definitions**.
2. Nhấn **Create new Task Definition**.
3. Chọn Launch Type là **AWS Fargate**.
4. Đặt tên Task Definition:

```
backend-task
```

5. Thiết lập cấu hình Task:

- CPU: **256 (.25 vCPU)**
- Memory: **512 MiB**

6. Thêm Container Backend:

- Image: Image Backend trên Amazon ECR
- Port Mapping: **8000** (hoặc cổng ứng dụng)
- Essential: Enabled

7. Chọn **Next** để tiếp tục.

---

### Bước 3. Tạo Task Definition cho Frontend

1. Chọn **Create new Task Definition**.
2. Đặt tên:

```
frontend-task
```

3. Thiết lập:

- CPU: **256 (.25 vCPU)**
- Memory: **512 MiB**

4. Thêm Container Frontend:

- Image: Image Frontend trên Amazon ECR
- Port Mapping:
  - 80
  - hoặc 3000 (tùy ứng dụng)

5. Hoàn tất việc tạo Task Definition.

---

### Bước 4. Cấu hình CloudWatch Log Groups

1. Trong phần Container của Task Definition, chọn **Logging**.
2. Chọn Log Driver:

```
awslogs
```

3. Đối với Backend:

```
Log Group:
/ecs/backend
```

4. Đối với Frontend:

```
Log Group:
/ecs/frontend
```

5. Thiết lập Region AWS.
6. Đặt Stream Prefix phù hợp, ví dụ:

```
backend
frontend
```

7. Lưu Task Definition.

---

### Bước 5. Thiết lập biến môi trường và Secrets

1. Trong phần Container Definition, chọn **Environment Variables**.
2. Thêm các biến môi trường cần thiết, ví dụ:

- DEBUG
- ALLOWED_HOSTS
- DB_HOST
- DB_NAME
- DB_PORT

3. Trong mục **Secrets**, chọn **Add Secret**.
4. Liên kết các Secret từ AWS Secrets Manager:

- Endpoint Amazon RDS
- Username Database
- Password Database
- API Keys
- JWT Secret
- Các khóa bí mật khác

5. Kiểm tra toàn bộ biến môi trường trước khi lưu.

---

### Bước 6. Tạo Task Execution Role

1. Truy cập dịch vụ **IAM**.
2. Chọn **Roles**.
3. Nhấn **Create Role**.
4. Chọn Trusted Entity:

```
Elastic Container Service Task
```

5. Gán các Policy cần thiết:

- AmazonECSTaskExecutionRolePolicy
- AmazonEC2ContainerRegistryReadOnly
- CloudWatchLogsFullAccess (hoặc quyền ghi Logs phù hợp)
- SecretsManagerReadWrite hoặc quyền chỉ đọc Secrets cần thiết

6. Đặt tên Role, ví dụ:

```
ecsTaskExecutionRole
```

7. Quay lại Task Definition.
8. Chọn Role vừa tạo tại mục **Task Execution Role**.

---

### Bước 7. Tạo ECS Service và kiểm tra Task

1. Mở **ECS Cluster** vừa tạo.
2. Chọn **Create Service**.
3. Chọn Launch Type:

```
Fargate
```

4. Chọn Task Definition tương ứng.
5. Đặt tên Service:

```
backend-service
```

hoặc

```
frontend-service
```

6. Thiết lập:

- Desired Tasks: **2**
- Deployment Type: Rolling Update

7. Chọn VPC và hai Subnet thuộc AZ1 và AZ2.
8. Chọn Security Group phù hợp.
9. Nếu sử dụng Load Balancer, liên kết với Target Group tương ứng.
10. Nhấn **Create Service**.

---

### Bước 8. Kiểm tra Task khởi chạy

1. Mở ECS Cluster.
2. Chọn tab **Services**.
3. Kiểm tra trạng thái Service là:

```
Active
```

4. Chọn tab **Tasks**.
5. Xác nhận các Task đều có trạng thái:

```
RUNNING
```

6. Mở **CloudWatch Logs** để kiểm tra Log của Backend và Frontend.
7. Truy cập ứng dụng thông qua DNS của Application Load Balancer (nếu đã cấu hình).
8. Kiểm tra ứng dụng phản hồi thành công và không phát sinh lỗi trong quá trình khởi chạy.

Hình 1 ![Hình 1.](/images/5-Workshop/5.5-Neon-Operations/image001.png)
Hình 2 ![Hình 2.](/images/5-Workshop/5.5-Neon-Operations/image002.png)
Hình 3 ![Hình 3.](/images/5-Workshop/5.5-Neon-Operations/image003.png)
Hình 4 ![Hình 4.](/images/5-Workshop/5.5-Neon-Operations/image004.png)
Hình 5 ![Hình 5.](/images/5-Workshop/5.5-Neon-Operations/image005.png)
Hình 6 ![Hình 6.](/images/5-Workshop/5.5-Neon-Operations/image006.png)
Hình 7 ![Hình 7.](/images/5-Workshop/5.5-Neon-Operations/image007.png)
Hình 8 ![Hình 8.](/images/5-Workshop/5.5-Neon-Operations/image008.png)
Hình 9 ![Hình 9.](/images/5-Workshop/5.5-Neon-Operations/image009.png)
Hình 10 ![Hình 10.](/images/5-Workshop/5.5-Neon-Operations/image010.png)


![Hình 1.](/images/5-Workshop/5.4-Neon-Deployment/image001.png)
![Hình 2.](/images/5-Workshop/5.4-Neon-Deployment/image002.png)
![Hình 3.](/images/5-Workshop/5.4-Neon-Deployment/image003.png)
![Hình 4.](/images/5-Workshop/5.4-Neon-Deployment/image004.png)
![Hình 5.](/images/5-Workshop/5.4-Neon-Deployment/image005.png)
![Hình 6.](/images/5-Workshop/5.4-Neon-Deployment/image006.png)
![Hình 7.](/images/5-Workshop/5.4-Neon-Deployment/image007.png)
![Hình 8.](/images/5-Workshop/5.4-Neon-Deployment/image008.png)
![Hình 9.](/images/5-Workshop/5.4-Neon-Deployment/image009.png)
![Hình 10.](/images/5-Workshop/5.4-Neon-Deployment/image010.png)
![Hình 11.](/images/5-Workshop/5.4-Neon-Deployment/image011.png)
![Hình 12.](/images/5-Workshop/5.4-Neon-Deployment/image012.png)
![Hình 13.](/images/5-Workshop/5.4-Neon-Deployment/image013.png)
![Hình 14.](/images/5-Workshop/5.4-Neon-Deployment/image014.png)
![Hình 15.](/images/5-Workshop/5.4-Neon-Deployment/image015.png)
![Hình 16.](/images/5-Workshop/5.4-Neon-Deployment/image016.png)
![Hình 17.](/images/5-Workshop/5.4-Neon-Deployment/image017.png)
![Hình 18.](/images/5-Workshop/5.4-Neon-Deployment/image018.png)
![Hình 19.](/images/5-Workshop/5.4-Neon-Deployment/image019.png)
![Hình 20.](/images/5-Workshop/5.4-Neon-Deployment/image020.png)
![Hình 21.](/images/5-Workshop/5.4-Neon-Deployment/image021.png)
![Hình 22.](/images/5-Workshop/5.4-Neon-Deployment/image022.png)
![Hình 23.](/images/5-Workshop/5.4-Neon-Deployment/image023.png)
![Hình 24.](/images/5-Workshop/5.4-Neon-Deployment/image024.png)
![Hình 25.](/images/5-Workshop/5.4-Neon-Deployment/image025.png)
![Hình 26.](/images/5-Workshop/5.4-Neon-Deployment/image026.png)
![Hình 27.](/images/5-Workshop/5.4-Neon-Deployment/image027.png)
![Hình 28.](/images/5-Workshop/5.4-Neon-Deployment/image028.png)
![Hình 29.](/images/5-Workshop/5.4-Neon-Deployment/image029.png)
![Hình 30.](/images/5-Workshop/5.4-Neon-Deployment/image030.png)
![Hình 31.](/images/5-Workshop/5.4-Neon-Deployment/image031.png)
![Hình 32.](/images/5-Workshop/5.4-Neon-Deployment/image032.png)
![Hình 33.](/images/5-Workshop/5.4-Neon-Deployment/image033.png)
![Hình 34.](/images/5-Workshop/5.4-Neon-Deployment/image034.png)
![Hình 35.](/images/5-Workshop/5.4-Neon-Deployment/image035.png)
![Hình 36.](/images/5-Workshop/5.4-Neon-Deployment/image036.png)
![Hình 37.](/images/5-Workshop/5.4-Neon-Deployment/image037.png)
![Hình 38.](/images/5-Workshop/5.4-Neon-Deployment/image038.png)
![Hình 39.](/images/5-Workshop/5.4-Neon-Deployment/image039.png)
![Hình 40.](/images/5-Workshop/5.4-Neon-Deployment/image040.png)
![Hình 41.](/images/5-Workshop/5.4-Neon-Deployment/image041.png)
![Hình 42.](/images/5-Workshop/5.4-Neon-Deployment/image042.png)
![Hình 43.](/images/5-Workshop/5.4-Neon-Deployment/image043.png)
