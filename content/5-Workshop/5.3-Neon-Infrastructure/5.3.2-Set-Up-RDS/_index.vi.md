---
title : "Khởi tạo và cấu hình RDS"
date : 2024-01-01
weight : 2
chapter : false
pre : " <b> 5.3.2. </b> "
---


### Tổng quan kiến trúc triển khai

Hạ tầng cần được xây dựng theo mô hình multi-tier với các lớp sau:

- Public subnet: tiếp nhận lưu lượng từ Internet
- Private subnet: chạy ứng dụng và dịch vụ nội bộ
- Database subnet: triển khai RDS của hệ thống
- S3 bucket: lưu trữ frontend, media, audio, logs
- IAM Role và OIDC: cấp quyền deploy an toàn cho GitHub Actions

### 5.3.6. Tạo DB Subnet Group cho Amazon RDS

1. Mở Amazon RDS Console.
2. Chọn Subnet groups.
3. Nhấn Create DB Subnet Group.
4. Chọn VPC của dự án.
5. Chọn các private subnet ở hai AZ.
6. Nhấn Create.

![Hình 31.](/5-Workshop/images/5.3-Neon-Infracstructure/image031.png)
![Hình 32.](/5-Workshop/images/5.3-Neon-Infracstructure/image032.png)


### 5.3.7. Tạo DB Parameter Group cho MySQL

1. Vào RDS Console → Parameter groups.
2. Chọn Create parameter group.
3. Cấu hình:
   - Group name: `neonfoodmap-mysql80-params`
   - Description: `Parameter group tối ưu utf8mb4 cho NeonFoodmap`
   - Engine type: `MySQL`
   - Parameter group family: `mysql8.0`
   - Type: `DB Parameter Group`
4. Nhấn Create.
5. Chọn parameter group vừa tạo → Edit.
6. Cập nhật:
   - `character_set_server = utf8mb4`
   - `collation_server = utf8mb4_unicode_ci`
7. Nhấn Save changes.

![Hình 33.](/5-Workshop/images/5.3-Neon-Infracstructure/image033.png)
![Hình 34.](/5-Workshop/images/5.3-Neon-Infracstructure/image034.png)
![Hình 35.](/5-Workshop/images/5.3-Neon-Infracstructure/image035.png)
![Hình 36.](/5-Workshop/images/5.3-Neon-Infracstructure/image036.png)
![Hình 37.](/5-Workshop/images/5.3-Neon-Infracstructure/image037.png)
![Hình 38.](/5-Workshop/images/5.3-Neon-Infracstructure/image038.png)


### 5.3.8. Tạo Security Group cho RDS

1. Mở EC2 Console → Security Groups.
2. Chọn Create security group.
3. Thiết lập:
   - Name: `neonfoodmap-rds-sg`
   - Description: `Allow inbound traffic from ECS tasks only`
   - VPC: chọn VPC dự án
4. Trong Inbound rules, thêm rule:
   - Type: `MySQL/Aurora`
   - Port: `3306`
   - Source: security group của ECS task hoặc backend service
5. Giữ nguyên outbound rule mặc định.
6. Nhấn Create security group.

![Hình 39.](/5-Workshop/images/5.3-Neon-Infracstructure/image039.png)
![Hình 40.](/5-Workshop/images/5.3-Neon-Infracstructure/image040.png)

### 5.3.9. Khởi tạo Amazon RDS MySQL instance

1. Vào Amazon RDS Console → Databases → Create database.
2. Chọn Standard Create.
3. Chọn engine `MySQL` và phiên bản phù hợp.
4. Trong phần Settings:
   - DB instance identifier: `neonfoodmap-mysql-db`
   - Master username: `admin`
   - Master password: đặt mật khẩu mạnh và lưu lại nơi an toàn
   - Instance type: `db.t3.micro`
5. Trong phần Storage:
   - Storage type: `gp3`
   - Allocated storage: `20 GiB`
   - Tích chọn storage autoscaling tối đa `100 GB`
