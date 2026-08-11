---
title: "Week 5 Worklog"
date: 2024-01-29
weight: 5
chapter: false
pre: " <b> 1.5. </b> "
---

### Week 5 Objectives:

* Develop the demo web application (frontend and backend).
* Containerize application components using Docker.
* Set up Amazon ECR (Elastic Container Registry) for image storage.
* Deploy containerized application on Amazon ECS (Elastic Container Service).
* Configure ECS task definitions and services.

### Tasks to be carried out this week:
| Day | Task                                                                                                                                                                                   | Start Date | Completion Date | Reference Material                        |
| --- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------- | --------------- | ----------------------------------------- |
| 1   | - Develop frontend: <br>&emsp; + Create React/Vue application <br>&emsp; + Build UI components <br>&emsp; + Integrate with backend API <br>&emsp; + Test locally | 07/09/2026 | 07/09/2026      | React/Vue documentation |
| 2   | - Develop backend API: <br>&emsp; + Create REST API endpoints <br>&emsp; + Implement business logic <br>&emsp; + Connect to RDS and DynamoDB <br>&emsp; + Test API locally | 07/10/2026 | 07/10/2026      | Node.js/Python docs |
| 3   | - Containerize applications: <br>&emsp; + Write Dockerfiles <br>&emsp; + Optimize image sizes <br>&emsp; + Test containers locally <br>&emsp; + Create docker-compose for local dev | 07/11/2026 | 07/11/2026      | <https://docs.docker.com/> |
| 4   | - Set up Amazon ECR and ECS: <br>&emsp; + Create ECR repositories <br>&emsp; + Push images to ECR <br>&emsp; + Create ECS cluster <br>&emsp; + Configure task definitions | 07/12/2026 | 07/12/2026      | <https://000048.awsstudygroup.com/> |
| 5   | - Deploy to ECS: <br>&emsp; + Create ECS services <br>&emsp; + Configure load balancer integration <br>&emsp; + Set up auto scaling <br>&emsp; + Test deployment | 07/13/2026 | 07/13/2026      | <https://000048.awsstudygroup.com/> |


### Week 5 Achievements:

* **Application Development:**
  * Built functional React/Vue frontend with responsive UI
  * Developed RESTful backend API with Node.js/Python
  * Implemented authentication and authorization
  * Connected backend to RDS (PostgreSQL) and DynamoDB
  * Created comprehensive API documentation

* **Containerization:**
  * Created optimized Dockerfiles for frontend and backend
  * Implemented multi-stage builds to reduce image size
  * Configured environment variables and secrets management
  * Tested containers locally with docker-compose
  * Prepared images for production deployment

* **Amazon ECR Setup:**
  * Created private ECR repositories for application images
  * Configured ECR lifecycle policies for image retention
  * Pushed Docker images to ECR successfully
  * Set up ECR scanning for vulnerabilities

* **Amazon ECS Deployment:**
  * Created ECS Fargate cluster for serverless containers
  * Defined ECS task definitions with appropriate resource allocation
  * Configured ECS services with desired count and placement strategies
  * Integrated ECS with Application Load Balancer from Week 2
  * Set up ECS service auto scaling based on CPU/memory
  * Configured CloudWatch Logs for container logging
  * Successfully deployed application to production

* **Key Achievements:**
  * Fully functional cloud-native application
  * Containerized microservices architecture
  * Production deployment on ECS
  * Integrated with AWS services (RDS, DynamoDB, ALB)
  * Ready for staging environment and testing in Week 6