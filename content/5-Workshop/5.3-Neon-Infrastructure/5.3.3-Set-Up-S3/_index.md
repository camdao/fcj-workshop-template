---
title : "Initialize and Configure S3"
date : 2024-01-01
weight : 3
chapter : false
pre : " <b> 5.3.3. </b> "
---

### 5.3.11. Create 4 S3 Buckets for the System

Create buckets for the following purposes:

- `frontend`
- `media`
- `audio`
- `logs`

Steps:

1. Open the Amazon S3 Console.
2. Click **Create bucket**.
3. Enter a globally unique bucket name on AWS.
4. Select the same region as your VPC and RDS.
5. Keep **Block all public access** set to Enabled.
6. Click **Create bucket**.
7. Repeat for all 4 buckets.

![Figure 11. Create S3 buckets](/5-Workshop/images/5.3-neon-infrastructure/placeholder-s3-buckets.png)

### 5.3.12. Enable Versioning for Media and Audio Buckets

1. Select the `neonfoodmap-media-dev` bucket.
2. Go to the **Properties** tab.
3. Select **Bucket Versioning** → **Edit**.
4. Choose **Enable**.
5. Repeat the same steps for the `neonfoodmap-audio-dev` bucket.

![Figure 12. Enable Versioning](/5-Workshop/images/5.3-neon-infrastructure/placeholder-s3-versioning.png)

### 5.3.13. Configure Lifecycle Rule for Storage Bucket

1. Select the bucket you want to apply the lifecycle rule to.
2. Go to **Management** → **Lifecycle rules**.
3. Click **Create lifecycle rule**.
4. Name it, for example: `Move-to-IA-after-90d`.
5. Select **Apply to all objects in the bucket**.
6. Choose to transition objects to `Standard-IA` after 90 days.

![Figure 13. Configure Lifecycle Rule](/5-Workshop/images/5.3-neon-infrastructure/placeholder-s3-lifecycle.png)

### 5.3.14. Block Public Access and Enable ACL for Bucket

1. Select the bucket.
2. Go to the **Permissions** tab.
3. Select **Block public access** → **Edit**.
4. Enable all **Block all public access** options.
5. Save.
6. Go to **Object Ownership** → **Edit**.
7. Select `ACLs enabled`.
8. Select `Bucket owner preferred`.
9. Click **Save changes**.

![Figure 14. Configure bucket access permissions](/5-Workshop/images/5.3-neon-infrastructure/placeholder-s3-permissions.png)
