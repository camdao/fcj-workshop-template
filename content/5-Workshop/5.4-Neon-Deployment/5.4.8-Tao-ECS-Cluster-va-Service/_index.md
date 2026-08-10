---
title : "Create ECS Cluster and Service"
date : 2024-01-01
weight : 8
chapter : false
pre : " <b> 5.4.8. </b> "
---

After completing this section, the system will meet the following requirements:

- Successfully create an ECS Cluster using **AWS Fargate**
- Configure ECS Service using Subnets across **2 Availability Zones (AZ1, AZ2)** for high availability
- Create Task Definition for Backend with CPU **256** and RAM **512 MB**
- Configure CloudWatch Logs for Container
- Set up environment variables and Secrets for the application
- Configure IAM Task Execution Role to allow ECS to pull Docker Images from Amazon ECR and write logs to CloudWatch
- Verify that Tasks start and run correctly

---

### Implementation Steps

#### Step 1. Create ECS Cluster using AWS Fargate

1. Access **AWS Management Console**
2. Search for and select **Amazon ECS** service
3. In the left menu, select **Clusters**
4. Click **Create cluster**
5. For **Cluster name**, enter:

```text
neonfoodmap-cluster
```

6. In the **Infrastructure** section, select:

```text
AWS Fargate (serverless)
```

7. Review cluster configuration
8. Click **Create** to create the Cluster
9. After successful creation, the Cluster will appear in the list

> **Note:** ECS Cluster is a logical resource and is not directly assigned to AZ1 or AZ2. Multi-Availability Zone deployment is configured when creating the ECS Service by selecting Subnets from AZ1 and AZ2.

![](/images/5-Workshop/5.4-Neon-Deployment/image010.png)
![](/images/5-Workshop/5.4-Neon-Deployment/image011.png)
![](/images/5-Workshop/5.4-Neon-Deployment/image012.png)
![](/images/5-Workshop/5.4-Neon-Deployment/image013.png)
![](/images/5-Workshop/5.4-Neon-Deployment/image014.png)
![](/images/5-Workshop/5.4-Neon-Deployment/image015.png)

---

#### Step 2. Create Task Definition for Backend with CPU 256 and RAM 512 MB

Task Definition specifies how ECS launches the Backend Container, including Docker Image, CPU, RAM, Port, Environment Variables, and Log Configuration.

1. In Amazon ECS, select **Task definitions**
2. Click **Create new task definition**
3. Enter Task Definition name:

```text
neonfoodmap-backend
```

4. In **Infrastructure requirements**, select:

```text
AWS Fargate
```

5. Configure resources:

```text
CPU: 0.25 vCPU
Memory: 0.5 GB
```

Which corresponds to:

```text
CPU: 256
RAM: 512 MiB
```

6. For **Task execution role**, select the IAM Role for ECS Task Execution:

```text
NeonFoodmap-TaskExecution-Role
```

7. For **Task role**, select the IAM Role that allows container to access AWS services:

```text
NeonFoodmap-ECS-Backend-Role
```

8. In the **Container** section, click **Add container**
9. Enter Container name:

```text
backend
```

10. For **Image URI**, enter the Backend Docker Image stored in Amazon ECR:

```text
<AWS_ACCOUNT_ID>.dkr.ecr.ap-southeast-1.amazonaws.com/neonfoodmap-backend:latest
```

11. Configure **Port mapping**:

```text
Container port: 8000
Protocol: TCP
App protocol: HTTP
```

12. Configure **Environment variables** required for the application:

```text
DJANGO_SETTINGS_MODULE=config.settings
DEBUG=False
ALLOWED_HOSTS=<DOMAIN>
AWS_REGION=ap-southeast-1
AWS_STORAGE_BUCKET_NAME=<S3_BUCKET_NAME>
```

13. Configure **Secrets** for sensitive information:

```text
DB_HOST: <RDS_ENDPOINT>
DB_NAME: <DATABASE_NAME>
DB_USER: <DATABASE_USER>
DB_PASSWORD: ValueFrom AWS Secrets Manager
```

14. Configure Container Logs using **Amazon CloudWatch Logs**:

```text
Log driver: awslogs
Log Group: /ecs/neonfoodmap-backend
Region: ap-southeast-1
Stream prefix: ecs
```

