---
name: "integration-messaging"
displayName: "Integration & Messaging"
description: "Integration & Messaging services - SNS, SQS, AppSync, Amazon MQ, MSK, and Step Functions for building event-driven and messaging architectures"
keywords: ["messaging", "integration", "sns", "sqs", "appsync", "mq", "kafka", "msk", "stepfunctions", "events"]
author: "Zen"
---

# Integration & Messaging Power

## Overview

Provides access to AWS messaging and integration services for building event-driven, decoupled architectures with pub/sub patterns, message queues, GraphQL APIs, and workflow orchestration.

## Available MCP Servers

### sns-sqs
**Package:** `awslabs.amazon-sns-sqs-mcp-server@latest`
**Purpose:** Manage SNS topics and SQS queues for pub/sub and queuing patterns

### appsync
**Package:** `awslabs.aws-appsync-mcp-server@latest`
**Purpose:** Manage GraphQL APIs with AppSync

### amazon-mq
**Package:** `awslabs.amazon-mq-mcp-server@latest`
**Purpose:** Managed message broker service (ActiveMQ, RabbitMQ)

### msk
**Package:** `awslabs.aws-msk-mcp-server@latest`
**Purpose:** Managed Kafka service for streaming data

### stepfunctions
**Package:** `awslabs.stepfunctions-tool-mcp-server@latest`
**Purpose:** Orchestrate workflows with Step Functions
**Configuration:**
- `STATE_MACHINE_PREFIX` - Filter by prefix
- `STATE_MACHINE_LIST` - Specific state machines
- `STATE_MACHINE_TAG_KEY/VALUE` - Filter by tags

## Best Practices

### ✅ Do:
- Use SNS for fan-out patterns
- Use SQS for decoupling services
- Implement dead-letter queues
- Use FIFO queues when order matters
- Enable message encryption
- Monitor queue depth

### ❌ Don't:
- Don't use SQS for real-time messaging
- Don't skip error handling
- Don't ignore message retention limits
- Don't forget idempotency

---

**Source:** AWS Labs
**License:** Apache-2.0