6. Trong phần Connectivity:
   - Compute resource: `Don't connect to an EC2 compute resource`
   - VPC: chọn VPC dự án
   - DB subnet group: chọn group đã tạo
   - Public access: `No`
   - VPC security group: chọn `neonfoodmap-rds-sg`
   - Database port: `3306`
7. Trong phần Monitoring:
   - Tích chọn `Error log` và `Slow query log`
8. Trong phần Additional configuration:
   - Initial database name: `buocchancoi_db`
   - DB parameter group: `neonfoodmap-mysql80-params`
   - Enable automated backups với retention `7 days`
   - Enable encryption
9. Nhấn Create database.

![Hình 41.](/5-Workshop/images/5.3-Neon-Infracstructure/image041.png)
![Hình 42.](/5-Workshop/images/5.3-Neon-Infracstructure/image042.png)
![Hình 43.](/5-Workshop/images/5.3-Neon-Infracstructure/image043.png)
![Hình 44.](/5-Workshop/images/5.3-Neon-Infracstructure/image044.png)
![Hình 45.](/5-Workshop/images/5.3-Neon-Infracstructure/image045.png)
![Hình 46.](/5-Workshop/images/5.3-Neon-Infracstructure/image046.png)
![Hình 47.](/5-Workshop/images/5.3-Neon-Infracstructure/image047.png)
![Hình 48.](/5-Workshop/images/5.3-Neon-Infracstructure/image048.png)
![Hình 49.](/5-Workshop/images/5.3-Neon-Infracstructure/image049.png)
![Hình 50.](/5-Workshop/images/5.3-Neon-Infracstructure/image050.png)
![Hình 51.](/5-Workshop/images/5.3-Neon-Infracstructure/image051.png)
![Hình 52.](/5-Workshop/images/5.3-Neon-Infracstructure/image052.png)
![Hình 53.](/5-Workshop/images/5.3-Neon-Infracstructure/image053.png)
![Hình 54.](/5-Workshop/images/5.3-Neon-Infracstructure/image054.png)
![Hình 55.](/5-Workshop/images/5.3-Neon-Infracstructure/image055.png)
![Hình 56.](/5-Workshop/images/5.3-Neon-Infracstructure/image056.png)
![Hình 57.](/5-Workshop/images/5.3-Neon-Infracstructure/image057.png)
![Hình 58.](/5-Workshop/images/5.3-Neon-Infracstructure/image058.png)
![Hình 59.](/5-Workshop/images/5.3-Neon-Infracstructure/image059.png)
![Hình 60.](/5-Workshop/images/5.3-Neon-Infracstructure/image060.png)
![Hình 61.](/5-Workshop/images/5.3-Neon-Infracstructure/image061.png)
![Hình 62.](/5-Workshop/images/5.3-Neon-Infracstructure/image062.png)
![Hình 63.](/5-Workshop/images/5.3-Neon-Infracstructure/image063.png)
![Hình 64.](/5-Workshop/images/5.3-Neon-Infracstructure/image064.png)
![Hình 65.](/5-Workshop/images/5.3-Neon-Infracstructure/image065.png)
![Hình 66.](/5-Workshop/images/5.3-Neon-Infracstructure/image066.png)
![Hình 67.](/5-Workshop/images/5.3-Neon-Infracstructure/image067.png)
![Hình 68.](/5-Workshop/images/5.3-Neon-Infracstructure/image068.png)
![Hình 69.](/5-Workshop/images/5.3-Neon-Infracstructure/image069.png)
![Hình 70.](/5-Workshop/images/5.3-Neon-Infracstructure/image070.png)
![Hình 71.](/5-Workshop/images/5.3-Neon-Infracstructure/image071.png)
![Hình 72.](/5-Workshop/images/5.3-Neon-Infracstructure/image072.png)
![Hình 73.](/5-Workshop/images/5.3-Neon-Infracstructure/image073.png)
![Hình 74.](/5-Workshop/images/5.3-Neon-Infracstructure/image074.png)
![Hình 75.](/5-Workshop/images/5.3-Neon-Infracstructure/image075.png)
![Hình 76.](/5-Workshop/images/5.3-Neon-Infracstructure/image076.png)
![Hình 77.](/5-Workshop/images/5.3-Neon-Infracstructure/image077.png)
![Hình 78.](/5-Workshop/images/5.3-Neon-Infracstructure/image078.png)
![Hình 79.](/5-Workshop/images/5.3-Neon-Infracstructure/image079.png)
![Hình 80.](/5-Workshop/images/5.3-Neon-Infracstructure/image080.png)
![Hình 81.](/5-Workshop/images/5.3-Neon-Infracstructure/image081.png)
![Hình 82.](/5-Workshop/images/5.3-Neon-Infracstructure/image082.png)
![Hình 83.](/5-Workshop/images/5.3-Neon-Infracstructure/image083.png)
![Hình 84.](/5-Workshop/images/5.3-Neon-Infracstructure/image084.png)
![Hình 85.](/5-Workshop/images/5.3-Neon-Infracstructure/image085.png)
![Hình 86.](/5-Workshop/images/5.3-Neon-Infracstructure/image086.png)
![Hình 87.](/5-Workshop/images/5.3-Neon-Infracstructure/image087.png)
![Hình 88.](/5-Workshop/images/5.3-Neon-Infracstructure/image088.png)
![Hình 89.](/5-Workshop/images/5.3-Neon-Infracstructure/image089.png)
![Hình 90.](/5-Workshop/images/5.3-Neon-Infracstructure/image090.png)
![Hình 91.](/5-Workshop/images/5.3-Neon-Infracstructure/image091.png)
![Hình 92.](/5-Workshop/images/5.3-Neon-Infracstructure/image092.png)
![Hình 93.](/5-Workshop/images/5.3-Neon-Infracstructure/image093.png)
![Hình 94.](/5-Workshop/images/5.3-Neon-Infracstructure/image094.png)
![Hình 95.](/5-Workshop/images/5.3-Neon-Infracstructure/image095.png)
![Hình 96.](/5-Workshop/images/5.3-Neon-Infracstructure/image096.png)
![Hình 97.](/5-Workshop/images/5.3-Neon-Infracstructure/image097.png)
![Hình 98.](/5-Workshop/images/5.3-Neon-Infracstructure/image098.png)
![Hình 99.](/5-Workshop/images/5.3-Neon-Infracstructure/image099.png)
![Hình 100.](/5-Workshop/images/5.3-Neon-Infracstructure/image100.png)
![Hình 101.](/5-Workshop/images/5.3-Neon-Infracstructure/image101.png)
![Hình 102.](/5-Workshop/images/5.3-Neon-Infracstructure/image102.png)
![Hình 103.](/5-Workshop/images/5.3-Neon-Infracstructure/image103.png)
![Hình 104.](/5-Workshop/images/5.3-Neon-Infracstructure/image104.png)
![Hình 105.](/5-Workshop/images/5.3-Neon-Infracstructure/image105.png)
![Hình 106.](/5-Workshop/images/5.3-Neon-Infracstructure/image106.png)
![Hình 107.](/5-Workshop/images/5.3-Neon-Infracstructure/image107.png)
![Hình 108.](/5-Workshop/images/5.3-Neon-Infracstructure/image108.png)
![Hình 109.](/5-Workshop/images/5.3-Neon-Infracstructure/image109.png)
![Hình 110.](/5-Workshop/images/5.3-Neon-Infracstructure/image110.png)
![Hình 111.](/5-Workshop/images/5.3-Neon-Infracstructure/image111.png)
![Hình 112.](/5-Workshop/images/5.3-Neon-Infracstructure/image112.png)
![Hình 113.](/5-Workshop/images/5.3-Neon-Infracstructure/image113.png)
![Hình 114.](/5-Workshop/images/5.3-Neon-Infracstructure/image114.png)
![Hình 115.](/5-Workshop/images/5.3-Neon-Infracstructure/image115.png)
![Hình 116.](/5-Workshop/images/5.3-Neon-Infracstructure/image116.png)
![Hình 117.](/5-Workshop/images/5.3-Neon-Infracstructure/image117.png)
![Hình 118.](/5-Workshop/images/5.3-Neon-Infracstructure/image118.png)
![Hình 119.](/5-Workshop/images/5.3-Neon-Infracstructure/image119.png)
![Hình 120.](/5-Workshop/images/5.3-Neon-Infracstructure/image120.png)
![Hình 121.](/5-Workshop/images/5.3-Neon-Infracstructure/image121.png)
![Hình 122.](/5-Workshop/images/5.3-Neon-Infracstructure/image122.png)
![Hình 123.](/5-Workshop/images/5.3-Neon-Infracstructure/image123.png)
![Hình 124.](/5-Workshop/images/5.3-Neon-Infracstructure/image124.png)
![Hình 125.](/5-Workshop/images/5.3-Neon-Infracstructure/image125.png)
![Hình 126.](/5-Workshop/images/5.3-Neon-Infracstructure/image126.png)
![Hình 127.](/5-Workshop/images/5.3-Neon-Infracstructure/image127.png)
![Hình 128.](/5-Workshop/images/5.3-Neon-Infracstructure/image128.png)
![Hình 129.](/5-Workshop/images/5.3-Neon-Infracstructure/image129.png)
![Hình 130.](/5-Workshop/images/5.3-Neon-Infracstructure/image130.png)
![Hình 131.](/5-Workshop/images/5.3-Neon-Infracstructure/image131.png)
![Hình 132.](/5-Workshop/images/5.3-Neon-Infracstructure/image132.png)
![Hình 133.](/5-Workshop/images/5.3-Neon-Infracstructure/image133.png)
![Hình 134.](/5-Workshop/images/5.3-Neon-Infracstructure/image134.png)
![Hình 135.](/5-Workshop/images/5.3-Neon-Infracstructure/image135.png)
![Hình 136.](/5-Workshop/images/5.3-Neon-Infracstructure/image136.png)
![Hình 137.](/5-Workshop/images/5.3-Neon-Infracstructure/image137.png)
![Hình 138.](/5-Workshop/images/5.3-Neon-Infracstructure/image138.png)
![Hình 139.](/5-Workshop/images/5.3-Neon-Infracstructure/image139.png)
![Hình 140.](/5-Workshop/images/5.3-Neon-Infracstructure/image140.png)
![Hình 141.](/5-Workshop/images/5.3-Neon-Infracstructure/image141.png)
![Hình 142.](/5-Workshop/images/5.3-Neon-Infracstructure/image142.png)
![Hình 143.](/5-Workshop/images/5.3-Neon-Infracstructure/image143.png)
![Hình 144.](/5-Workshop/images/5.3-Neon-Infracstructure/image144.png)
![Hình 145.](/5-Workshop/images/5.3-Neon-Infracstructure/image145.png)
![Hình 146.](/5-Workshop/images/5.3-Neon-Infracstructure/image146.png)
![Hình 147.](/5-Workshop/images/5.3-Neon-Infracstructure/image147.png)
![Hình 148.](/5-Workshop/images/5.3-Neon-Infracstructure/image148.png)
![Hình 149.](/5-Workshop/images/5.3-Neon-Infracstructure/image149.png)
![Hình 150.](/5-Workshop/images/5.3-Neon-Infracstructure/image150.png)
![Hình 151.](/5-Workshop/images/5.3-Neon-Infracstructure/image151.png)
![Hình 152.](/5-Workshop/images/5.3-Neon-Infracstructure/image152.png)
![Hình 153.](/5-Workshop/images/5.3-Neon-Infracstructure/image153.png)
![Hình 154.](/5-Workshop/images/5.3-Neon-Infracstructure/image154.png)
![Hình 155.](/5-Workshop/images/5.3-Neon-Infracstructure/image155.png)


### 5.3.10. Lấy endpoint và lưu vào file `.env`

1. Mở DB instance vừa tạo.
2. Chọn tab Connectivity & security.
3. Copy giá trị Endpoint.
4. Dán vào file `.env` của dự án để backend kết nối đúng địa chỉ database.

![Hình 10. Lấy Endpoint database](/5-Workshop/images/5.3-neon-infrastructure/placeholder-rds-endpoint.png)
