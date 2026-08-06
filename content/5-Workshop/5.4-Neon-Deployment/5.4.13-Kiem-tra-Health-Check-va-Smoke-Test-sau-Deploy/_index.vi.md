---
title : "Kiểm tra health check và smoke test sau deploy"
date : 2024-01-01
weight : 13
chapter : false
pre : " <b> 5.4.13. </b> "
---

### 5.4.13. Kiểm tra health check và smoke test sau deploy

Sau khi ECS task chạy xong, kiểm tra trạng thái target group.

Các mục cần kiểm tra:

- Target group frontend chuyển sang `Healthy`
- Target group backend chuyển sang `Healthy`
- ALB DNS có thể truy cập bằng browser
- Endpoint `/api/...` trả về response hợp lệ

Ví dụ kiểm tra:

- Frontend: `http://<alb-dns>`
- Backend: `http://<alb-dns>/api/...`

![Hình 16. Kiểm tra health check và smoke test](/5-Workshop/images/5.4-neon-deployment/placeholder-smoke-test.png)

