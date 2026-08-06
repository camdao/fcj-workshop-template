---
title : "Initialize and Configure VPC"
date : 2024-01-01
weight : 1
chapter : false
pre : " <b> 5.3.1. </b> "
---

### 5.3.1.1 Create Amazon VPC

The first step is to create a VPC and subnets following the standard architecture.

1. Go to the AWS Management Console.
2. Open the VPC service.
3. Select Your VPCs → Create VPC.
4. Choose the **VPC and more** option.
5. Configure the following settings:
   - Name tag auto-generation: `NeonFood`
   - IPv4 CIDR block: `10.0.0.0/16`
   - Number of AZs: `2`
   - Number of Public Subnets: `2`
   - Number of Private Subnets: `4`
6. Click **Create VPC**.

Expected results:

- Public subnet 1: `10.0.0.0/20`
- Public subnet 2: `10.0.16.0/20`
- Private subnet 1: `10.0.128.0/20`
- Private subnet 2: `10.0.144.0/20`
- Private subnet 3: `10.0.160.0/20`
- Private subnet 4: `10.0.176.0/20`

![Figure 1.](/5-Workshop/images/5.3-Neon-Infracstructure/image001.png)
![Figure 2.](/5-Workshop/images/5.3-Neon-Infracstructure/image002.png)
![Figure 3.](/5-Workshop/images/5.3-Neon-Infracstructure/image003.png)
![Figure 4.](/5-Workshop/images/5.3-Neon-Infracstructure/image004.png)
![Figure 5.](/5-Workshop/images/5.3-Neon-Infracstructure/image005.png)
![Figure 6.](/5-Workshop/images/5.3-Neon-Infracstructure/image006.png)
![Figure 7.](/5-Workshop/images/5.3-Neon-Infracstructure/image007.png)
![Figure 8.](/5-Workshop/images/5.3-Neon-Infracstructure/image008.png)

### 5.3.1.2. Create Elastic IP for NAT Gateway

1. Open the VPC Console.
2. Select **Elastic IP addresses**.
3. Click **Allocate Elastic IP address**.
4. Add a tag `Name=EIP-NAT-AZ1a`.
5. Click **Allocate**.

![Figure 9.](/5-Workshop/images/5.3-Neon-Infracstructure/image009.png)
![Figure 10.](/5-Workshop/images/5.3-Neon-Infracstructure/image010.png)
![Figure 11.](/5-Workshop/images/5.3-Neon-Infracstructure/image011.png)
![Figure 12.](/5-Workshop/images/5.3-Neon-Infracstructure/image012.png)

### 5.3.1.3. Create NAT Gateway

1. Go to VPC Console → **NAT gateways**.
2. Click **Create NAT gateway**.
3. Configure:
   - Name: `NAT-Gateway-AZ1a`
   - Subnet: public subnet in AZ 1a
   - Connectivity type: `Public`
   - Elastic IP: select the EIP you created earlier
4. Click **Create NAT gateway**.
5. Wait until the status shows `Available`.

![Figure 13.](/5-Workshop/images/5.3-Neon-Infracstructure/image013.png)
![Figure 14.](/5-Workshop/images/5.3-Neon-Infracstructure/image014.png)
![Figure 15.](/5-Workshop/images/5.3-Neon-Infracstructure/image015.png)
![Figure 16.](/5-Workshop/images/5.3-Neon-Infracstructure/image016.png)

### 5.3.1.4. Configure Route Table for Private Subnet

1. Open **Route tables**.
2. Select the route table associated with the private subnet in AZ 1a.
3. Choose **Routes** → **Edit routes**.
4. Add a new route:
   - Destination: `0.0.0.0/0`
   - Target: the NAT Gateway you just created
5. Click **Save changes**.

![Figure 17.](/5-Workshop/images/5.3-Neon-Infracstructure/image017.png)
![Figure 18.](/5-Workshop/images/5.3-Neon-Infracstructure/image018.png)
![Figure 19.](/5-Workshop/images/5.3-Neon-Infracstructure/image019.png)
![Figure 20.](/5-Workshop/images/5.3-Neon-Infracstructure/image020.png)
![Figure 21.](/5-Workshop/images/5.3-Neon-Infracstructure/image021.png)
![Figure 22.](/5-Workshop/images/5.3-Neon-Infracstructure/image022.png)
![Figure 23.](/5-Workshop/images/5.3-Neon-Infracstructure/image023.png)
![Figure 24.](/5-Workshop/images/5.3-Neon-Infracstructure/image024.png)
![Figure 25.](/5-Workshop/images/5.3-Neon-Infracstructure/image025.png)
![Figure 26.](/5-Workshop/images/5.3-Neon-Infracstructure/image026.png)

### 5.3.1.5. Enable Auto-assign Public IPv4 for Public Subnets

1. Go to VPC Console → **Subnets**.
2. Select public subnet 1.
3. Choose **Actions** → **Edit subnet settings**.
4. Check **Enable auto-assign public IPv4 address**.
5. Save.
6. Repeat the same steps for public subnet 2.

![Figure 27.](/5-Workshop/images/5.3-Neon-Infracstructure/image027.png)
![Figure 28.](/5-Workshop/images/5.3-Neon-Infracstructure/image028.png)
![Figure 29.](/5-Workshop/images/5.3-Neon-Infracstructure/image029.png)
![Figure 30.](/5-Workshop/images/5.3-Neon-Infracstructure/image030.png)
