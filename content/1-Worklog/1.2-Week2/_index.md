---
title: "Week 2 Worklog"
date: 2024-01-08
weight: 2
chapter: false
pre: " <b> 1.2. </b> "
---

### Week 2 Objectives:

* Master Amazon EC2 fundamentals and instance management.
* Understand IAM roles for EC2 and apply least privilege principles.
* Learn load balancing concepts with Application Load Balancer (ALB) and Network Load Balancer (NLB).
* Implement Auto Scaling Groups for high availability and elasticity.
* Set up comprehensive monitoring and alerting with CloudWatch.

### Tasks to be carried out this week:
| Day | Task                                                                                                                                                                                   | Start Date | Completion Date | Reference Material                        |
| --- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------- | --------------- | ----------------------------------------- |
| 1   | - Learn EC2 fundamentals: <br>&emsp; + Instance types and families (t3, m5, c5, r5, etc.) <br>&emsp; + AMI (Amazon Machine Images) <br>&emsp; + Storage options (EBS volumes, instance store) <br>&emsp; + Key pairs and SSH access <br> - **Practice:** <br>&emsp; + Launch EC2 instances <br>&emsp; + Connect via SSH <br>&emsp; + Manage EBS volumes | 06/18/2026 | 06/18/2026      | <https://000004.awsstudygroup.com/> |
| 2   | - Learn IAM Roles for EC2: <br>&emsp; + Service roles vs user roles <br>&emsp; + EC2 instance profiles <br>&emsp; + Temporary credentials via metadata service <br>&emsp; + Best practices for service access <br> - **Practice:** <br>&emsp; + Create IAM role for EC2 <br>&emsp; + Attach role to instance <br>&emsp; + Test AWS CLI from instance without access keys | 06/19/2026 | 06/19/2026      | <https://000008.awsstudygroup.com/> |
| 3   | - Learn about Load Balancers: <br>&emsp; + Application Load Balancer (ALB) - Layer 7 <br>&emsp; + Network Load Balancer (NLB) - Layer 4 <br>&emsp; + Target groups and health checks <br>&emsp; + Listener rules and routing <br> - **Practice:** <br>&emsp; + Create ALB <br>&emsp; + Configure target group <br>&emsp; + Set up health checks <br>&emsp; + Test load distribution | 06/20/2026 | 06/20/2026      | <https://000045.awsstudygroup.com/> |
| 4   | - Learn Auto Scaling: <br>&emsp; + Launch templates <br>&emsp; + Auto Scaling Groups (ASG) <br>&emsp; + Scaling policies (target tracking, step, simple) <br>&emsp; + Desired, minimum, maximum capacity <br> - **Practice:** <br>&emsp; + Create launch template <br>&emsp; + Set up Auto Scaling Group <br>&emsp; + Configure scaling policies <br>&emsp; + Test scale-out and scale-in | 06/21/2026 | 06/21/2026      | <https://000047.awsstudygroup.com/> |
| 5   | - Learn CloudWatch monitoring: <br>&emsp; + Metrics (built-in and custom) <br>&emsp; + Logs and log groups <br>&emsp; + Alarms and notifications <br>&emsp; + Dashboards <br>&emsp; + CloudWatch Agent <br> - **Practice:** <br>&emsp; + Set up CloudWatch alarms <br>&emsp; + Create custom metrics <br>&emsp; + Configure log aggregation <br>&emsp; + Build monitoring dashboard | 06/22/2026 | 06/22/2026      | <https://000051.awsstudygroup.com/> |


### Week 2 Achievements:

* **Amazon EC2 Mastery:**
  * Understood EC2 instance types and selection criteria:
    * General Purpose (t3, t3a, m5) - balanced compute, memory, network
    * Compute Optimized (c5, c6i) - high-performance processors
    * Memory Optimized (r5, r6i) - for memory-intensive applications
    * Storage Optimized (i3, d2) - high IOPS and throughput
  * Learned EC2 instance lifecycle:
    * Launch, start, stop, terminate, reboot
    * Instance states and billing implications
  * Mastered storage options:
    * EBS volumes (gp3, gp2, io2, st1, sc1)
    * Instance store (ephemeral storage)
    * EBS snapshots and backup strategies
  * Practiced instance management:
    * Launched multiple EC2 instances in VPC from Week 1
    * Configured security groups for web and app tiers
    * Generated and managed SSH key pairs
    * Connected to instances using SSH and Session Manager
    * Attached and mounted EBS volumes
    * Created EBS snapshots for backup
  * Understood AMI concepts:
    * Public, private, and shared AMIs
    * Creating custom AMIs from instances
    * AMI lifecycle and deregistration

* **IAM Roles for EC2:**
  * Deep understanding of service roles:
    * Difference between IAM users and IAM roles
    * How EC2 retrieves temporary credentials via instance metadata
    * Instance profiles (container for IAM role)
  * Best practices for EC2 security:
    * Never hardcode credentials in applications
    * Use IAM roles for all AWS API access
    * Rotate credentials automatically
    * Principle of least privilege for role policies
  * Practical implementation:
    * Created IAM role with S3 read-only access
    * Created IAM role with CloudWatch logging permissions
    * Attached roles to running instances
    * Tested AWS CLI commands without configuring credentials
    * Verified temporary credentials via metadata endpoint
  * Understood trust policies and permissions boundaries

