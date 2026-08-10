---
title : "Create Application Load Balancer and Configure Routing"
date : 2024-01-01
weight : 11
chapter : false
pre : " <b> 5.4.11. </b> "
---

Application Load Balancer (ALB) distributes HTTP/HTTPS traffic to Backend ECS tasks, providing health checking and SSL termination.

---

### 5.4.11.1. Create Security Group for ALB

Security Group controls inbound/outbound traffic for the ALB.

1. Open **EC2 Console** → **Security Groups**
2. Click **Create security group**
3. Configure settings:
   - **Name**: `alb-sg`
   - **Description**: `Security Group for Public Application Load Balancer`
   - **VPC**: Select project VPC
4. Add **Inbound rules**:
   - Type: `HTTP`, Port: `80`, Source: `0.0.0.0/0`
   - Type: `HTTPS`, Port: `443`, Source: `0.0.0.0/0`
5. **Outbound rules**: Keep default (All traffic)
6. Click **Create security group**

![Figure 11. Create ALB security group](/images/5-Workshop/5.4-neon-deployment/placeholder-alb-sg.png)

---

### 5.4.11.2. Create Target Group for Backend

Target Group defines the group of targets (ECS tasks) that ALB routes traffic to.

1. Open **EC2 Console** → **Target Groups**
2. Click **Create target group**
3. Configure **Basic configuration**:
   - **Target type**: `IP addresses` (for Fargate tasks)
   - **Target group name**: `TG-NeonFoodMap-BE`
   - **Protocol**: `HTTP`
   - **Port**: `8000` (Django backend port)
   - **VPC**: Select project VPC

4. Configure **Health checks**:
   - **Health check protocol**: `HTTP`
   - **Health check path**: `/api/health` or `/admin/`
   - **Advanced health check settings**:
     - Healthy threshold: `2`
     - Unhealthy threshold: `2`
     - Timeout: `5 seconds`
     - Interval: `30 seconds`
     - Success codes: `200`

5. Click **Next**
6. **Register targets** step: Skip (ECS Service will register automatically)
7. Click **Create target group**

![](/images/5-Workshop/5.4-Neon-Deployment/image025.png)
![](/images/5-Workshop/5.4-Neon-Deployment/image026.png)
![](/images/5-Workshop/5.4-Neon-Deployment/image027.png)
![](/images/5-Workshop/5.4-Neon-Deployment/image028.png)
![](/images/5-Workshop/5.4-Neon-Deployment/image029.png)

---

### 5.4.11.3. Create Application Load Balancer

1. Open **EC2 Console** → **Load Balancers**
2. Select **Create load balancer** → **Application Load Balancer**
3. Configure **Basic configuration**:
   - **Load balancer name**: `ALB-NeonFoodMap`
   - **Scheme**: `Internet-facing`
   - **IP address type**: `IPv4`

4. Configure **Network mapping**:
   - **VPC**: Select project VPC
   - **Mappings**: Select at least 2 Availability Zones
   - Select **Public subnets** in each AZ

5. Configure **Security groups**:
   - Select `alb-sg` created in step 5.4.11.1
   - Deselect default security group

6. Configure **Listeners and routing**:
   - **Listener**: `HTTP` port `80`
   - **Default action**: Forward to `TG-NeonFoodMap-BE`

7. Review configuration and click **Create load balancer**
8. Wait for ALB to transition to `Active` state

![](/images/5-Workshop/5.4-Neon-Deployment/image030.png)
![](/images/5-Workshop/5.4-Neon-Deployment/image031.png)
![](/images/5-Workshop/5.4-Neon-Deployment/image032.png)
![](/images/5-Workshop/5.4-Neon-Deployment/image033.png)
![](/images/5-Workshop/5.4-Neon-Deployment/image034.png)
![](/images/5-Workshop/5.4-Neon-Deployment/image035.png)
![](/images/5-Workshop/5.4-Neon-Deployment/image036.png)
![](/images/5-Workshop/5.4-Neon-Deployment/image037.png)

---

### 5.4.11.4. Configure Listener Rules (Optional)

For more complex routing (e.g., path-based routing):

1. Open **ALB** → **Listeners and rules**
2. Select listener `HTTP:80`
3. Click **Manage rules**
4. Click **Add rule**
5. Configure rule:
   - **Name**: `route-backend-api`
   - **Condition**: Add condition → **Path** → `/api/*`
   - **Action**: Forward to → `TG-NeonFoodMap-BE`
   - **Priority**: `1`
6. Click **Save**

![](/images/5-Workshop/5.4-Neon-Deployment/image038.png)

![Figure 84.](/images/5-Workshop/5.5-Neon-Operations/image084.png)
![Figure 85.](/images/5-Workshop/5.5-Neon-Operations/image085.png)
![Figure 86.](/images/5-Workshop/5.5-Neon-Operations/image086.png)
![Figure 87.](/images/5-Workshop/5.5-Neon-Operations/image087.png)
![Figure 83.](/images/5-Workshop/5.5-Neon-Operations/image083.png)

---

### Verification

After completion:

| Component | Expected Result |
|-----------|-----------------|
| Security Group | `alb-sg` with inbound HTTP/HTTPS |
| Target Group | `TG-NeonFoodMap-BE` with health check `/api/health` |
| ALB | `ALB-NeonFoodMap` in Active state |
| Listener | HTTP:80 forwards to Backend target group |
| DNS Name | ALB has DNS name like `*.elb.amazonaws.com` |

**Get ALB DNS name:**
```bash
# CLI command to get ALB DNS
aws elbv2 describe-load-balancers \
  --names ALB-NeonFoodMap \
  --query 'LoadBalancers[0].DNSName' \
  --output text
```

Use this DNS name to:
- Configure Route 53 (if using custom domain)
- Test backend API: `http://<ALB-DNS>/api/health`
- Configure in ECS Service