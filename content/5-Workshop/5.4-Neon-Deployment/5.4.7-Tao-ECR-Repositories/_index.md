---
title : "Create ECR Repository"
date : 2024-01-01
weight : 7
chapter : false
pre : " <b> 5.4.7. </b> "
---

Amazon Elastic Container Registry (ECR) is a managed Docker container registry. The project requires a repository to store the Backend Django image.

---

### 5.4.7.1. Repository Provisioning Methods

#### Method 1: Execution via PowerShell Script (Recommended)
Run the automated script included in the project directory, which enforces idempotency and security standards:

```powershell
cd aws_04_deploy
.\01_create_ecr_repos.ps1
```

![Executing ECR Repository creation script](/images/5-Workshop/5.3-Neon-Infracstructure/image084.png)

Expected output displaying URI for the repository:

![ECR Repository creation result](/images/5-Workshop/5.3-Neon-Infracstructure/image085.png)

#### Method 2: Execution via AWS CLI or Management Console
Execute the following CLI command (requires configured AWS credentials):

```bash
# Provision Backend Repository
aws ecr create-repository \
  --repository-name neonfoodmap-backend \
  --region ap-southeast-1 \
  --image-scanning-configuration scanOnPush=true \
  --encryption-configuration encryptionType=AES256 \
  --tags Key=Project,Value=NeonFoodmap
```

![Manual ECR Repository creation via AWS Console](/images/5-Workshop/5.3-Neon-Infracstructure/image086.png)

---

### 5.4.7.2. ECR Security Compliance Standards

The container repository is configured with enterprise security controls:

| Feature | Configuration | Security Benefit |
| :--- | :--- | :--- |
| **Scan On Push** | `scanOnPush = true` | Automatically scans container images for CVE vulnerabilities upon push |
| **Encryption** | `encryptionType = AES256` | Enforces server-side data encryption at rest using AES-256 |
| **Resource Tags** | `Project=NeonFoodmap` | Establishes resource identification tags for cost tracking |

---

### 5.4.7.3. Verification

Execute the CLI command below to verify repository creation:

```bash
aws ecr describe-repositories \
  --repository-names neonfoodmap-backend \
  --region ap-southeast-1
```

The output will display repository details including the `repositoryUri` - the address used to push/pull Docker images.