* **Load Balancing Architecture:**
  * Learned load balancer types and use cases:
    * **Application Load Balancer (ALB):**
      * Layer 7 (HTTP/HTTPS) routing
      * Path-based and host-based routing
      * WebSocket and HTTP/2 support
      * Integration with WAF for security
    * **Network Load Balancer (NLB):**
      * Layer 4 (TCP/UDP) routing
      * Ultra-low latency and high throughput
      * Static IP addresses and Elastic IP support
      * PrivateLink integration
  * Understood load balancer components:
    * Listeners (protocol and port configuration)
    * Target groups (instances, IPs, Lambda functions)
    * Health checks (interval, timeout, threshold)
    * Routing rules and conditions
  * Implemented practical load balancing:
    * Created ALB in public subnets
    * Configured target group with multiple EC2 instances
    * Set up health checks (HTTP GET /health)
    * Configured listener rules for different paths
    * Tested traffic distribution across instances
    * Monitored target health in console
  * Understood advanced features:
    * SSL/TLS termination
    * Sticky sessions (session affinity)
    * Connection draining
    * Cross-zone load balancing

* **Auto Scaling Implementation:**
  * Mastered Auto Scaling concepts:
    * Elasticity and scalability principles
    * Horizontal scaling vs vertical scaling
    * Launch templates vs launch configurations
  * Learned scaling components:
    * Launch template (AMI, instance type, user data, security groups)
    * Auto Scaling Group (desired, min, max capacity)
    * Scaling policies (when and how to scale)
    * Cooldown periods
  * Understood scaling policy types:
    * Target tracking scaling (maintain metric at target value)
    * Step scaling (scale based on metric breach size)
    * Simple scaling (scale by fixed amount)
    * Scheduled scaling (predictable patterns)
  * Implemented production-ready Auto Scaling:
    * Created launch template with web application
    * Configured Auto Scaling Group with min=2, max=6, desired=2
    * Set up target tracking policy (CPU utilization at 70%)
    * Integrated ASG with ALB target group
    * Configured health checks (EC2 + ELB)
    * Tested automatic scale-out under load
    * Tested automatic scale-in after load decrease
    * Verified zero-downtime during scaling events
  * Understood ASG best practices:
    * Multi-AZ distribution for high availability
    * Using multiple instance types for cost optimization
    * Proper health check grace period
    * Instance protection for controlled updates

* **CloudWatch Monitoring & Observability:**
  * Learned CloudWatch components:
    * **Metrics:** Time-series data points
      * Default EC2 metrics (CPU, Network, Disk)
      * Custom metrics via PutMetricData API
      * Metric resolution (standard 5-min, high-resolution 1-sec)
    * **Logs:** Centralized log aggregation
      * Log groups and log streams
      * Log retention policies
      * Log Insights for querying
    * **Alarms:** Automated notifications
      * Metric alarms (threshold-based)
      * Composite alarms (combine multiple alarms)
      * Alarm actions (SNS, Auto Scaling, EC2 actions)
    * **Dashboards:** Visual representation of metrics
  * Implemented comprehensive monitoring:
    * Created CloudWatch alarms for critical metrics:
      * High CPU utilization (>80% for 5 minutes)
      * Low memory available (custom metric)
      * High disk usage
      * ALB unhealthy target count
      * ALB 5XX errors
    * Set up SNS topics for alarm notifications
    * Subscribed email addresses to SNS topics
    * Installed CloudWatch Agent on EC2 instances
    * Configured agent to collect:
      * Memory utilization
      * Disk space utilization
      * Custom application metrics
    * Set up log aggregation:
      * Application logs to CloudWatch Logs
      * System logs (syslog, auth.log)
      * Web server access and error logs
    * Created CloudWatch dashboard showing:
      * EC2 instance metrics
      * ALB metrics
      * ASG metrics
      * Custom application metrics
    * Used CloudWatch Logs Insights for log analysis
  * Understood CloudWatch best practices:
    * Setting appropriate alarm thresholds
    * Using composite alarms to reduce noise
    * Implementing log retention policies
    * Tagging resources for cost allocation

* **Integrated Architecture Achievement:**
  * Successfully built a complete, production-ready compute tier:
    * Multi-AZ deployment with Auto Scaling
    * Application Load Balancer for traffic distribution
    * Health checks ensuring only healthy instances serve traffic
    * Automatic scaling based on demand
    * Comprehensive monitoring and alerting
    * Secure access using IAM roles (no hardcoded credentials)
  * Tested end-to-end functionality:
    * Deployed sample web application
    * Verified load balancing across instances
    * Simulated high load to trigger scale-out
    * Verified new instances automatically added to ALB
    * Confirmed alarms triggered appropriately
    * Tested instance failure and automatic replacement

* **Key Takeaways:**
  * Can design and implement highly available, auto-scaling applications
  * Understand how to properly secure EC2 instances using IAM roles
  * Know how to implement effective load balancing strategies
  * Can set up production-grade monitoring and alerting
  * Ready to build resilient applications that handle variable traffic
  * Prepared for next week's storage and database services