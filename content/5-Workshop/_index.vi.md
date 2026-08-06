---
title: "Workshop"
date: 2024-01-01
weight: 5
chapter: false
pre: " <b> 5. </b> "
---

# NeonFoodMap - Triển khai ứng dụng Full Stack trên AWS

#### Tổng quan

Workshop này hướng dẫn bạn qua toàn bộ quy trình triển khai một ứng dụng full-stack (NeonFoodMap) trên hạ tầng AWS. Bạn sẽ học cách thiết kế, xây dựng và vận hành một hệ thống production-ready sử dụng các dịch vụ AWS hiện đại và thực hành DevOps.

Ứng dụng NeonFoodMap là một nền tảng khám phá ẩm thực dựa trên vị trí, cho phép người dùng khám phá các điểm đến (POI), nghe bình luận âm thanh và đặt các tour cao cấp với tích hợp thanh toán.

#### Tổng quan kiến trúc

Workshop bao gồm triển khai kiến trúc đa tầng bao gồm:
- **Frontend**: Ứng dụng React được phục vụ qua S3 và CloudFront CDN
- **Backend**: API Node.js chạy trên ECS Fargate đằng sau Application Load Balancer
- **Database**: Amazon RDS MySQL để lưu trữ dữ liệu bền vững
- **Media Storage**: S3 buckets cho hình ảnh và file âm thanh
- **CI/CD**: GitHub Actions workflow với triển khai tự động
- **Monitoring**: CloudWatch dashboards, alarms và tổng hợp log

#### Nội dung

1. [Tổng quan Workshop](5.1-workshop-overview/)
2. [Yêu cầu tiên quyết](5.2-prerequiste/)
3. [Thiết lập hạ tầng](5.3-neon-infrastructure/)
4. [Triển khai ứng dụng](5.4-neon-deployment/)
5. [Vận hành và giám sát](5.5-neon-operations/)