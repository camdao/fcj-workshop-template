---
title : "Thiết lập IAM Roles"
date : 2024-01-01
weight : 4
chapter : false
pre : " <b> 5.3.4. </b> "
---

## Tổng quan

Sau khi đã tạo IAM Users & Groups bằng CloudFormation (xem [5.4.3](../../5.4-neon-deployment/5.4.3-cloudformation/)), phần này hướng dẫn tạo **IAM Roles cho Services** để ứng dụng có thể hoạt động:

- **ECS Task Execution Role**: Pull Docker images từ ECR và ghi logs
- **ECS Task Role**: Cho phép backend truy cập S3
- **GitHub Actions Role**: CI/CD deployment tự động

## 5.3.4.1. IAM Role cho ECS Task Execution

Role này cho phép ECS pull Docker images từ ECR và ghi logs vào CloudWatch.

**Các bước thực hiện:**

1. Mở **IAM Console** → **Roles** → **Create role**
2. Chọn trusted entity: **AWS service** → **Elastic Container Service** → **ECS Task**
3. Gắn managed policy: `AmazonECSTaskExecutionRolePolicy`
4. Đặt tên role: `NeonFoodmap-TaskExecution-Role`
5. Tạo role

![Hình 110.](/images/5-Workshop/5.3-Neon-Infracstructure/image110.png)
![Hình 112.](/images/5-Workshop/5.3-Neon-Infracstructure/image112.png)
![Hình 114.](/images/5-Workshop/5.3-Neon-Infracstructure/image114.png)
![Hình 115.](/images/5-Workshop/5.3-Neon-Infracstructure/image115.png)

## 5.3.4.2. IAM Role cho ECS Task (Backend Application)

Role này cho phép Django backend truy cập S3 để lưu/đọc media files.

**Các bước thực hiện:**

1. Mở **IAM Console** → **Roles** → **Create role**
2. Chọn trusted entity: **AWS service** → **Elastic Container Service** → **ECS Task**
3. **Không** gắn managed policy (sẽ tạo inline policy)
4. Đặt tên role: `NeonFoodmap-ECS-Backend-Role`
5. Sau khi tạo role, vào role và tạo **inline policy** với nội dung:

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": [
        "s3:ListBucket"
      ],
      "Resource": "arn:aws:s3:::neonfoodmap-media-*"
    },
    {
      "Effect": "Allow",
      "Action": [
        "s3:GetObject",
        "s3:PutObject",
        "s3:DeleteObject"
      ],
      "Resource": "arn:aws:s3:::neonfoodmap-media-*/*"
    }
  ]
}
```

![Hình 117.](/images/5-Workshop/5.3-Neon-Infracstructure/image117.png)
![Hình 119.](/images/5-Workshop/5.3-Neon-Infracstructure/image119.png)
![Hình 121.](/images/5-Workshop/5.3-Neon-Infracstructure/image121.png)
![Hình 123.](/images/5-Workshop/5.3-Neon-Infracstructure/image123.png)
![Hình 125.](/images/5-Workshop/5.3-Neon-Infracstructure/image125.png)
![Hình 127.](/images/5-Workshop/5.3-Neon-Infracstructure/image127.png)
![Hình 129.](/images/5-Workshop/5.3-Neon-Infracstructure/image129.png)
![Hình 131.](/images/5-Workshop/5.3-Neon-Infracstructure/image131.png)

## 5.3.4.3. GitHub OIDC Provider và IAM Role cho CI/CD

Thiết lập này cho phép GitHub Actions deploy ứng dụng mà không cần lưu AWS access keys trong GitHub Secrets.

### Bước 1: Tạo OIDC Identity Provider

1. Vào **IAM Console** → **Access management** → **Identity providers**
2. Chọn **Add provider**
3. Chọn **OpenID Connect**
4. Nhập thông tin:
   - **Provider URL**: `https://token.actions.githubusercontent.com`
   - **Audience**: `sts.amazonaws.com`
5. Nhấn **Add provider**

![Hình 133.](/images/5-Workshop/5.3-Neon-Infracstructure/image133.png)
![Hình 135.](/images/5-Workshop/5.3-Neon-Infracstructure/image135.png)
![Hình 137.](/images/5-Workshop/5.3-Neon-Infracstructure/image137.png)
![Hình 139.](/images/5-Workshop/5.3-Neon-Infracstructure/image139.png)

### Bước 2: Tạo IAM Role cho GitHub Actions

1. Vào **IAM Console** → **Roles** → **Create role**
2. Chọn **Web identity**
3. Chọn **Identity provider**: GitHub OIDC provider vừa tạo
4. **Audience**: `sts.amazonaws.com`
5. Gắn policies cho phép GitHub Actions:
   - Deploy backend: `AmazonEC2ContainerRegistryPowerUser`, `AmazonECS_FullAccess`
   - Deploy frontend: `AmazonS3FullAccess`, `CloudFrontFullAccess`
6. Đặt tên role: `NeonFoodmap-GitHub-Actions-Role`

![Hình 142.](/images/5-Workshop/5.3-Neon-Infracstructure/image142.png)
![Hình 143.](/images/5-Workshop/5.3-Neon-Infracstructure/image143.png)
![Hình 145.](/images/5-Workshop/5.3-Neon-Infracstructure/image145.png)
![Hình 149.](/images/5-Workshop/5.3-Neon-Infracstructure/image149.png)

### Bước 3: Cấu hình Trust Policy

Sau khi tạo role, chỉnh sửa Trust Policy để chỉ cho phép repository và branch cụ thể:

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Principal": {
        "Federated": "arn:aws:iam::ACCOUNT_ID:oidc-provider/token.actions.githubusercontent.com"
      },
      "Action": "sts:AssumeRoleWithWebIdentity",
      "Condition": {
        "StringEquals": {
          "token.actions.githubusercontent.com:aud": "sts.amazonaws.com"
        },
        "StringLike": {
          "token.actions.githubusercontent.com:sub": "repo:HaoWasabi/NeonFoodmap:ref:refs/heads/main"
        }
      }
    }
  ]
}
```

**Lưu ý**: Thay `ACCOUNT_ID` bằng AWS Account ID của bạn.

![Hình 151.](/images/5-Workshop/5.3-Neon-Infracstructure/image151.png)
![Hình 153.](/images/5-Workshop/5.3-Neon-Infracstructure/image153.png)
![Hình 155.](/images/5-Workshop/5.3-Neon-Infracstructure/image155.png)

## Tóm tắt IAM Roles

| **Role** | **Mục đích** | **Được sử dụng bởi** |
|----------|--------------|---------------------|
| `NeonFoodmap-TaskExecution-Role` | Pull Docker images, ghi logs | ECS Task Definition (executionRoleArn) |
| `NeonFoodmap-ECS-Backend-Role` | Truy cập S3 cho media files | ECS Task Definition (taskRoleArn) |
| `NeonFoodmap-GitHub-Actions-Role` | CI/CD deployment tự động | GitHub Actions workflows |