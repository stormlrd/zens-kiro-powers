# HIPAA Compliance on AWS

## Key Requirements

### Data Encryption
- **At Rest**: Use KMS encryption for all PHI
- **In Transit**: TLS 1.2+ for all connections
- **Backups**: Encrypt all backups and snapshots

### Access Controls
- **IAM**: Implement least privilege access
- **MFA**: Require MFA for all users
- **Audit**: Enable CloudTrail for all API calls
- **Monitoring**: Use CloudWatch for access monitoring

### Data Retention
- **Minimum**: 6 years for HIPAA records
- **Lifecycle**: Implement S3 lifecycle policies
- **Deletion**: Secure deletion procedures
- **Archival**: Use Glacier for long-term storage

## AWS Services for HIPAA

### HIPAA-Eligible Services
- HealthLake (FHIR data store)
- HealthOmics (genomics)
- S3 (encrypted storage)
- RDS (encrypted databases)
- DynamoDB (encrypted tables)
- Lambda (with VPC)
- ECS/EKS (with encryption)

### BAA Required
- Sign AWS Business Associate Addendum
- Enable HIPAA-eligible services only
- Document compliance measures
- Regular compliance audits

## HealthLake Best Practices

### FHIR Resources
- Use standard FHIR R4 resources
- Implement proper consent management
- Track data provenance
- Version all resources

### Data Import
- Validate FHIR bundles before import
- Use batch operations for efficiency
- Monitor import jobs
- Handle errors appropriately

### Querying
- Use FHIR search parameters
- Implement pagination
- Cache common queries
- Monitor query performance

## HealthOmics Best Practices

### Genomics Workflows
- Use reference genomes from AWS
- Implement quality control checks
- Monitor workflow execution
- Store results securely

### Data Management
- Use sequence stores for raw data
- Implement variant stores for analysis
- Tag all resources appropriately
- Monitor storage costs

## Security Checklist

- [ ] Sign AWS BAA
- [ ] Enable encryption at rest (KMS)
- [ ] Enable encryption in transit (TLS)
- [ ] Configure VPC endpoints
- [ ] Enable CloudTrail logging
- [ ] Implement IAM least privilege
- [ ] Enable MFA for all users
- [ ] Configure CloudWatch alarms
- [ ] Implement backup procedures
- [ ] Document compliance measures
- [ ] Regular security audits
- [ ] Incident response plan
