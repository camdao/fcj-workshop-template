---
title : "Design and Build NeonFoodMap Infrastructure on AWS"
date : 2024-01-01
weight : 3
chapter : false
pre : " <b> 5.3. </b> "
---

### Objectives

In this section, you will deploy the NeonFoodMap infrastructure on AWS following a clear, sequential, end-to-end workflow. The content is organized step by step — from network initialization and data setup to access configuration and final verification.

### Deployment Architecture Overview

The infrastructure is built using a multi-tier model with the following layers:

- Public subnet: receives traffic from the Internet
- Private subnet: runs applications and internal services
- Database subnet: hosts the system's RDS instance
- S3 bucket: stores frontend assets, media, audio, and logs
- IAM Role and OIDC: grants secure deploy permissions to GitHub Actions

### Deployment Summary

After completing all the steps above, the NeonFoodMap system has a complete foundational infrastructure for secure operation and continuous deployment:

- VPC and subnets follow the correct multi-tier network model
- NAT Gateway allows private subnets to access the Internet in a controlled manner
- RDS MySQL is deployed in a private subnet, accessible only through the allowed security group
- S3 is configured to store system resources
- IAM Role and GitHub OIDC enable GitHub Actions to deploy to AWS following the principle of least privilege
Successfully create bucket

![Success](/images/5-Workshop/5.5-Policy/create-bucket-success.png)

3. Navigate to: Services > VPC > Endpoints, then select the Gateway VPC endpoint you created earlier. Click the Policy tab. Click Edit policy.

![policy](/images/5-Workshop/5.5-Policy/policy1.png)

The default policy allows access to all S3 Buckets through the VPC endpoint.

4. In Edit Policy console, copy & Paste the following policy, then replace yourbucketname-2 with your 2nd bucket name. This policy will allow access through the VPC endpoint to your new bucket, but not any other bucket in Amazon S3. Click Save to apply the policy.

```
{
  "Id": "Policy1631305502445",
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "Stmt1631305501021",
      "Action": "s3:*",
      "Effect": "Allow",
      "Resource": [
      				"arn:aws:s3:::yourbucketname-2",
       				"arn:aws:s3:::yourbucketname-2/*"
       ],
      "Principal": "*"
    }
  ]
}
```

![custom policy](/images/5-Workshop/5.5-Policy/policy2.png)

Successfully customize policy

![success](/static/images/5-Workshop/5.5-Policy/success.png)

5. From your session on the Test-Gateway-Endpoint instance, test access to the S3 bucket you created in Part 1: Access S3 from VPC
```
aws s3 ls s3://<yourbucketname>
```

This command will return an error because access to this bucket is not permitted by your new VPC endpoint policy:

![error](/static/images/5-Workshop/5.5-Policy/error.png)

6. Return to your home directory on your EC2 instance ` cd~ `

+ Create a file ```fallocate -l 1G test-bucket2.xyz ```
+ Copy file to 2nd bucket ```aws s3 cp test-bucket2.xyz s3://<your-2nd-bucket-name>```

![success](/static/images/5-Workshop/5.5-Policy/test2.png)

This operation succeeds because it is permitted by the VPC endpoint policy.

![success](/static/images/5-Workshop/5.5-Policy/test2-success.png)

+ Then we test access to the first bucket by copy the file to 1st bucket `aws s3 cp test-bucket2.xyz s3://<your-1st-bucket-name>`

![fail](/static/images/5-Workshop/5.5-Policy/test2-fail.png)

This command will return an error because access to this bucket is not permitted by your new VPC endpoint policy.

#### Part 3 Summary:

In this section, you created a VPC endpoint policy for Amazon S3, and used the AWS CLI to test the policy. AWS CLI actions targeted to your original S3 bucket failed because you applied a policy that only allowed access to the second bucket you created. AWS CLI actions targeted for your second bucket succeeded because the policy allowed them. These policies can be useful in situations where you need to control access to resources through VPC endpoints.


