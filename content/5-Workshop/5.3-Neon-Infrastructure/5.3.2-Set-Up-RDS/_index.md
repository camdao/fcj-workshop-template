---
title : "Initialize and Configure RDS"
date : 2024-01-01
weight : 2
chapter : false
pre : " <b> 5.3.2. </b> "
---

### Deployment Architecture Overview

The infrastructure is built using a multi-tier model with the following layers:

- Public subnet: receives traffic from the Internet
- Private subnet: runs applications and internal services
- Database subnet: hosts the system's RDS instance
- S3 bucket: stores frontend assets, media, audio, and logs
- IAM Role and OIDC: grants secure deploy permissions to GitHub Actions

### 5.3.6. Create DB Subnet Group for Amazon RDS

1. Open the Amazon RDS Console.
2. Select **Subnet groups**.
3. Click **Create DB Subnet Group**.
4. Select the project VPC.
5. Select private subnets across two AZs.
6. Click **Create**.

![Figure 31.](/5-Workshop/images/5.3-Neon-Infracstructure/image031.png)
![Figure 32.](/5-Workshop/images/5.3-Neon-Infracstructure/image032.png)

### 5.3.7. Create DB Parameter Group for MySQL

1. Go to RDS Console → **Parameter groups**.
2. Click **Create parameter group**.
3. Configure:
   - Group name: `neonfoodmap-mysql80-params`
   - Description: `Parameter group optimized for utf8mb4 for NeonFoodmap`
   - Engine type: `MySQL`
   - Parameter group family: `mysql8.0`
   - Type: `DB Parameter Group`
4. Click **Create**.
5. Select the newly created parameter group → **Edit**.
6. Update the following:
   - `character_set_server = utf8mb4`
   - `collation_server = utf8mb4_unicode_ci`
7. Click **Save changes**.

![Figure 33.](/5-Workshop/images/5.3-Neon-Infracstructure/image033.png)
![Figure 34.](/5-Workshop/images/5.3-Neon-Infracstructure/image034.png)
![Figure 35.](/5-Workshop/images/5.3-Neon-Infracstructure/image035.png)
![Figure 36.](/5-Workshop/images/5.3-Neon-Infracstructure/image036.png)
![Figure 37.](/5-Workshop/images/5.3-Neon-Infracstructure/image037.png)
![Figure 38.](/5-Workshop/images/5.3-Neon-Infracstructure/image038.png)

### 5.3.8. Create Security Group for RDS

1. Open EC2 Console → **Security Groups**.
2. Click **Create security group**.
3. Set up:
   - Name: `neonfoodmap-rds-sg`
   - Description: `Allow inbound traffic from ECS tasks only`
   - VPC: select the project VPC
4. Under **Inbound rules**, add a rule:
   - Type: `MySQL/Aurora`
   - Port: `3306`
   - Source: the security group of the ECS task or backend service
5. Keep the default outbound rule unchanged.
6. Click **Create security group**.

![Figure 39.](/5-Workshop/images/5.3-Neon-Infracstructure/image039.png)
![Figure 40.](/5-Workshop/images/5.3-Neon-Infracstructure/image040.png)

### 5.3.9. Create Amazon RDS MySQL Instance

1. Go to Amazon RDS Console → **Databases** → **Create database**.
2. Select **Standard Create**.
3. Choose engine `MySQL` and the appropriate version.
4. Under **Settings**:
   - DB instance identifier: `neonfoodmap-mysql-db`
   - Master username: `admin`
   - Master password: set a strong password and store it in a safe place
   - Instance type: `db.t3.micro`
5. Under **Storage**:
   - Storage type: `gp3`
   - Allocated storage: `20 GiB`
   - Enable storage autoscaling up to `100 GB`
6. Under **Connectivity**:
   - Compute resource: `Don't connect to an EC2 compute resource`
   - VPC: select the project VPC
   - DB subnet group: select the group you created
   - Public access: `No`
   - VPC security group: select `neonfoodmap-rds-sg`
   - Database port: `3306`
