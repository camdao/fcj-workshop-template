---
title : "Kiểm tra pipeline CI/CD"
date : 2024-01-01
weight : 9
chapter : false
pre : " <b> 5.4.9. </b> "
---

### 5.4.9. Kiểm tra pipeline CI/CD

Pipeline chính gồm 6 job theo thứ tự:

1. `backend-test`
2. `frontend-check`
3. `e2e-tests`
4. `build-and-push`
5. `deploy-backend`
6. `smoke-tests`

#### Trigger policy

- Push vào `main` → chạy toàn bộ pipeline
- Push vào `develop` hoặc `feature/**` → chạy các job test cơ bản
- Pull request về `main` → chạy các job test cơ bản

![Hình 9. Pipeline CI/CD](/5-Workshop/images/5.4-neon-deployment/placeholder-pipeline.png)

