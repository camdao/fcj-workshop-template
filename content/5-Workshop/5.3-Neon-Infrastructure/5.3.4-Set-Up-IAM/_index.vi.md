---
title : "Khởi tạo và cấu hình IAM"
date : 2024-01-01
weight : 4
chapter : false
pre : " <b> 5.3.4. </b> "
---

### 5.3.15. Tạo IAM Role cho ECS task execution

1. Mở IAM Console → Roles → Create role.
2. Chọn trusted entity `AWS service → Elastic Container Service → ECS Task`.
3. Đặt tên role:
   - `NeonFoodmap-TaskExecution-Role`
   - `NeonFoodmap-ECS-Backend-Role`
4. Hoàn tất tạo role.
5. Gắn inline policy cho backend role với quyền:
   - `s3:ListBucket`
   - `s3:GetObject`
   - `s3:PutObject`

![Hình 15. Tạo IAM Role cho ECS](/5-Workshop/images/5.3-neon-infrastructure/placeholder-iam-role.png)

### 5.3.16. Tạo GitHub OIDC provider và IAM Role cho GitHub Actions

1. Vào IAM Console → Access management → Identity providers.
2. Chọn Add provider.
3. Chọn OpenID Connect.
4. Provider URL: `https://token.actions.githubusercontent.com`
5. Audience: `sts.amazonaws.com`
6. Nhấn Add provider.
7. Tạo role mới với trusted entity là Web identity.
8. Chọn GitHub OIDC provider đã tạo.
9. Gắn policy phù hợp để GitHub Actions triển khai lên S3/ECR/ECS.
10. Cấu hình trust policy để chỉ repository và nhánh được phép Assume Role.

![Hình 16. Thiết lập GitHub OIDC](/5-Workshop/images/5.3-neon-infrastructure/placeholder-github-oidc.png)
