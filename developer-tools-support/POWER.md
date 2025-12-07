---
name: "developer-tools-support"
displayName: "Developer Tools & Support"
description: "Developer productivity tools - Code documentation generation, frontend development, Git research, IAM management, OpenAPI, synthetic data, and security best practices"
keywords: ["developer", "tools", "documentation", "frontend", "git", "iam", "openapi", "security", "well-architected"]
author: "Zen"
---

# Developer Tools & Support Power

## Overview

Essential developer productivity tools for AWS development, including code documentation, frontend tooling, IAM management, API development, and security best practices.

## Available MCP Servers

### code-doc-gen
**Package:** `awslabs.code-doc-gen-mcp-server@latest`
**Purpose:** Generate code documentation automatically

### frontend
**Package:** `awslabs.frontend-mcp-server@latest`
**Purpose:** Frontend development tools and utilities

### git-repo-research
**Package:** `awslabs.git-repo-research-mcp-server@latest`
**Purpose:** Research and analyze Git repositories
**Configuration:**
- `GITHUB_TOKEN` - GitHub personal access token

### iam
**Package:** `awslabs.iam-mcp-server@latest`
**Purpose:** Manage IAM policies, roles, and permissions

### openapi
**Package:** `awslabs.openapi-mcp-server@latest`
**Purpose:** Work with OpenAPI specifications
**Configuration:**
- `API_NAME` - API name
- `API_BASE_URL` - Base URL
- `API_SPEC_URL` - OpenAPI spec URL

### syntheticdata
**Package:** `awslabs.syntheticdata-mcp-server@latest`
**Purpose:** Generate synthetic test data

### well-architected-security
**Package:** `awslabs.well-architected-security-mcp-server@latest`
**Purpose:** AWS Well-Architected security best practices

## Best Practices

### ✅ Do:
- Document code as you write
- Follow IAM least privilege
- Use OpenAPI for API design
- Generate test data for development
- Follow Well-Architected principles
- Review security regularly

### ❌ Don't:
- Don't skip documentation
- Don't use overly permissive IAM
- Don't hardcode API endpoints
- Don't use production data in dev
- Don't ignore security findings

---

**Source:** AWS Labs
**License:** Apache-2.0
