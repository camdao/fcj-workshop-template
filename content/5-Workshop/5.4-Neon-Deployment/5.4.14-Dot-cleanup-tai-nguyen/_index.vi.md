---
title : "Dọn dẹp tài nguyên"
date : 2024-01-01
weight : 14
chapter : false
pre : " <b> 5.4.14. </b> "
---

### 5.4.14. Dọn dẹp tài nguyên

Khi kết thúc thực hành, hãy dọn dẹp tài nguyên để tránh phát sinh chi phí.

Các bước chủ yếu:

1. Xóa ECS service
2. Xóa task definition không còn dùng
3. Xóa cluster nếu cần
4. Xóa ECR repositories
5. Xóa load balancer và target group
6. Xóa stack CloudFormation nếu không còn cần thiết

![Hình 17. Dọn dẹp tài nguyên sau triển khai](/5-Workshop/images/5.4-neon-deployment/placeholder-cleanup.png)

