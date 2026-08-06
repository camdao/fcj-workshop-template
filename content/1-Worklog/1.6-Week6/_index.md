---
title: "Week 6 Worklog"
date: 2024-01-01
weight: 6
chapter: false
pre: " <b> 1.6. </b> "
---

### Week 6 Objectives:

* Master Elastic Load Balancing (ELB) concepts and types.
* Understand Auto Scaling for dynamic resource management.
* Learn high availability and fault tolerance patterns.
* Practice building scalable and resilient architectures.

### Tasks to be carried out this week:
| Day | Task                                                                                                                                                                                                   | Start Date | Completion Date | Reference Material                        |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ---------- | --------------- | ----------------------------------------- |
| 2   | - Learn ELB Fundamentals: <br>&emsp; + Load balancing concepts <br>&emsp; + Application Load Balancer (ALB) <br>&emsp; + Network Load Balancer (NLB) <br>&emsp; + Gateway Load Balancer (GWLB)       | 07/16/2026 | 07/16/2026      | <https://cloudjourney.awsstudygroup.com/> |
| 3   | - Learn ELB Features: <br>&emsp; + Target groups <br>&emsp; + Health checks <br>&emsp; + Listener rules and routing <br>&emsp; + SSL/TLS termination                                                 | 07/17/2026 | 07/17/2026      | <https://cloudjourney.awsstudygroup.com/> |
| 4   | - **Practice:** <br>&emsp; + Create ALB and NLB <br>&emsp; + Configure target groups <br>&emsp; + Set up health checks <br>&emsp; + Configure routing rules                                           | 07/18/2026 | 07/18/2026      | <https://cloudjourney.awsstudygroup.com/> |
| 5   | - Learn Auto Scaling: <br>&emsp; + Auto Scaling Groups (ASG) <br>&emsp; + Launch templates <br>&emsp; + Scaling policies (target tracking, step, scheduled) <br>&emsp; + Lifecycle hooks             | 07/19/2026 | 07/19/2026      | <https://cloudjourney.awsstudygroup.com/> |
| 6   | - **Practice:** <br>&emsp; + Create Auto Scaling Groups <br>&emsp; + Configure scaling policies <br>&emsp; + Integrate with Load Balancers <br>&emsp; + Test scaling behavior                        | 07/20/2026 | 07/20/2026      | <https://cloudjourney.awsstudygroup.com/> |


### Week 6 Achievements:

* Mastered Elastic Load Balancing fundamentals:
  * Understanding load balancing concepts and benefits
  * Application Load Balancer (Layer 7) for HTTP/HTTPS traffic
  * Network Load Balancer (Layer 4) for TCP/UDP traffic
  * Gateway Load Balancer for third-party virtual appliances
  * Choosing the right load balancer type

* Learned ELB components and features:
  * Target groups for routing traffic to instances
  * Health checks for monitoring target health
  * Listener rules for routing based on conditions
  * SSL/TLS termination and certificate management
  * Cross-Zone load balancing

* Successfully configured load balancers:
  * Created Application Load Balancers with multiple target groups
  * Set up Network Load Balancers for high-performance workloads
  * Configured health checks with appropriate thresholds
  * Implemented path-based and host-based routing
  * Set up SSL/TLS certificates with ACM

* Understood load balancer security:
  * Security groups for load balancers
  * AWS WAF integration for application protection
  * Access logs for auditing and troubleshooting
  * Connection draining and deregistration delay

* Mastered Auto Scaling fundamentals:
  * Auto Scaling Groups (ASG) concepts
  * Launch templates and launch configurations
  * Desired, minimum, and maximum capacity
  * Instance distribution across Availability Zones

* Learned Auto Scaling policies:
  * Target tracking scaling (maintain metric at target)
  * Step scaling (scale based on CloudWatch alarms)
  * Scheduled scaling (predictable load patterns)
  * Predictive scaling (ML-based forecasting)

* Successfully implemented Auto Scaling:
  * Created Auto Scaling Groups with launch templates
  * Configured target tracking policies for CPU utilization
  * Set up step scaling policies with CloudWatch alarms
  * Integrated ASG with load balancers
  * Implemented lifecycle hooks for custom actions

* Gained practical experience with:
  * High availability architecture design
  * Fault tolerance and resilience patterns
  * Cost optimization through dynamic scaling
  * Load testing and performance validation

* Understood scaling best practices:
  * Warm-up and cooldown periods
  * Health check grace period
  * Instance protection during maintenance
  * Scaling metrics selection

* Built foundational knowledge for building highly available, fault-tolerant, and cost-effective applications on AWS.