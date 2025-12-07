# Infrastructure as Code Best Practices

## General Principles

### Version Control
- Store all IaC in Git
- Use meaningful commit messages
- Tag releases
- Use branches for environments

### Modularity
- Create reusable modules
- Follow DRY principle
- Separate concerns
- Use composition over inheritance

### Security
- Scan templates for vulnerabilities
- Use least privilege IAM
- Encrypt sensitive data
- Enable CloudTrail logging

## CDK Best Practices

### Project Structure
```
project/
├── bin/           # App entry points
├── lib/           # Stack definitions
├── test/          # Unit tests
└── cdk.json       # CDK configuration
```

### Constructs
- Use L2 constructs by default
- Create custom L3 constructs for patterns
- Avoid L1 unless necessary
- Share constructs across projects

### Testing
- Write unit tests for stacks
- Use snapshot testing
- Test IAM policies
- Validate synthesized templates

## CloudFormation Best Practices

### Template Organization
- Use nested stacks for large deployments
- Parameterize for reusability
- Use mappings for environment-specific values
- Leverage conditions for optional resources

### Change Management
- Use change sets before updates
- Enable termination protection
- Implement rollback triggers
- Monitor stack events

## Terraform Best Practices

### State Management
- Use remote state (S3 + DynamoDB)
- Enable state locking
- Never commit state files
- Use workspaces for environments

### Module Design
- Keep modules focused
- Version modules
- Document inputs/outputs
- Publish to registry

## Deployment Strategies

### Blue/Green
```
Deploy new version → Test → Switch traffic → Retire old
```

### Canary
```
Deploy to subset → Monitor → Gradually increase → Full rollout
```

### Rolling
```
Update instances in batches → Validate → Continue
```

## CI/CD Integration

### Pipeline Stages
1. Validate syntax
2. Run security scans
3. Execute tests
4. Deploy to dev
5. Integration tests
6. Deploy to staging
7. Approval gate
8. Deploy to production

### Tools
- AWS CodePipeline
- GitHub Actions
- GitLab CI
- Jenkins
