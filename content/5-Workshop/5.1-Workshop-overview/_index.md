---
title: "Workshop Overview"
date: 2026-08-03
weight: 1
chapter: false
pre: " <b> 5.1. </b> "
---

## 1. Project Introduction

**NeonFoodMap** is an automated digital tourism platform for **Vinh Khanh Food Street, District 4, Ho Chi Minh City**. It helps visitors discover culinary and cultural destinations through interactive maps, POI information, multimedia content, and audio guides accessible via location detection or QR code.

**Repository:** [github.com/HaoWasabi/NeonFoodmap](https://github.com/HaoWasabi/NeonFoodmap)

**Target Users:**
- **Visitors**: Search destinations and access audio guides
- **Business Partners**: Update menus and promotions
- **Administrators**: Manage content, users, and operations

**Technology:**
- Frontend: React SPA
- Backend: Django REST API
- Database: MySQL

## 2. Problem & Solution

### Current Challenges

**Business Operations:**
- **Fragmented Information**: Location data, menus, images, and audio content are scattered across multiple platforms and systems, making it difficult to maintain consistency and provide a unified experience
- **High Operational Costs**: Manual content management and updates require significant time and human resources
- **Limited Scalability**: Existing systems struggle to handle large volumes of visitors efficiently, especially during peak tourism seasons
- **Inconsistent Experience**: Visitors receive different quality of information depending on access channels

**Technical Infrastructure:**
- **Security Vulnerabilities**: Exposed databases, hardcoded credentials, and lack of proper access controls create significant security risks
- **Manual Deployment**: Time-consuming manual deployment processes lead to slower release cycles and higher risk of human error
- **No Monitoring**: Lack of proper logging, metrics, and alerting makes it difficult to identify and resolve issues quickly
- **Cost Visibility**: No clear tracking of infrastructure costs or mechanisms to prevent budget overruns

### Solution Approach

NeonFoodMap addresses these challenges through a modern cloud-native architecture:

**Centralized Platform:**
- Single unified platform for all POI content, media, and audio guides
- Consistent API and data model for all user interfaces
- Streamlined content management for business partners

**Secure AWS Infrastructure:**
- Multi-AZ VPC deployment for high availability and fault tolerance
- Private subnets for databases and backend services
- IAM roles and security groups following least-privilege principle
- Encryption at rest and in transit

**Automated CI/CD:**
- GitHub Actions workflows for automated testing and deployment
- OIDC authentication eliminates long-lived AWS credentials
- Zero-downtime rolling updates for backend services
- Automated CloudFront cache invalidation for frontend updates

**Comprehensive Monitoring:**
- CloudWatch logs and metrics for all components
- SNS email alerts for critical issues and anomalies
- AWS Budgets and Cost Anomaly Detection for financial governance
- Dashboards for real-time system health visibility

## 3. Architecture Overview

![Overall Platform Architecture on AWS](images/platform_architecture.jpg)

The system uses a **multi-tier architecture** in Amazon VPC across two Availability Zones in `ap-southeast-1`:

**Architecture Layers:**

| Layer | Components | Purpose |
|-------|-----------|---------|
| **Presentation** | CloudFront, S3 | Deliver React SPA globally with low latency |
| **Application** | ALB, ECS Fargate | Run Django API containers with auto-scaling |
| **Data** | RDS MySQL, S3 | Store business data and media files securely |
| **Network** | VPC, Subnets, Gateways | Isolate and route traffic securely |
| **CI/CD** | GitHub Actions, OIDC, ECR | Automate build and deployment |
| **Monitoring** | CloudWatch, SNS | Track metrics, logs, and send alerts |

## 4. Technology Stack

| Category | Technologies |
|----------|-------------|
| Frontend | React, Vite |
| Backend | Django, Gunicorn, Python, Docker |
| Infrastructure | AWS VPC, ECS Fargate, RDS MySQL, S3, CloudFront, ALB |
| CI/CD | GitHub Actions, GitHub OIDC, AWS STS, ECR |
| Monitoring | CloudWatch, SNS, AWS Budgets, Cost Anomaly Detection |
| Security | IAM, Security Groups, Origin Access Control |
