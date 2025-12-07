---
name: "data-analytics"
displayName: "Data & Analytics"
description: "Data & Analytics services and tools - DynamoDB, RDS, Aurora DSQL, Neptune, Keyspaces, DocumentDB, ElastiCache, Redshift, and S3 Tables for data management"
keywords: ["data", "analytics", "database", "dynamodb", "rds", "aurora", "neptune", "redshift", "sql", "nosql"]
author: "Zen"
repository: "https://github.com/stormlrd/zens-kiro-powers"
---

# Data & Analytics Power

## Overview

The Data & Analytics Power provides comprehensive access to AWS database and analytics services, enabling you to build data-driven applications with various database engines and analytics tools.

**Key capabilities:**
- **NoSQL Databases**: DynamoDB, DocumentDB, Keyspaces
- **Relational Databases**: Aurora DSQL, MySQL, PostgreSQL, Redshift
- **Graph Database**: Neptune for connected data
- **Caching**: ElastiCache (Redis/Valkey), Memcached
- **Analytics**: S3 Tables, Redshift for data warehousing

## Available MCP Servers

### dynamodb
**Package:** `awslabs.dynamodb-mcp-server@latest`
**Purpose:** Manage DynamoDB tables and execute queries
**Authentication:** AWS IAM credentials

### aurora-dsql
**Package:** `awslabs.aurora-dsql-mcp-server@latest`
**Purpose:** PostgreSQL-compatible serverless distributed SQL database
**Authentication:** AWS IAM credentials
**Configuration Required:**
- `CLUSTER` - DSQL cluster identifier
- `REGION` - AWS region

### mysql
**Package:** `awslabs.mysql-mcp-server@latest`
**Purpose:** Connect to RDS MySQL or Aurora MySQL
**Authentication:** AWS IAM credentials
**Configuration Required:**
- `resource_arn` - RDS cluster/instance ARN
- `secret_arn` - Secrets Manager ARN
- `database` - Database name

### postgres
**Package:** `awslabs.postgres-mcp-server@latest`
**Purpose:** Connect to RDS PostgreSQL or Aurora PostgreSQL
**Authentication:** AWS IAM credentials
**Configuration Required:**
- `resource_arn` - RDS cluster/instance ARN
- `secret_arn` - Secrets Manager ARN
- `database` - Database name

### neptune
**Package:** `awslabs.amazon-neptune-mcp-server@latest`
**Purpose:** Query graph data with Gremlin or SPARQL
**Authentication:** AWS IAM credentials
**Configuration Required:**
- `NEPTUNE_ENDPOINT` - Neptune cluster endpoint

### keyspaces
**Package:** `awslabs.amazon-keyspaces-mcp-server@latest`
**Purpose:** Cassandra-compatible managed database
**Authentication:** AWS IAM credentials

### documentdb
**Package:** `awslabs.documentdb-mcp-server@latest`
**Purpose:** MongoDB-compatible document database
**Authentication:** AWS IAM credentials

### elasticache
**Package:** `awslabs.elasticache-mcp-server@latest`
**Purpose:** Manage Redis/Valkey clusters
**Authentication:** AWS IAM credentials

### memcached
**Package:** `awslabs.memcached-mcp-server@latest`
**Purpose:** Connect to Memcached clusters
**Configuration Required:**
- `MEMCACHED_HOST` - Cluster endpoint
- `MEMCACHED_PORT` - Port (default: 11211)

### valkey
**Package:** `awslabs.valkey-mcp-server@latest`
**Purpose:** Open-source Redis alternative
**Configuration Required:**
- `VALKEY_HOST` - Cluster endpoint
- `VALKEY_PORT` - Port (default: 6379)

### redshift
**Package:** `awslabs.redshift-mcp-server@latest`
**Purpose:** Data warehouse queries and management
**Authentication:** AWS IAM credentials

### s3-tables
**Package:** `awslabs.s3-tables-mcp-server@latest`
**Purpose:** Query data in S3 with table format
**Authentication:** AWS IAM credentials

## Best Practices

### ✅ Do:

- **Choose the right database** - Match database type to use case
- **Use connection pooling** - Reuse connections efficiently
- **Implement caching** - Use ElastiCache for frequently accessed data
- **Monitor performance** - Track query latency and throughput
- **Secure credentials** - Use Secrets Manager for database passwords
- **Backup regularly** - Enable automated backups
- **Use read replicas** - Scale read operations

### ❌ Don't:

- **Never hardcode credentials** - Use Secrets Manager or IAM auth
- **Never skip indexing** - Create appropriate indexes
- **Never ignore limits** - Respect service quotas
- **Never use SELECT *** - Query only needed columns
- **Never skip connection management** - Close connections properly
- **Never ignore costs** - Monitor and optimize database usage

## Configuration

**Authentication Required**: AWS IAM credentials

**Environment Variables:**
- `AWS_PROFILE` - AWS CLI profile name
- `AWS_REGION` - AWS region
- `FASTMCP_LOG_LEVEL` - Logging level

## Tips

1. **DynamoDB**: Use single-table design for efficiency
2. **Aurora DSQL**: Understand constraints (no foreign keys, arrays)
3. **Neptune**: Use Gremlin for property graphs, SPARQL for RDF
4. **ElastiCache**: Implement cache-aside pattern
5. **Redshift**: Use COPY for bulk loads
6. **RDS**: Enable Performance Insights for monitoring

---

**Source:** AWS Labs
**License:** Apache-2.0
