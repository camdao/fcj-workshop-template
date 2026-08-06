---
title : "Khởi tạo và cấu hình S3"
date : 2024-01-01
weight : 3
chapter : false
pre : " <b> 5.3.3. </b> "
---

### 5.3.11. Tạo 4 bucket S3 cho hệ thống

Tạo các bucket theo chức năng sau:

- `frontend`
- `media`
- `audio`
- `logs`

Các bước:

1. Mở Amazon S3 Console.
2. Chọn Create bucket.
3. Nhập tên bucket duy nhất trên AWS.
4. Chọn cùng region với VPC và RDS.
5. Giữ `Block all public access` ở trạng thái Enabled.
6. Nhấn Create bucket.
7. Lặp lại cho đủ 4 bucket.

![Hình 11. Tạo S3 buckets](/5-Workshop/images/5.3-neon-infrastructure/placeholder-s3-buckets.png)

### 5.3.12. Bật Versioning cho media và audio bucket

1. Chọn bucket `neonfoodmap-media-dev`.
2. Vào tab Properties.
3. Chọn Bucket Versioning → Edit.
4. Chọn Enable.
5. Lặp lại tương tự với bucket `neonfoodmap-audio-dev`.

![Hình 12. Bật Versioning](/5-Workshop/images/5.3-neon-infrastructure/placeholder-s3-versioning.png)

### 5.3.13. Cấu hình lifecycle rule cho bucket lưu trữ

1. Chọn bucket cần áp dụng lifecycle.
2. Vào Management → Lifecycle rules.
3. Chọn Create lifecycle rule.
4. Đặt tên ví dụ: `Move-to-IA-after-90d`.
5. Chọn Apply to all objects in the bucket.
6. Chọn chuyển object sang `Standard-IA` sau 90 ngày.

![Hình 13. Cấu hình Lifecycle Rule](/5-Workshop/images/5.3-neon-infrastructure/placeholder-s3-lifecycle.png)

### 5.3.14. Chặn truy cập public và bật ACL cho bucket

1. Chọn bucket.
2. Vào tab Permissions.
3. Chọn Block public access → Edit.
4. Bật tất cả tùy chọn Block all public access.
5. Lưu lại.
6. Vào Object Ownership → Edit.
7. Chọn `ACLs enabled`.
8. Chọn `Bucket owner preferred`.
9. Nhấn Save changes.

![Hình 14. Cấu hình quyền truy cập bucket](/5-Workshop/images/5.3-neon-infrastructure/placeholder-s3-permissions.png)
