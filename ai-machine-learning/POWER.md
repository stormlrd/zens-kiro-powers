---
name: "ai-machine-learning"
displayName: "AI & Machine Learning"
description: "AI & Machine Learning services and tools - Amazon Bedrock, Kendra, Q Business, Knowledge Bases, and Nova Canvas for building intelligent applications"
keywords: ["ai", "ml", "bedrock", "kendra", "qbusiness", "knowledge-base", "nova", "machine-learning", "genai"]
author: "Zen"
repository: "https://github.com/stormlrd/zens-kiro-powers"
---

# AI & Machine Learning Power

## Overview

The AI & Machine Learning Power provides comprehensive access to AWS AI and ML services, enabling you to build intelligent applications with foundation models, knowledge bases, search capabilities, and generative AI tools.

**Key capabilities:**
- **Amazon Bedrock**: Access foundation models and custom model imports
- **Knowledge Management**: Kendra search, Q Business, and Bedrock Knowledge Bases
- **Data Automation**: Bedrock Data Automation for document processing
- **Image Generation**: Nova Canvas for AI-powered image creation
- **Agent Core**: Build AI agents with Bedrock Agent Core

## Available MCP Servers

### bedrock-agentcore
**Package:** `awslabs.amazon-bedrock-agentcore-mcp-server@latest`
**Purpose:** Build and manage AI agents with Amazon Bedrock Agent Core
**Authentication:** AWS IAM credentials

### kendra-index
**Package:** `awslabs.amazon-kendra-index-mcp-server@latest`
**Purpose:** Search and retrieve information from Amazon Kendra indexes
**Authentication:** AWS IAM credentials
**Configuration Required:**
- `KEND_INDEX_ID` - Your Kendra index ID
- `KEND_ROLE_ARN` - IAM role ARN for Kendra access

### qbusiness-anonymous
**Package:** `awslabs.amazon-qbusiness-anonymous-mcp-server@latest`
**Purpose:** Interact with Amazon Q Business applications
**Authentication:** AWS IAM credentials
**Configuration Required:**
- `QBUSINESS_APP_ID` - Your Q Business application ID
- `QBUSINESS_USER_ID` - User identifier

### qindex
**Package:** `awslabs.amazon-qindex-mcp-server@latest`
**Purpose:** Manage and query Amazon Q indexes
**Authentication:** AWS IAM credentials
**Configuration Required:**
- `QINDEX_ID` - Your Q index ID

### bedrock-custom-model-import
**Package:** `awslabs.aws-bedrock-custom-model-import-mcp-server@latest`
**Purpose:** Import custom models into Amazon Bedrock
**Authentication:** AWS IAM credentials
**Configuration Required:**
- `BEDROCK_MODEL_IMPORT_S3_BUCKET` - S3 bucket for model storage
- `BEDROCK_MODEL_IMPORT_ROLE_ARN` - IAM role ARN

### bedrock-data-automation
**Package:** `awslabs.aws-bedrock-data-automation-mcp-server@latest`
**Purpose:** Automate document processing with Bedrock Data Automation
**Authentication:** AWS IAM credentials
**Configuration Required:**
- `AWS_BUCKET_NAME` - S3 bucket for document storage
- `BASE_DIR` - Base directory for processing

### bedrock-kb-retrieval
**Package:** `awslabs.bedrock-kb-retrieval-mcp-server@latest`
**Purpose:** Retrieve information from Bedrock Knowledge Bases
**Authentication:** AWS IAM credentials
**Configuration:**
- `KB_INCLUSION_TAG_KEY` - Optional tag key to filter knowledge bases
- `BEDROCK_KB_RERANKING_ENABLED` - Enable/disable reranking (default: false)

### nova-canvas
**Package:** `awslabs.nova-canvas-mcp-server@latest`
**Purpose:** Generate images using Amazon Nova Canvas
**Authentication:** AWS IAM credentials

## Best Practices

### ✅ Do:

- **Use appropriate models** - Select foundation models based on your use case
- **Implement RAG patterns** - Combine Knowledge Bases with generation for accuracy
- **Tag resources** - Use tags to organize and filter AI/ML resources
- **Monitor costs** - Track model invocations and data processing costs
- **Secure credentials** - Use IAM roles and least privilege access
- **Test thoroughly** - Validate AI outputs before production use

### ❌ Don't:

- **Never hardcode credentials** - Use AWS profiles or IAM roles
- **Never skip validation** - Always validate AI-generated content
- **Never ignore limits** - Respect service quotas and rate limits
- **Never expose sensitive data** - Sanitize inputs to AI models
- **Never cache tokens long-term** - Refresh credentials regularly

## Configuration

**Authentication Required**: AWS IAM credentials

**Environment Variables:**
- `AWS_PROFILE` - AWS CLI profile name
- `AWS_REGION` - AWS region (e.g., us-east-1)
- `FASTMCP_LOG_LEVEL` - Logging level (ERROR, INFO, DEBUG)

**Setup Steps:**
1. Configure AWS credentials (`aws configure`)
2. Create required resources (Kendra indexes, Q Business apps, etc.)
3. Note resource IDs and ARNs
4. Install this power and configure environment variables
5. Test connection with appropriate tools

## Tips

1. **Start with Knowledge Bases** - Use Bedrock KB for RAG patterns
2. **Leverage Kendra** - For enterprise search capabilities
3. **Use Q Business** - For conversational AI experiences
4. **Monitor usage** - Track costs and optimize model selection
5. **Implement guardrails** - Use Bedrock Guardrails for safety
6. **Test prompts** - Iterate on prompt engineering
7. **Cache responses** - Reduce costs with intelligent caching
8. **Use streaming** - For better user experience with long responses

---

**Source:** AWS Labs
**License:** Apache-2.0
