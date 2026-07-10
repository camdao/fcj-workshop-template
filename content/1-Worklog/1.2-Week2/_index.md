---
title: "Week 2 Worklog"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 1.2. </b> "
---
<!-- {{% notice warning %}} 
⚠️ **Note:** The following information is for reference purposes only. Please **do not copy verbatim** for your own report, including this warning.
{{% /notice %}} -->


### Week 2 Objectives:

* Master Amazon EC2 (Elastic Compute Cloud) essentials and compute fundamentals.
* Learn instance profiling with IAM Roles for EC2.
* Understand EC2 instance types, AMI, storage, and networking.

### Tasks to be carried out this week:
| Day | Task                                                                                                                                                                                                   | Start Date | Completion Date | Reference Material                        |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ---------- | --------------- | ----------------------------------------- |
| 2   | - Learn EC2 Compute Essentials: <br>&emsp; + EC2 instance types and families <br>&emsp; + Instance lifecycle and states <br>&emsp; + Pricing models (On-Demand, Reserved, Spot) <br>&emsp; + AMI (Amazon Machine Images) | 06/18/2026 | 06/18/2026      | <https://cloudjourney.awsstudygroup.com/> |
| 3   | - Learn EC2 Storage & Networking: <br>&emsp; + EBS (Elastic Block Store) <br>&emsp; + EBS volume types <br>&emsp; + Security Groups <br>&emsp; + Key pairs <br>&emsp; + Elastic IP                     | 06/19/2026 | 06/19/2026      | <https://cloudjourney.awsstudygroup.com/> |
| 4   | - **Practice:** <br>&emsp; + Launch EC2 instances <br>&emsp; + Configure Security Groups <br>&emsp; + Connect via SSH <br>&emsp; + Attach and manage EBS volumes                                       | 06/20/2026 | 06/20/2026      | <https://cloudjourney.awsstudygroup.com/> |
| 5   | - Learn IAM Roles for EC2: <br>&emsp; + Instance profiles <br>&emsp; + Attaching IAM roles to EC2 <br>&emsp; + AWS credentials management <br>&emsp; + Best practices for EC2 security                 | 06/21/2026 | 06/21/2026      | <https://cloudjourney.awsstudygroup.com/> |
| 6   | - **Practice:** <br>&emsp; + Create IAM roles for EC2 <br>&emsp; + Attach roles to instances <br>&emsp; + Test permissions <br>&emsp; + Access AWS services from EC2 using IAM roles                   | 06/22/2026 | 06/22/2026      | <https://cloudjourney.awsstudygroup.com/> |


### Week 2 Achievements:

* Mastered Amazon EC2 compute essentials:
  * EC2 instance types and families (General Purpose, Compute Optimized, Memory Optimized, etc.)
  * Instance lifecycle and states (pending, running, stopped, terminated)
  * Pricing models (On-Demand, Reserved Instances, Spot Instances, Savings Plans)
  * Understanding when to use different instance types

* Learned about Amazon Machine Images (AMI):
  * AMI types and sources
  * Creating custom AMIs
  * AMI sharing and copying across regions

* Understood EC2 storage options:
  * EBS (Elastic Block Store) volume types (gp3, gp2, io2, st1, sc1)
  * EBS snapshots and backup strategies
  * Instance store vs. EBS
  * Volume attachment and detachment

* Mastered EC2 networking fundamentals:
  * Security Groups configuration and rules
  * Network interfaces (ENI)
  * Elastic IP addresses
  * SSH key pairs management

* Successfully launched and managed EC2 instances:
  * Created instances using different configurations
  * Connected to instances via SSH
  * Configured Security Groups for proper access control
  * Attached and managed EBS volumes

* Learned Instance Profiling with IAM Roles for EC2:
  * Understanding instance profiles
  * Creating IAM roles for EC2 instances
  * Attaching IAM roles to running instances
  * Best practices for EC2 security and permissions

* Practiced IAM Roles implementation:
  * Created IAM roles with appropriate policies
  * Attached roles to EC2 instances
  * Tested access to AWS services from EC2 using roles
  * Eliminated the need for hardcoded credentials

* Understood EC2 security best practices:
  * Principle of least privilege for IAM roles
  * Security Group rule management
  * SSH key management
  * Regular patching and updates

* Gained hands-on experience with EC2 automation and management via Console and CLI.
