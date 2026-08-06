---
title: "Week 7 Worklog"
date: 2024-01-01
weight: 7
chapter: false
pre: " <b> 1.7. </b> "
---

### Week 7 Objectives:

* Master AWS CloudFormation for Infrastructure as Code.
* Understand template structure and resource management.
* Learn stack operations and change sets.
* Practice automating infrastructure deployment.

### Tasks to be carried out this week:
| Day | Task                                                                                                                                                                                                   | Start Date | Completion Date | Reference Material                        |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ---------- | --------------- | ----------------------------------------- |
| 2   | - Learn CloudFormation Fundamentals: <br>&emsp; + Infrastructure as Code concepts <br>&emsp; + Template anatomy (YAML/JSON) <br>&emsp; + Resources, parameters, outputs <br>&emsp; + Intrinsic functions | 07/23/2026 | 07/23/2026      | <https://cloudjourney.awsstudygroup.com/> |
| 3   | - Learn Stack Management: <br>&emsp; + Creating and updating stacks <br>&emsp; + Change sets <br>&emsp; + Stack policies <br>&emsp; + Drift detection                                                 | 07/24/2026 | 07/24/2026      | <https://cloudjourney.awsstudygroup.com/> |
| 4   | - **Practice:** <br>&emsp; + Write CloudFormation templates <br>&emsp; + Create stacks from templates <br>&emsp; + Use parameters and mappings <br>&emsp; + Configure outputs                         | 07/25/2026 | 07/25/2026      | <https://cloudjourney.awsstudygroup.com/> |
| 5   | - Learn Advanced Features: <br>&emsp; + Nested stacks <br>&emsp; + Cross-stack references <br>&emsp; + Custom resources <br>&emsp; + StackSets for multi-account/region                              | 07/26/2026 | 07/26/2026      | <https://cloudjourney.awsstudygroup.com/> |
| 6   | - **Practice:** <br>&emsp; + Create nested stacks <br>&emsp; + Implement cross-stack references <br>&emsp; + Use change sets <br>&emsp; + Deploy multi-tier application                               | 07/27/2026 | 07/27/2026      | <https://cloudjourney.awsstudygroup.com/> |


### Week 7 Achievements:

* Mastered Infrastructure as Code concepts:
  * Understanding benefits of IaC (version control, repeatability, automation)
  * CloudFormation vs. other IaC tools
  * Declarative vs. imperative approaches
  * Template-driven infrastructure management

* Learned CloudFormation template structure:
  * YAML and JSON syntax
  * Template sections (Parameters, Resources, Outputs, Mappings, Conditions)
  * Resource declaration and properties
  * Intrinsic functions (Ref, GetAtt, Sub, Join, Select)

* Successfully created CloudFormation templates:
  * Wrote templates for VPC, subnets, and security groups
  * Created templates for EC2 instances with user data
  * Defined S3 buckets, IAM roles, and policies
  * Used parameters for reusable templates

* Understood stack operations:
  * Creating stacks from templates
  * Updating stacks with change sets
  * Rolling back failed updates
  * Deleting stacks and resource cleanup

* Learned change management:
  * Change sets for previewing updates
  * Stack policies for protecting resources
  * Drift detection for configuration compliance
  * Update behaviors (No Interrupt, Some Interrupt, Replacement)

* Mastered CloudFormation features:
  * Conditions for conditional resource creation
  * Mappings for environment-specific values
  * Outputs for exporting values
  * DependsOn for explicit resource dependencies

* Successfully implemented advanced patterns:
  * Nested stacks for modular templates
  * Cross-stack references with exports/imports
  * Custom resources with Lambda
  * Stack termination protection

* Gained practical experience with:
  * Version controlling CloudFormation templates
  * Automating infrastructure deployment
  * Managing multiple environments (dev, staging, prod)
  * Troubleshooting stack creation failures

* Understood CloudFormation best practices:
  * Organizing templates for reusability
  * Parameter validation and constraints
  * Using AWS Systems Manager Parameter Store
  * Cost estimation before deployment

* Built foundational knowledge for advanced IaC concepts, CI/CD integration, and multi-account/multi-region deployments with StackSets.