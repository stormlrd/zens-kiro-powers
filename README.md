# Zen's Kiro Powers

A comprehensive collection of Kiro Powers for AWS development, organized by service category. Each power provides MCP server configurations, documentation, and steering files for specific AWS service domains.

## Quick Start

1. **Browse Powers**: Check the [Available Powers](#available-powers) section below
2. **Choose a Power**: Select the power that matches your needs
3. **Install**: Use Kiro's "Add Custom Power" feature (see [Installation](#installation))
4. **Configure**: Set up environment variables in the power's mcp.json
5. **Activate**: Enable the power in Kiro and start using it

Each power is self-contained and can be installed independently.

## Available Powers

### 🤖 AI & Machine Learning
**GitHub URL:** `https://github.com/stormlrd/zens-kiro-powers/tree/main/ai-machine-learning`

Amazon Bedrock, Kendra, Q Business, Knowledge Bases, and Nova Canvas for building intelligent applications.

**Servers:** bedrock-agentcore, kendra-index, qbusiness-anonymous, qindex, bedrock-custom-model-import, bedrock-data-automation, bedrock-kb-retrieval, nova-canvas

### 📊 Data & Analytics
**GitHub URL:** `https://github.com/stormlrd/zens-kiro-powers/tree/main/data-analytics`

DynamoDB, RDS, Aurora DSQL, Neptune, Keyspaces, DocumentDB, ElastiCache, Redshift, and S3 Tables for data management.

**Servers:** dynamodb, aurora-dsql, mysql, postgres, neptune, keyspaces, documentdb, elasticache, memcached, valkey, redshift, s3-tables

### 📡 Integration & Messaging
**GitHub URL:** `https://github.com/stormlrd/zens-kiro-powers/tree/main/integration-messaging`

SNS, SQS, AppSync, Amazon MQ, MSK, and Step Functions for event-driven architectures.

**Servers:** sns-sqs, appsync, amazon-mq, msk, stepfunctions

### ☁️ Getting Started with AWS
**GitHub URL:** `https://github.com/stormlrd/zens-kiro-powers/tree/main/getting-started-aws`

Essential AWS services for beginners - AWS API access and AWS Knowledge Base.

**Servers:** aws-api, aws-knowledge

### 💰 Cost & Operations
**GitHub URL:** `https://github.com/stormlrd/zens-kiro-powers/tree/main/cost-operations`

AWS Pricing, Cost Explorer, CloudWatch, CloudTrail, Billing, and Prometheus for cost optimization and observability.

**Servers:** aws-pricing, cost-explorer, billing-cost-management, cloudwatch, cloudwatch-appsignals, cloudtrail, prometheus

### 🏗️ Infrastructure & Deployment
**GitHub URL:** `https://github.com/stormlrd/zens-kiro-powers/tree/main/infrastructure-deployment`

CDK, CloudFormation, Terraform, Lambda, ECS, EKS, Serverless, and Finch for building and deploying infrastructure.

**Servers:** cdk, cloudformation, terraform, lambda, serverless, ecs, eks, finch, ccapi, support

### 🛠️ Developer Tools & Support
**GitHub URL:** `https://github.com/stormlrd/zens-kiro-powers/tree/main/developer-tools-support`

Code documentation, frontend development, Git research, IAM management, OpenAPI, synthetic data, and security best practices.

**Servers:** code-doc-gen, frontend, git-repo-research, iam, openapi, syntheticdata, well-architected-security

### 🌐 Specialized Services
**GitHub URL:** `https://github.com/stormlrd/zens-kiro-powers/tree/main/specialized-services`

Data processing, AWS diagrams, IoT SiteWise, Location Services, Core utilities, and Timestream for InfluxDB.

**Servers:** data-processing, aws-diagram, iot-sitewise, location, core, timestream-influxdb

### 🏥 Healthcare & Lifesciences
**GitHub URL:** `https://github.com/stormlrd/zens-kiro-powers/tree/main/healthcare-lifesciences`

AWS HealthOmics for genomics and HealthLake for FHIR-based healthcare data management.

**Servers:** healthomics, healthlake

### 📚 Documentation
**GitHub URL:** `https://github.com/stormlrd/zens-kiro-powers/tree/main/documentation`

Comprehensive AWS service documentation, API references, and best practices guides.

**Servers:** aws-documentation

### 📦 Uncategorized
**GitHub URL:** `https://github.com/stormlrd/zens-kiro-powers/tree/main/uncategorized`

Additional AWS services - IAC management, networking, CloudWatch Application Signals, document loading, and SageMaker AI.

**Servers:** aws-iac, aws-network, cloudwatch-applicationsignals, document-loader, sagemaker-ai

### 🚀 Amplify
**GitHub URL:** `https://github.com/stormlrd/zens-kiro-powers/tree/main/amplify`

AWS Amplify for full-stack application development.

**Servers:** appsync, serverless

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

### Option 1: Install from GitHub (Recommended)

1. Open Kiro IDE
2. Open the Powers panel (sidebar)
3. Click "Add Custom Power"
4. Select "Import power from GitHub"
5. Copy and paste the GitHub URL from the power you want (see [Available Powers](#available-powers) section)
   - Example: `https://github.com/stormlrd/zens-kiro-powers/tree/main/ai-machine-learning`
6. Configure environment variables in the power's mcp.json
7. Enable/disable specific servers as needed

### Option 2: Install from Local Folder

1. Clone this repository to your local machine
2. Open Kiro IDE
3. Open the Powers panel (sidebar)
4. Click "Add Custom Power"
5. Select "Import power from a folder"
6. Navigate to and select the specific power folder (e.g., `ai-machine-learning/`)
7. Configure environment variables in the power's mcp.json
8. Enable/disable specific servers as needed

### After Installation

1. Configure required environment variables (see each power's POWER.md)
2. Enable the MCP servers you need
3. Activate the power to start using it

## Usage

Each power can be activated in Kiro to access its MCP servers and steering guidance. Refer to individual POWER.md files for specific usage instructions and examples.

## Publishing to GitHub

This repository is published at: `https://github.com/stormlrd/zens-kiro-powers`

To update or fork:

1. Clone or fork this repository
2. Make your changes
3. Push to your GitHub:
   ```bash
   git add .
   git commit -m "Your changes"
   git push
   ```
4. Share individual power URLs:
   ```
   https://github.com/stormlrd/zens-kiro-powers/tree/main/POWER_NAME
   ```

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
