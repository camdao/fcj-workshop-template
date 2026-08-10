---
title: "CloudWatch Monitoring and Alerting"
date: 2026-08-05
weight: 6
chapter: false
pre: " <b> 5.4.6. </b> "
---
After the application is deployed, configure CloudWatch to monitor logs and resource health, and to receive alerts when an abnormal condition occurs. This section covers the main operations; section 5.5 verifies the resulting data after deployment.

## 1. Collect logs and use Logs Insights

### Configure ECS log groups

1. In the frontend and backend task definitions, select the **awslogs** log driver, use Region `ap-southeast-1`, and configure these log groups.

| Service      | Log group                     |
| ------------ | ----------------------------- |
| Backend ECS  | `/ecs/neonfoodmap-backend`  |
| Frontend ECS | `/ecs/neonfoodmap-frontend` |

2. Open **CloudWatch → Log groups**, open each group, choose **Actions → Edit retention setting**, and set retention to `30 days`.

![CloudWatch Log Groups list](images/image079.png)

3. After the ECS service starts tasks, check the log streams to confirm that the containers are writing logs.

![ECS backend log streams in CloudWatch](images/image106.png)

### Save Logs Insights queries

1. Open **CloudWatch → Logs Insights** and select the backend log group.
2. Create, run, and save operational queries to find errors/exceptions, check health checks, and filter 5XX requests. Adapt fields and patterns to the application log format.

![Open CloudWatch Logs Insights](images/image105.png)

![Save a CloudWatch Logs Insights query](images/image107.png)

## 2. Create an operational dashboard

1. Open **CloudWatch → Dashboards → Create dashboard** and name it `NeonFoodMap-Operational-Dashboard`.

![Create a CloudWatch dashboard](images/image067.png)

2. Choose **Add widget**, then select an appropriate widget type such as **Line** or **Number**.

![Add a CloudWatch dashboard widget](images/image068.png)

3. Add key metrics: ECS CPU/memory and task count; ALB request count, target response time, healthy hosts, and 5XX errors; RDS CPU, connection count, and free storage.

![Select Application Load Balancer metrics](images/image070.png)

![CloudWatch dashboard with ECS, ALB, and Logs Insights metrics](images/image076.png)

## 3. Create alarms and SNS notifications

1. Create an SNS topic named `NeonFoodMap-Alerts` in **Amazon SNS → Topics**, then create and confirm an **Email** subscription.

![Create an SNS topic](images/image047.png)

![Create an SNS email subscription](images/image048.png)

2. Open **CloudWatch → Alarms → Create alarm**, choose a metric, set its threshold, and select `NeonFoodMap-Alerts` as the notification action.

![Create a CloudWatch alarm](images/image050.png)

3. Create these two alarms: ![Tạo Alarm 1](images/image055.png) ![Tạo Alarm 2](images/image056.png)

| Alarm                         | Metric                              | Threshold                    |
| ----------------------------- | ----------------------------------- | ---------------------------- |
| `ECS-Backend-HighCPU-Alarm` | `ECSServiceAverageCPUUtilization` | `>= 80%` for `5 minutes` |
| `ALB-5XX-Error-Alarm`       | `HTTPCode_Target_5XX_Count`       | `>= 10` for `1 minute`   |

4. Confirm that each alarm is **OK** or **Insufficient data**. Test alarms in a test environment only; do not create artificial errors in production.

![Configured CloudWatch alarms](images/image065.png)

## 4. Enable VPC Flow Logs (optional)

1. Open **Amazon VPC → Your VPCs**, select the system VPC, and open the **Flow Logs** tab.

![Select a VPC to configure Flow Logs](images/image098.png)

2. Choose **Create flow log**.

![Create a VPC Flow Log](images/image100.png)

3. Set **Traffic type** to `All`, set **Destination** to `CloudWatch Logs`, then choose a dedicated log group and an appropriate IAM role.

![Configure CloudWatch Logs as the VPC Flow Logs destination](images/image102.png)

4. Create the Flow Log and confirm that its state is `Active`. Enable Flow Logs only when needed because log storage and queries incur costs.

![VPC Flow Log created with CloudWatch Logs as the destination](images/image103.png)
