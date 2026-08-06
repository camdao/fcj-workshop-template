---
title: "Worklog Tuần 11"
date: 2024-01-01
weight: 11
chapter: false
pre: " <b> 1.11. </b> "
---

### Mục tiêu tuần 11:

* Nắm vững các dịch vụ bảo mật AWS và best practices.
* Hiểu về encryption, secrets management và compliance.
* Tìm hiểu các công cụ và frameworks về security của AWS.
* Thực hành triển khai giải pháp bảo mật toàn diện.

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc                                                                                                                                                                                   | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu                            |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------ | --------------- | ----------------------------------------- |
| 2   | - Tìm hiểu Security Fundamentals: <br>&emsp; + Shared responsibility model <br>&emsp; + AWS security services overview <br>&emsp; + Security best practices <br>&emsp; + Compliance frameworks | 20/08/2026   | 20/08/2026      | <https://cloudjourney.awsstudygroup.com/> |
| 3   | - Tìm hiểu AWS KMS & Secrets Manager: <br>&emsp; + Encryption at rest và in transit <br>&emsp; + KMS keys và policies <br>&emsp; + Secrets rotation <br>&emsp; + AWS Certificate Manager  | 21/08/2026   | 21/08/2026      | <https://cloudjourney.awsstudygroup.com/> |
| 4   | - **Thực hành:** <br>&emsp; + Tạo KMS keys <br>&emsp; + Encrypt data với KMS <br>&emsp; + Lưu secrets trong Secrets Manager <br>&emsp; + Triển khai secret rotation                       | 22/08/2026   | 22/08/2026      | <https://cloudjourney.awsstudygroup.com/> |
| 5   | - Tìm hiểu Security Tools: <br>&emsp; + AWS WAF cho application protection <br>&emsp; + AWS Shield cho DDoS protection <br>&emsp; + GuardDuty cho threat detection <br>&emsp; + Security Hub | 23/08/2026   | 23/08/2026      | <https://cloudjourney.awsstudygroup.com/> |
| 6   | - **Thực hành:** <br>&emsp; + Cấu hình AWS WAF rules <br>&emsp; + Bật GuardDuty <br>&emsp; + Review Security Hub findings <br>&emsp; + Triển khai security best practices                 | 24/08/2026   | 24/08/2026      | <https://cloudjourney.awsstudygroup.com/> |


### Kết quả đạt được tuần 11:

* Nắm vững kiến thức cơ bản về AWS security:
  * Hiểu shared responsibility model
  * Landscape của các dịch vụ security AWS
  * Nguyên tắc thiết kế security
  * Yêu cầu compliance và regulatory

* Tìm hiểu về encryption và key management:
  * AWS KMS cho encryption key management
  * Customer Master Keys (CMKs)
  * Key policies và grants
  * Envelope encryption

* Thành công triển khai encryption:
  * Tạo và quản lý KMS keys
  * Mã hóa data at rest (EBS, S3, RDS)
  * Cấu hình encryption in transit (TLS/SSL)
  * Tự động key rotation

* Nắm vững secrets management:
  * Các khái niệm AWS Secrets Manager
  * Lưu trữ database credentials
  * Quản lý API keys và tokens
  * Automatic secret rotation

* Tìm hiểu các dịch vụ security AWS:
  * AWS WAF cho web application firewall
  * AWS Shield cho DDoS protection
  * Amazon GuardDuty cho threat detection
  * AWS Security Hub cho centralized security

* Thành công cấu hình security tools:
  * Tạo WAF rules và web ACLs
  * Bật GuardDuty cho threat monitoring
  * Cấu hình Security Hub standards
  * Thiết lập automated remediation

* Hiểu các best practices về IAM security:
  * Nguyên tắc least privilege
  * MFA cho privileged accounts
  * IAM Access Analyzer
  * Service control policies (SCPs)

* Tìm hiểu về network security:
  * Best practices cho VPC security groups
  * Cấu hình Network ACLs
  * AWS Network Firewall
  * Phân tích VPC Flow Logs

* Có kinh nghiệm thực tế với:
  * Security incident response
  * Compliance auditing
  * Security automation
  * Vulnerability management

* Hiểu các compliance frameworks:
  * AWS Artifact cho compliance reports
  * Cân nhắc GDPR, HIPAA, PCI DSS
  * AWS Config cho compliance monitoring
  * AWS Audit Manager

* Xây dựng kiến thức nền tảng cho việc triển khai defense-in-depth security, đáp ứng yêu cầu compliance và duy trì môi trường AWS an toàn.