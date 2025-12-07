# IAM Security Best Practices

## Principle of Least Privilege

### Start Minimal
```json
{
  "Version": "2012-10-17",
  "Statement": [{
    "Effect": "Allow",
    "Action": ["service:SpecificAction"],
    "Resource": "arn:aws:service:region:account:resource/specific-id"
  }]
}
```

### Avoid Wildcards
❌ Bad:
```json
"Action": "*"
"Resource": "*"
```

✅ Good:
```json
"Action": ["s3:GetObject", "s3:PutObject"]
"Resource": "arn:aws:s3:::my-bucket/*"
```

## IAM Roles vs Users

### Use Roles For:
- EC2 instances
- Lambda functions
- ECS tasks
- Cross-account access
- Temporary access

### Use Users For:
- Individual developers
- CI/CD systems (with rotation)
- Long-term credentials (avoid if possible)

## Policy Structure

### Resource-Based Policies
- Attached to resources (S3, SQS, etc.)
- Define who can access the resource
- Support cross-account access

### Identity-Based Policies
- Attached to users, groups, roles
- Define what the identity can do
- Managed or inline

## Security Checklist

- [ ] Enable MFA for all users
- [ ] Rotate access keys regularly
- [ ] Use IAM roles instead of keys
- [ ] Review permissions quarterly
- [ ] Enable CloudTrail logging
- [ ] Use AWS Organizations SCPs
- [ ] Implement password policy
- [ ] Remove unused credentials
- [ ] Use IAM Access Analyzer
- [ ] Tag IAM resources

## Common Patterns

### Lambda Execution Role
```json
{
  "Version": "2012-10-17",
  "Statement": [{
    "Effect": "Allow",
    "Action": [
      "logs:CreateLogGroup",
      "logs:CreateLogStream",
      "logs:PutLogEvents"
    ],
    "Resource": "arn:aws:logs:*:*:*"
  }]
}
```

### S3 Read-Only Access
```json
{
  "Version": "2012-10-17",
  "Statement": [{
    "Effect": "Allow",
    "Action": ["s3:GetObject", "s3:ListBucket"],
    "Resource": [
      "arn:aws:s3:::my-bucket",
      "arn:aws:s3:::my-bucket/*"
    ]
  }]
}
```

### DynamoDB Table Access
```json
{
  "Version": "2012-10-17",
  "Statement": [{
    "Effect": "Allow",
    "Action": [
      "dynamodb:GetItem",
      "dynamodb:PutItem",
      "dynamodb:Query"
    ],
    "Resource": "arn:aws:dynamodb:region:account:table/MyTable"
  }]
}
```
