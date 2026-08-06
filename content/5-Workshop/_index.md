---
title: "Workshop"
date: 2024-01-01
weight: 5
chapter: false
pre: " <b> 5. </b> "
---

# NeonFoodMap - Full Stack Application Deployment on AWS

#### Overview

This workshop guides you through the complete process of deploying a full-stack application (NeonFoodMap) on AWS infrastructure. You will learn how to design, build, and operate a production-ready system using modern AWS services and DevOps practices.

The NeonFoodMap application is a location-based food discovery platform that allows users to explore points of interest (POIs), listen to audio commentary, and book premium tours with integrated payment processing.

#### Architecture Overview

The workshop covers deployment of a multi-tier architecture including:
- **Frontend**: React application served via S3 and CloudFront CDN
- **Backend**: Node.js API running on ECS Fargate behind Application Load Balancer
- **Database**: Amazon RDS MySQL for persistent data storage
- **Media Storage**: S3 buckets for images and audio files
- **CI/CD**: GitHub Actions workflow with automated deployment
- **Monitoring**: CloudWatch dashboards, alarms, and log aggregation

#### Content

1. [Workshop Overview](5.1-workshop-overview/)
2. [Prerequisites](5.2-prerequiste/)
3. [Infrastructure Setup](5.3-neon-infrastructure/)
4. [Application Deployment](5.4-neon-deployment/)
5. [Operations and Monitoring](5.5-neon-operations/)