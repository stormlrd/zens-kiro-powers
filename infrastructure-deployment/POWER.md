---
name: "infrastructure-deployment"
displayName: "Infrastructure & Deployment"
description: "Infrastructure as Code and deployment tools - CDK, CloudFormation, Terraform, Lambda, ECS, EKS, Serverless, and Finch for building and deploying AWS infrastructure"
keywords: ["infrastructure", "deployment", "cdk", "cloudformation", "terraform", "lambda", "ecs", "eks", "iac", "serverless"]
author: "Zen"
repository: "https://github.com/stormlrd/zens-kiro-powers"
---

# Infrastructure & Deployment Power

## Overview

Comprehensive infrastructure as code and deployment tools for AWS, enabling you to build, deploy, and manage cloud infrastructure with best practices.

## Available MCP Servers

### cdk
**Package:** `awslabs.cdk-mcp-server@latest`
**Purpose:** AWS Cloud Development Kit for infrastructure as code

### cloudformation
**Package:** `awslabs.cfn-mcp-server@latest`
**Purpose:** Manage CloudFormation stacks and templates

### terraform
**Package:** `awslabs.terraform-mcp-server@latest`
**Purpose:** Terraform infrastructure management

### lambda
**Package:** `awslabs.lambda-tool-mcp-server@latest`
**Purpose:** Manage and invoke Lambda functions
**Configuration:**
- `FUNCTION_PREFIX` - Filter by prefix
- `FUNCTION_LIST` - Specific functions
- `FUNCTION_TAG_KEY/VALUE` - Filter by tags

### serverless
**Package:** `awslabs.aws-serverless-mcp-server@latest`
**Purpose:** Serverless application deployment

### ecs
**Package:** `awslabs-ecs-mcp-server`
**Purpose:** Manage ECS clusters and services

### eks
**Package:** `awslabs.eks-mcp-server@latest`
**Purpose:** Manage EKS clusters and Kubernetes workloads

### finch
**Package:** `awslabs.finch-mcp-server@latest`
**Purpose:** Container development with Finch

### ccapi
**Package:** `awslabs.ccapi-mcp-server@latest`
**Purpose:** Cloud Control API for resource management

### support
**Package:** `awslabs.aws-support-mcp-server@latest`
**Purpose:** AWS Support case management

## Best Practices

### ✅ Do:
- Use IaC for all infrastructure
- Version control your templates
- Use CDK for complex logic
- Implement CI/CD pipelines
- Tag all resources
- Use separate environments
- Enable drift detection

### ❌ Don't:
- Don't manually create resources
- Don't skip testing
- Don't hardcode values
- Don't ignore security scanning
- Don't skip documentation

---

**Source:** AWS Labs
**License:** Apache-2.0
