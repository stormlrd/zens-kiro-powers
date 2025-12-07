---
name: "cost-operations"
displayName: "Cost & Operations"
description: "Cost management and operational monitoring - AWS Pricing, Cost Explorer, CloudWatch, CloudTrail, Billing, and Prometheus for cost optimization and observability"
keywords: ["cost", "operations", "pricing", "cloudwatch", "monitoring", "billing", "observability", "prometheus"]
author: "Zen"
---

# Cost & Operations Power

## Overview

Comprehensive cost management and operational monitoring tools for AWS, enabling cost optimization, performance monitoring, and operational excellence.

## Available MCP Servers

### aws-pricing
**Package:** `awslabs.aws-pricing-mcp-server@latest`
**Purpose:** Access real-time AWS pricing information

### cost-explorer
**Package:** `awslabs.cost-explorer-mcp-server@latest`
**Purpose:** Analyze and forecast AWS costs

### billing-cost-management
**Package:** `awslabs.billing-cost-management-mcp-server@latest`
**Purpose:** Manage billing and cost allocation

### cloudwatch
**Package:** `awslabs.cloudwatch-mcp-server@latest`
**Purpose:** Monitor metrics, logs, and alarms

### cloudwatch-appsignals
**Package:** `awslabs.cloudwatch-appsignals-mcp-server@latest`
**Purpose:** Application performance monitoring

### cloudtrail
**Package:** `awslabs.cloudtrail-mcp-server@latest`
**Purpose:** Audit AWS API calls and governance

### prometheus
**Package:** `awslabs.prometheus-mcp-server@latest`
**Purpose:** Prometheus metrics integration

## Best Practices

### ✅ Do:
- Set up billing alerts
- Review costs weekly
- Use Cost Explorer for trends
- Tag resources for allocation
- Enable CloudWatch alarms
- Monitor key metrics
- Use CloudTrail for auditing

### ❌ Don't:
- Don't ignore cost anomalies
- Don't skip resource tagging
- Don't disable CloudTrail
- Don't ignore alarms
- Don't forget to clean up unused resources

---

**Source:** AWS Labs
**License:** Apache-2.0
