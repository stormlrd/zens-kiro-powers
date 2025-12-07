---
name: "getting-started-aws"
displayName: "Getting Started with AWS"
description: "Essential AWS services for beginners - AWS API access and AWS Knowledge Base for learning and exploring AWS services"
keywords: ["aws", "getting-started", "api", "knowledge", "documentation", "learning", "beginner"]
author: "Zen"
repository: "https://github.com/stormlrd/zens-kiro-powers"
---

# Getting Started with AWS Power

## Overview

The perfect starting point for AWS development, providing direct API access and comprehensive knowledge base for learning AWS services and best practices.

## Available MCP Servers

### aws-api
**Package:** `awslabs.aws-api-mcp-server@latest`
**Purpose:** Execute AWS API calls directly with validation
**Authentication:** AWS IAM credentials

### aws-knowledge
**Type:** HTTP server
**URL:** https://knowledge-mcp.global.api.aws
**Purpose:** Access AWS best practices, documentation, and service announcements

## Best Practices

### ✅ Do:
- Start with aws-knowledge to learn services
- Use aws-api for hands-on experimentation
- Follow AWS Well-Architected principles
- Enable CloudTrail for auditing
- Use IAM roles instead of access keys

### ❌ Don't:
- Don't hardcode credentials
- Don't skip security best practices
- Don't ignore cost monitoring
- Don't use root account for daily tasks

## Tips

1. **Learn by doing** - Use aws-api to experiment
2. **Read documentation** - Query aws-knowledge for guidance
3. **Start small** - Begin with simple services
4. **Monitor costs** - Set up billing alerts
5. **Follow security** - Use least privilege access

---

**Source:** AWS Labs
**License:** Apache-2.0
