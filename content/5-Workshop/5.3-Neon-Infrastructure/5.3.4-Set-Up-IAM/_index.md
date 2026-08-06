---
title : "Initialize and Configure IAM"
date : 2024-01-01
weight : 4
chapter : false
pre : " <b> 5.3.4. </b> "
---

### 5.3.15. Create IAM Role for ECS Task Execution

1. Open IAM Console → **Roles** → **Create role**.
2. Select trusted entity: `AWS service → Elastic Container Service → ECS Task`.
3. Name the roles:
   - `NeonFoodmap-TaskExecution-Role`
   - `NeonFoodmap-ECS-Backend-Role`
4. Complete the role creation.
5. Attach an inline policy to the backend role with the following permissions:
   - `s3:ListBucket`
   - `s3:GetObject`
   - `s3:PutObject`

![Figure 15. Create IAM Role for ECS](/images/5-Workshop/5.3-neon-infrastructure/placeholder-iam-role.png)

### 5.3.16. Create GitHub OIDC Provider and IAM Role for GitHub Actions

1. Go to IAM Console → **Access management** → **Identity providers**.
2. Click **Add provider**.
3. Select **OpenID Connect**.
4. Provider URL: `https://token.actions.githubusercontent.com`
5. Audience: `sts.amazonaws.com`
6. Click **Add provider**.
7. Create a new role with trusted entity set to **Web identity**.
8. Select the GitHub OIDC provider you just created.
9. Attach the appropriate policy so GitHub Actions can deploy to S3/ECR/ECS.
10. Configure the trust policy to allow only the specified repository and branch to Assume the Role.

![Figure 16. Set up GitHub OIDC](/images/5-Workshop/5.3-neon-infrastructure/placeholder-github-oidc.png)
