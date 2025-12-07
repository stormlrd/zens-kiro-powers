# AWS Fundamentals

## Core Concepts

### Regions and Availability Zones
- **Region**: Geographic area with multiple AZs
- **Availability Zone**: Isolated data center
- **Best Practice**: Deploy across multiple AZs for high availability

### IAM (Identity and Access Management)
- **Users**: Individual identities
- **Groups**: Collections of users
- **Roles**: Temporary credentials for services
- **Policies**: JSON documents defining permissions

### Security Best Practices
1. Enable MFA on root account
2. Use IAM roles for applications
3. Follow least privilege principle
4. Rotate credentials regularly
5. Enable CloudTrail logging

### Cost Management
- Set up billing alerts
- Use Cost Explorer
- Tag resources for cost allocation
- Use AWS Budgets
- Review Trusted Advisor recommendations

## Common Services

### Compute
- **EC2**: Virtual servers
- **Lambda**: Serverless functions
- **ECS/EKS**: Container orchestration

### Storage
- **S3**: Object storage
- **EBS**: Block storage for EC2
- **EFS**: File storage

### Database
- **RDS**: Managed relational databases
- **DynamoDB**: NoSQL database
- **Aurora**: High-performance relational

### Networking
- **VPC**: Virtual private cloud
- **Route 53**: DNS service
- **CloudFront**: CDN

## Getting Started Checklist

- [ ] Create AWS account
- [ ] Enable MFA on root account
- [ ] Create IAM admin user
- [ ] Set up billing alerts
- [ ] Configure AWS CLI
- [ ] Create first VPC
- [ ] Launch first EC2 instance
- [ ] Create S3 bucket
- [ ] Set up CloudWatch monitoring