7. Under **Monitoring**:
   - Enable `Error log` and `Slow query log`
8. Under **Additional configuration**:
   - Initial database name: `buocchancoi_db`
   - DB parameter group: `neonfoodmap-mysql80-params`
   - Enable automated backups with a retention period of `7 days`
   - Enable encryption
9. Click **Create database**.

![Figure 41.](/5-Workshop/images/5.3-Neon-Infracstructure/image041.png)
![Figure 42.](/5-Workshop/images/5.3-Neon-Infracstructure/image042.png)
![Figure 43.](/5-Workshop/images/5.3-Neon-Infracstructure/image043.png)
![Figure 44.](/5-Workshop/images/5.3-Neon-Infracstructure/image044.png)
![Figure 45.](/5-Workshop/images/5.3-Neon-Infracstructure/image045.png)
![Figure 46.](/5-Workshop/images/5.3-Neon-Infracstructure/image046.png)
![Figure 47.](/5-Workshop/images/5.3-Neon-Infracstructure/image047.png)
![Figure 48.](/5-Workshop/images/5.3-Neon-Infracstructure/image048.png)
![Figure 49.](/5-Workshop/images/5.3-Neon-Infracstructure/image049.png)
![Figure 50.](/5-Workshop/images/5.3-Neon-Infracstructure/image050.png)
![Figure 51.](/5-Workshop/images/5.3-Neon-Infracstructure/image051.png)
![Figure 52.](/5-Workshop/images/5.3-Neon-Infracstructure/image052.png)
![Figure 53.](/5-Workshop/images/5.3-Neon-Infracstructure/image053.png)
![Figure 54.](/5-Workshop/images/5.3-Neon-Infracstructure/image054.png)
![Figure 55.](/5-Workshop/images/5.3-Neon-Infracstructure/image055.png)
![Figure 56.](/5-Workshop/images/5.3-Neon-Infracstructure/image056.png)
![Figure 57.](/5-Workshop/images/5.3-Neon-Infracstructure/image057.png)
![Figure 58.](/5-Workshop/images/5.3-Neon-Infracstructure/image058.png)
![Figure 59.](/5-Workshop/images/5.3-Neon-Infracstructure/image059.png)
![Figure 60.](/5-Workshop/images/5.3-Neon-Infracstructure/image060.png)
![Figure 61.](/5-Workshop/images/5.3-Neon-Infracstructure/image061.png)
![Figure 62.](/5-Workshop/images/5.3-Neon-Infracstructure/image062.png)
![Figure 63.](/5-Workshop/images/5.3-Neon-Infracstructure/image063.png)
![Figure 64.](/5-Workshop/images/5.3-Neon-Infracstructure/image064.png)
![Figure 65.](/5-Workshop/images/5.3-Neon-Infracstructure/image065.png)
![Figure 66.](/5-Workshop/images/5.3-Neon-Infracstructure/image066.png)
![Figure 67.](/5-Workshop/images/5.3-Neon-Infracstructure/image067.png)
![Figure 68.](/5-Workshop/images/5.3-Neon-Infracstructure/image068.png)
![Figure 69.](/5-Workshop/images/5.3-Neon-Infracstructure/image069.png)
![Figure 70.](/5-Workshop/images/5.3-Neon-Infracstructure/image070.png)
![Figure 71.](/5-Workshop/images/5.3-Neon-Infracstructure/image071.png)
![Figure 72.](/5-Workshop/images/5.3-Neon-Infracstructure/image072.png)
![Figure 73.](/5-Workshop/images/5.3-Neon-Infracstructure/image073.png)
![Figure 74.](/5-Workshop/images/5.3-Neon-Infracstructure/image074.png)
![Figure 75.](/5-Workshop/images/5.3-Neon-Infracstructure/image075.png)
![Figure 76.](/5-Workshop/images/5.3-Neon-Infracstructure/image076.png)
![Figure 77.](/5-Workshop/images/5.3-Neon-Infracstructure/image077.png)
![Figure 78.](/5-Workshop/images/5.3-Neon-Infracstructure/image078.png)
![Figure 79.](/5-Workshop/images/5.3-Neon-Infracstructure/image079.png)
![Figure 80.](/5-Workshop/images/5.3-Neon-Infracstructure/image080.png)
![Figure 81.](/5-Workshop/images/5.3-Neon-Infracstructure/image081.png)
![Figure 82.](/5-Workshop/images/5.3-Neon-Infracstructure/image082.png)
![Figure 83.](/5-Workshop/images/5.3-Neon-Infracstructure/image083.png)
![Figure 84.](/5-Workshop/images/5.3-Neon-Infracstructure/image084.png)
![Figure 85.](/5-Workshop/images/5.3-Neon-Infracstructure/image085.png)
![Figure 86.](/5-Workshop/images/5.3-Neon-Infracstructure/image086.png)
![Figure 87.](/5-Workshop/images/5.3-Neon-Infracstructure/image087.png)
![Figure 88.](/5-Workshop/images/5.3-Neon-Infracstructure/image088.png)
![Figure 89.](/5-Workshop/images/5.3-Neon-Infracstructure/image089.png)
![Figure 90.](/5-Workshop/images/5.3-Neon-Infracstructure/image090.png)
![Figure 91.](/5-Workshop/images/5.3-Neon-Infracstructure/image091.png)
![Figure 92.](/5-Workshop/images/5.3-Neon-Infracstructure/image092.png)
![Figure 93.](/5-Workshop/images/5.3-Neon-Infracstructure/image093.png)
![Figure 94.](/5-Workshop/images/5.3-Neon-Infracstructure/image094.png)
![Figure 95.](/5-Workshop/images/5.3-Neon-Infracstructure/image095.png)
![Figure 96.](/5-Workshop/images/5.3-Neon-Infracstructure/image096.png)
![Figure 97.](/5-Workshop/images/5.3-Neon-Infracstructure/image097.png)
![Figure 98.](/5-Workshop/images/5.3-Neon-Infracstructure/image098.png)
![Figure 99.](/5-Workshop/images/5.3-Neon-Infracstructure/image099.png)
![Figure 100.](/5-Workshop/images/5.3-Neon-Infracstructure/image100.png)
![Figure 101.](/5-Workshop/images/5.3-Neon-Infracstructure/image101.png)
![Figure 102.](/5-Workshop/images/5.3-Neon-Infracstructure/image102.png)
![Figure 103.](/5-Workshop/images/5.3-Neon-Infracstructure/image103.png)
![Figure 104.](/5-Workshop/images/5.3-Neon-Infracstructure/image104.png)
![Figure 105.](/5-Workshop/images/5.3-Neon-Infracstructure/image105.png)
![Figure 106.](/5-Workshop/images/5.3-Neon-Infracstructure/image106.png)
![Figure 107.](/5-Workshop/images/5.3-Neon-Infracstructure/image107.png)
![Figure 108.](/5-Workshop/images/5.3-Neon-Infracstructure/image108.png)
![Figure 109.](/5-Workshop/images/5.3-Neon-Infracstructure/image109.png)
![Figure 110.](/5-Workshop/images/5.3-Neon-Infracstructure/image110.png)
![Figure 111.](/5-Workshop/images/5.3-Neon-Infracstructure/image111.png)
![Figure 112.](/5-Workshop/images/5.3-Neon-Infracstructure/image112.png)
![Figure 113.](/5-Workshop/images/5.3-Neon-Infracstructure/image113.png)
![Figure 114.](/5-Workshop/images/5.3-Neon-Infracstructure/image114.png)
![Figure 115.](/5-Workshop/images/5.3-Neon-Infracstructure/image115.png)
![Figure 116.](/5-Workshop/images/5.3-Neon-Infracstructure/image116.png)
![Figure 117.](/5-Workshop/images/5.3-Neon-Infracstructure/image117.png)
![Figure 118.](/5-Workshop/images/5.3-Neon-Infracstructure/image118.png)
![Figure 119.](/5-Workshop/images/5.3-Neon-Infracstructure/image119.png)
![Figure 120.](/5-Workshop/images/5.3-Neon-Infracstructure/image120.png)
![Figure 121.](/5-Workshop/images/5.3-Neon-Infracstructure/image121.png)
![Figure 122.](/5-Workshop/images/5.3-Neon-Infracstructure/image122.png)
![Figure 123.](/5-Workshop/images/5.3-Neon-Infracstructure/image123.png)
![Figure 124.](/5-Workshop/images/5.3-Neon-Infracstructure/image124.png)
![Figure 125.](/5-Workshop/images/5.3-Neon-Infracstructure/image125.png)
![Figure 126.](/5-Workshop/images/5.3-Neon-Infracstructure/image126.png)
![Figure 127.](/5-Workshop/images/5.3-Neon-Infracstructure/image127.png)
![Figure 128.](/5-Workshop/images/5.3-Neon-Infracstructure/image128.png)
![Figure 129.](/5-Workshop/images/5.3-Neon-Infracstructure/image129.png)
![Figure 130.](/5-Workshop/images/5.3-Neon-Infracstructure/image130.png)
![Figure 131.](/5-Workshop/images/5.3-Neon-Infracstructure/image131.png)
![Figure 132.](/5-Workshop/images/5.3-Neon-Infracstructure/image132.png)
![Figure 133.](/5-Workshop/images/5.3-Neon-Infracstructure/image133.png)
![Figure 134.](/5-Workshop/images/5.3-Neon-Infracstructure/image134.png)
![Figure 135.](/5-Workshop/images/5.3-Neon-Infracstructure/image135.png)
![Figure 136.](/5-Workshop/images/5.3-Neon-Infracstructure/image136.png)
![Figure 137.](/5-Workshop/images/5.3-Neon-Infracstructure/image137.png)
![Figure 138.](/5-Workshop/images/5.3-Neon-Infracstructure/image138.png)
![Figure 139.](/5-Workshop/images/5.3-Neon-Infracstructure/image139.png)
![Figure 140.](/5-Workshop/images/5.3-Neon-Infracstructure/image140.png)
![Figure 141.](/5-Workshop/images/5.3-Neon-Infracstructure/image141.png)
![Figure 142.](/5-Workshop/images/5.3-Neon-Infracstructure/image142.png)
![Figure 143.](/5-Workshop/images/5.3-Neon-Infracstructure/image143.png)
![Figure 144.](/5-Workshop/images/5.3-Neon-Infracstructure/image144.png)
![Figure 145.](/5-Workshop/images/5.3-Neon-Infracstructure/image145.png)
![Figure 146.](/5-Workshop/images/5.3-Neon-Infracstructure/image146.png)
![Figure 147.](/5-Workshop/images/5.3-Neon-Infracstructure/image147.png)
![Figure 148.](/5-Workshop/images/5.3-Neon-Infracstructure/image148.png)
![Figure 149.](/5-Workshop/images/5.3-Neon-Infracstructure/image149.png)
![Figure 150.](/5-Workshop/images/5.3-Neon-Infracstructure/image150.png)
![Figure 151.](/5-Workshop/images/5.3-Neon-Infracstructure/image151.png)
![Figure 152.](/5-Workshop/images/5.3-Neon-Infracstructure/image152.png)
![Figure 153.](/5-Workshop/images/5.3-Neon-Infracstructure/image153.png)
![Figure 154.](/5-Workshop/images/5.3-Neon-Infracstructure/image154.png)
![Figure 155.](/5-Workshop/images/5.3-Neon-Infracstructure/image155.png)

### 5.3.10. Retrieve Endpoint and Save to `.env` File

1. Open the DB instance you just created.
2. Select the **Connectivity & security** tab.
3. Copy the **Endpoint** value.
4. Paste it into the project's `.env` file so the backend can connect to the correct database address.

![Figure 10. Retrieve database Endpoint](/5-Workshop/images/5.3-neon-infrastructure/placeholder-rds-endpoint.png)
