---
name: "healthcare-lifesciences"
displayName: "Healthcare & Lifesciences"
description: "Healthcare and lifesciences services - AWS HealthOmics for genomics and HealthLake for FHIR-based healthcare data management"
keywords: ["healthcare", "lifesciences", "healthomics", "healthlake", "genomics", "fhir", "medical"]
author: "Zen"
---

# Healthcare & Lifesciences Power

## Overview

Specialized services for healthcare and lifesciences applications, including genomics analysis with HealthOmics and FHIR-based healthcare data management with HealthLake.

## Available MCP Servers

### healthomics
**Package:** `awslabs.aws-healthomics-mcp-server@latest`
**Purpose:** Genomics data storage, analysis, and workflow management
**Authentication:** AWS IAM credentials

### healthlake
**Package:** `awslabs.healthlake-mcp-server@latest`
**Purpose:** FHIR-based healthcare data store and analytics
**Authentication:** AWS IAM credentials

## Best Practices

### ✅ Do:
- Ensure HIPAA compliance
- Encrypt all healthcare data
- Use VPC endpoints for private access
- Implement audit logging
- Follow FHIR standards
- Use appropriate data retention policies

### ❌ Don't:
- Don't store PHI without encryption
- Don't skip compliance requirements
- Don't ignore access controls
- Don't forget audit trails

## Configuration

**Authentication Required**: AWS IAM credentials

**Environment Variables:**
- `AWS_PROFILE` - AWS CLI profile name
- `AWS_REGION` - AWS region
- `MCP_LOG_LEVEL` - Logging level

## Tips

1. **HealthOmics**: Use for genomics workflows and variant analysis
2. **HealthLake**: Store and query FHIR resources
3. **Compliance**: Enable CloudTrail and Config for audit
4. **Security**: Use KMS for encryption
5. **Integration**: Connect with existing EHR systems

---

**Source:** AWS Labs
**License:** Apache-2.0
