---
title : "Kích hoạt pipeline"
date : 2024-01-01
weight : 10
chapter : false
pre : " <b> 5.4.10. </b> "
---

### 5.4.10. Kích hoạt pipeline

1. Chuyển sang nhánh `main`.
2. Merge branch `develop` vào `main`.
3. Push code lên `main` để trigger pipeline.

Ví dụ:

```bash
git checkout main
git merge develop
git push origin main
```

![Hình 10. Trigger pipeline](/5-Workshop/images/5.4-neon-deployment/placeholder-trigger-pipeline.png)


