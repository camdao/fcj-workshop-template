---
title: "Week 1 Worklog"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 1.1. </b> "
---

### Week 1 Objectives:

* Connect and get acquainted with members of First Cloud Journey - AWS Study Group.
* Understand AWS fundamentals and core service categories.
* Master IAM (Identity and Access Management) for secure access control.
* Learn AWS Budgets for cost management and monitoring.
* Understand VPC networking fundamentals including subnets, security groups, and routing.

### Tasks to be carried out this week:
| Day | Task                                                                                                                                                                                   | Start Date | Completion Date | Reference Material                        |
| --- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------- | --------------- | ----------------------------------------- |
| 1   | - Get acquainted with FCAJ members <br> - Read and take note of internship unit rules and regulations                                                                                   | 06/11/2026 | 06/11/2026      |
| 2   | - Learn about AWS and its service categories <br>&emsp; + Compute (EC2, Lambda, ECS) <br>&emsp; + Storage (S3, EBS, EFS) <br>&emsp; + Networking (VPC, Route 53, CloudFront) <br>&emsp; + Database (RDS, DynamoDB) <br> - Create AWS Free Tier account <br> - Install & configure AWS CLI | 06/12/2026 | 06/12/2026      | <https://cloudjourney.awsstudygroup.com/> |
| 3   | - Deep dive into IAM: <br>&emsp; + Users, Groups, Roles <br>&emsp; + Policies and Permissions (managed vs inline) <br>&emsp; + MFA (Multi-Factor Authentication) <br>&emsp; + Best practices and least privilege <br> - **Practice:** <br>&emsp; + Create IAM users and groups <br>&emsp; + Assign policies <br>&emsp; + Set up MFA <br>&emsp; + Create service roles | 06/13/2026 | 06/13/2026      | <https://000007.awsstudygroup.com/> |
| 4   | - Learn about AWS Budgets: <br>&emsp; + Setting up cost alerts <br>&emsp; + Budget types (Cost, Usage, Reservation) <br>&emsp; + Monitoring usage and forecasting <br> - **Practice:** <br>&emsp; + Create monthly budget <br>&emsp; + Configure budget alerts <br>&emsp; + Set up billing alarms | 06/14/2026 | 06/14/2026      | <https://000002.awsstudygroup.com/> |
| 5   | - Learn VPC fundamentals: <br>&emsp; + VPC concepts and CIDR blocks <br>&emsp; + Public vs Private subnets <br>&emsp; + Internet Gateway and NAT Gateway <br>&emsp; + Route Tables <br>&emsp; + Security Groups vs NACLs <br> - **Practice:** <br>&emsp; + Create custom VPC <br>&emsp; + Configure subnets <br>&emsp; + Set up routing | 06/15/2026 | 06/15/2026      | <https://000003.awsstudygroup.com/> |


### Week 1 Achievements:

* Connected and became acquainted with First Cloud Journey team members and understood internship objectives.

* **AWS Fundamentals:**
  * Understood AWS global infrastructure (Regions, Availability Zones)
  * Learned core service categories:
    * Compute (EC2, Lambda, ECS, Fargate)
    * Storage (S3, EBS, EFS, Glacier)
    * Networking (VPC, Route 53, CloudFront, Direct Connect)
    * Database (RDS, DynamoDB, Aurora, ElastiCache)
    * Management & Governance (CloudWatch, CloudTrail, CloudFormation)
    * Security, Identity & Compliance (IAM, KMS, Secrets Manager)

* **Account Setup:**
  * Successfully created and configured AWS Free Tier account
  * Became familiar with AWS Management Console navigation
  * Installed and configured AWS CLI:
    * Access Key and Secret Key configuration
    * Default Region setup (e.g., us-east-1)
    * Output format configuration (json/yaml/table)
  * Verified CLI functionality with basic commands (`aws sts get-caller-identity`)

* **IAM Security Mastery:**
  * Deep understanding of IAM components:
    * Users (individual identities with long-term credentials)
    * Groups (collection of users with shared permissions)
    * Roles (temporary credentials for services/applications)
    * Policies (JSON documents defining permissions)
  * Learned policy types:
    * AWS Managed Policies (pre-built by AWS)
    * Customer Managed Policies (custom policies)
    * Inline Policies (directly attached to user/group/role)
  * Understood permission evaluation logic and policy structure
  * Implemented Multi-Factor Authentication (MFA) for enhanced security
  * Applied security best practices:
    * Principle of least privilege
    * Regular credential rotation
    * No root account usage for daily operations
    * Individual IAM users instead of shared credentials
  * Created practical IAM resources:
    * Admin user with MFA enabled
    * Developer group with appropriate permissions
    * EC2 service role for future use

* **Cost Management with AWS Budgets:**
  * Learned budget types and use cases:
    * Cost budgets (track spending)
    * Usage budgets (track service usage)
    * Reservation budgets (track RI utilization)
    * Savings Plans budgets
  * Set up comprehensive cost monitoring:
    * Created monthly budget with threshold alerts (e.g., $10/month)
    * Configured email notifications at 50%, 80%, and 100% thresholds
    * Set up CloudWatch billing alarms
  * Understood AWS Cost Explorer and cost allocation tags
  * Learned cost optimization strategies:
    * Right-sizing resources
    * Using Reserved Instances for predictable workloads
    * Implementing auto-scaling
    * Leveraging S3 lifecycle policies

* **VPC Networking Fundamentals:**
  * Understood VPC concepts:
    * Virtual private network in AWS cloud
    * CIDR notation and IP address planning
    * VPC sizing best practices (e.g., /16 for production)
  * Learned subnet design:
    * Public subnets (with Internet Gateway route)
    * Private subnets (for backend resources)
    * Subnet sizing and availability zone distribution
  * Mastered networking components:
    * Internet Gateway (IGW) - for public internet access
    * NAT Gateway - for private subnet outbound access
    * Route Tables - directing network traffic
    * Security Groups - stateful instance-level firewall
    * Network ACLs - stateless subnet-level firewall
  * Created hands-on VPC architecture:
    * Custom VPC with 10.0.0.0/16 CIDR block
    * Public subnet (10.0.1.0/24) in us-east-1a
    * Private subnet (10.0.2.0/24) in us-east-1b
    * Configured Internet Gateway and NAT Gateway
    * Set up route tables for public and private subnets
    * Created security groups with appropriate inbound/outbound rules
  * Understood VPC best practices:
    * Multi-AZ deployment for high availability
    * Separate subnets for different tiers (web, app, database)
    * Minimal security group rules (principle of least privilege)
    * Use of VPC Flow Logs for network monitoring

* **Key Takeaways:**
  * Acquired foundational knowledge to manage AWS resources securely
  * Understand how to implement defense-in-depth security with IAM and network controls
  * Can monitor and control AWS costs effectively
  * Ready to deploy resources in properly architected VPC environments
  * Prepared for next week's compute services with solid networking foundation