15. Review configuration and click **Create**

![](/images/5-Workshop/5.4-Neon-Deployment/image016.png)
![](/images/5-Workshop/5.4-Neon-Deployment/image017.png)
![](/images/5-Workshop/5.4-Neon-Deployment/image018.png)
![](/images/5-Workshop/5.4-Neon-Deployment/image019.png)
![](/images/5-Workshop/5.4-Neon-Deployment/image020.png)
![](/images/5-Workshop/5.4-Neon-Deployment/image021.png)
![](/images/5-Workshop/5.4-Neon-Deployment/image022.png)
![](/images/5-Workshop/5.4-Neon-Deployment/image023.png)
![](/images/5-Workshop/5.4-Neon-Deployment/image024.png)

---

#### Step 3. Configure CloudWatch Log Group for Backend

CloudWatch Logs centralize logs from the Backend Container for monitoring and troubleshooting.

1. Access **Amazon CloudWatch** service
2. Select **Logs → Log groups**
3. Click **Create log group**
4. Create Log Group for Backend:

```text
/ecs/neonfoodmap-backend
```

5. Click **Create**
6. Verify the Log Group appears
7. Confirm the Log Group name in Task Definition matches the created Log Group

> When ECS Task starts, container logs will be sent to the Log Group through the `awslogs` configuration.

---

#### Step 4. Configure Environment Variables and Secrets

##### 4.1. Environment Variables Configuration

In the Backend Task Definition, configure non-sensitive variables:

```text
DJANGO_SETTINGS_MODULE=config.settings
DEBUG=False
ALLOWED_HOSTS=api.neonfoodmap.example.com
AWS_REGION=ap-southeast-1
AWS_STORAGE_BUCKET_NAME=neonfoodmap-media
```

##### 4.2. Secrets Configuration for RDS

Sensitive database connection information is stored in **AWS Secrets Manager**:

1. Open the **Secrets** section of the Backend Container
2. Click **Add secret**
3. Configure:

```text
Name: DB_PASSWORD
ValueFrom: arn:aws:secretsmanager:ap-southeast-1:<ACCOUNT_ID>:secret:rds-credentials
```

##### 4.3. API Keys Configuration

For external service API Keys:

```text
Name: GOOGLE_TTS_API_KEY
ValueFrom: arn:aws:secretsmanager:ap-southeast-1:<ACCOUNT_ID>:secret:google-tts-key
```

> The Task needs permission to access Secrets from AWS Secrets Manager through the Task Execution Role.

---

#### Step 5. Configure Task Execution Role

Task Execution Role allows ECS to perform necessary operations during Task startup.

1. Access **AWS Console → IAM**
2. Select **Roles**
3. Find Role:

```text
NeonFoodmap-TaskExecution-Role
```

4. Verify the Role has permissions to:
   - Pull Docker Images from Amazon ECR
   - Write Container Logs to CloudWatch Logs
   - Access Secrets from AWS Secrets Manager

5. Required managed policies:
   - `AmazonECSTaskExecutionRolePolicy`
   - Custom policy for Secrets Manager (if using Secrets)

6. Return to Task Definition and confirm it uses this Role

---

### Verification

After completing the steps above, verify the configuration:

| Component | Expected Result |
|-----------|-----------------|
| ECS Cluster | Created and in `ACTIVE` state |
| Backend Task Definition | Created, CPU 256 and RAM 512 MiB |
| Backend Image | Points to Backend Repository in ECR |
| CloudWatch Logs | Has `/ecs/neonfoodmap-backend` |
| Environment Variables | Configured |
| Secrets | Configured via Secrets Manager |
| Task Execution Role | Assigned to Backend Task Definition |
| Task Role | Assigned to Backend (S3 access) |
| ECR Permission | Allows ECS to pull Image |

After completing these configurations, the system is ready to create an **ECS Service** and deploy Tasks across Subnets in **AZ1 and AZ2**.

![](/images/5-Workshop/5.4-Neon-Deployment/image039.png)
![](/images/5-Workshop/5.4-Neon-Deployment/image040.png)
![](/images/5-Workshop/5.4-Neon-Deployment/image041.png)
![](/images/5-Workshop/5.4-Neon-Deployment/image042.png)