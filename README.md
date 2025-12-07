# Zen's Kiro Powers

A comprehensive collection of Kiro Powers for AWS development, organized by service category. Each power provides MCP server configurations, documentation, and steering files for specific AWS service domains.

## Available Powers

### 🤖 AI & Machine Learning
**Path:** `ai-machine-learning/`
Amazon Bedrock, Kendra, Q Business, Knowledge Bases, and Nova Canvas for building intelligent applications.

**Servers:** bedrock-agentcore, kendra-index, qbusiness-anonymous, qindex, bedrock-custom-model-import, bedrock-data-automation, bedrock-kb-retrieval, nova-canvas

### 📊 Data & Analytics
**Path:** `data-analytics/`
DynamoDB, RDS, Aurora DSQL, Neptune, Keyspaces, DocumentDB, ElastiCache, Redshift, and S3 Tables for data management.

**Servers:** dynamodb, aurora-dsql, mysql, postgres, neptune, keyspaces, documentdb, elasticache, memcached, valkey, redshift, s3-tables

### 📡 Integration & Messaging
**Path:** `integration-messaging/`
SNS, SQS, AppSync, Amazon MQ, MSK, and Step Functions for event-driven architectures.

**Servers:** sns-sqs, appsync, amazon-mq, msk, stepfunctions

### ☁️ Getting Started with AWS
**Path:** `getting-started-aws/`
Essential AWS services for beginners - AWS API access and AWS Knowledge Base.

**Servers:** aws-api, aws-knowledge

### 💰 Cost & Operations
**Path:** `cost-operations/`
AWS Pricing, Cost Explorer, CloudWatch, CloudTrail, Billing, and Prometheus for cost optimization and observability.

**Servers:** aws-pricing, cost-explorer, billing-cost-management, cloudwatch, cloudwatch-appsignals, cloudtrail, prometheus

### 🏗️ Infrastructure & Deployment
**Path:** `infrastructure-deployment/`
CDK, CloudFormation, Terraform, Lambda, ECS, EKS, Serverless, and Finch for building and deploying infrastructure.

**Servers:** cdk, cloudformation, terraform, lambda, serverless, ecs, eks, finch, ccapi, support

### 🛠️ Developer Tools & Support
**Path:** `developer-tools-support/`
Code documentation, frontend development, Git research, IAM management, OpenAPI, synthetic data, and security best practices.

**Servers:** code-doc-gen, frontend, git-repo-research, iam, openapi, syntheticdata, well-architected-security

### 🌐 Specialized Services
**Path:** `specialized-services/`
Data processing, AWS diagrams, IoT SiteWise, Location Services, Core utilities, and Timestream for InfluxDB.

**Servers:** data-processing, aws-diagram, iot-sitewise, location, core, timestream-influxdb

### 🏥 Healthcare & Lifesciences
**Path:** `healthcare-lifesciences/`
AWS HealthOmics for genomics and HealthLake for FHIR-based healthcare data management.

**Servers:** healthomics, healthlake

### 📚 Documentation
**Path:** `documentation/`
Comprehensive AWS service documentation, API references, and best practices guides.

**Servers:** aws-documentation

### 📦 Uncategorized
**Path:** `uncategorized/`
Additional AWS services - IAC management, networking, CloudWatch Application Signals, document loading, and SageMaker AI.

**Servers:** aws-iac, aws-network, cloudwatch-applicationsignals, document-loader, sagemaker-ai

### 🚀 Amplify (In Progress)
**Path:** `amplify/`
AWS Amplify for full-stack application development.

## Power Structure

Each power follows this structure:

```
power-name/
├── POWER.md              # Main documentation with frontmatter
├── mcp.json              # MCP server configurations
└── steering/             # Steering files for guidance
    ├── guide-1.md
    └── guide-2.md
```

### POWER.md Format

Each POWER.md includes:
- **Frontmatter**: name, displayName, description, keywords, author
- **Overview**: Purpose and key capabilities
- **Available MCP Servers**: List of servers with descriptions
- **Best Practices**: Do's and Don'ts
- **Configuration**: Setup instructions
- **Tips**: Helpful guidance

### mcp.json Format

Standard MCP server configuration with:
- Server definitions
- Command and args
- Environment variables (using ${VAR} placeholders)
- Disabled flags for optional servers
- Auto-approve settings

### Steering Files

Markdown files providing:
- Best practices
- Code examples
- Architecture patterns
- Security guidelines
- Troubleshooting guides

## Environment Variables

Most powers use these common environment variables:

- `AWS_PROFILE` - AWS CLI profile name
- `AWS_REGION` - AWS region (e.g., us-east-1)
- `FASTMCP_LOG_LEVEL` - Logging level (ERROR, INFO, DEBUG)

Additional service-specific variables are documented in each power's POWER.md.

## Installation

1. Choose a power directory
2. Copy the power to your Kiro powers location
3. Configure environment variables in mcp.json
4. Enable/disable specific servers as needed
5. Activate the power in Kiro

## Usage

Each power can be activated in Kiro to access its MCP servers and steering guidance. Refer to individual POWER.md files for specific usage instructions and examples.

## Contributing

When adding new powers:
1. Follow the established structure
2. Include comprehensive POWER.md documentation
3. Provide mcp.json with all servers
4. Add relevant steering files
5. Use consistent formatting and style

## License

Apache-2.0

## Author

Zen / Stormlrd / Paul Dunlop

---
