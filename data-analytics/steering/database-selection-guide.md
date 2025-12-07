# Database Selection Guide

## Choose the Right Database

### DynamoDB
**Use When:**
- Need single-digit millisecond latency
- Serverless with automatic scaling
- Key-value or document data model
- Unpredictable workload patterns

**Avoid When:**
- Complex joins required
- Need ACID transactions across items
- Require complex queries

### Aurora DSQL
**Use When:**
- Need PostgreSQL compatibility
- True serverless (scale to zero)
- Distributed SQL with strong consistency
- Multi-region active-active

**Avoid When:**
- Need foreign key enforcement
- Require array/JSON column types
- Need triggers or stored procedures

### RDS (MySQL/PostgreSQL)
**Use When:**
- Traditional relational data model
- Need full SQL feature set
- Existing application compatibility
- Complex transactions required

**Avoid When:**
- Need serverless scaling
- Unpredictable traffic patterns
- Want zero operations overhead

### Neptune
**Use When:**
- Highly connected data (social networks)
- Need graph traversals
- Relationship queries are primary
- Knowledge graphs

**Avoid When:**
- Simple key-value lookups
- Tabular data without relationships
- Need SQL interface

### Redshift
**Use When:**
- Data warehousing
- Complex analytics queries
- Large-scale aggregations
- Business intelligence

**Avoid When:**
- Need real-time updates
- Small dataset (<100GB)
- Transactional workload

### ElastiCache/Valkey
**Use When:**
- Need sub-millisecond latency
- Caching layer for databases
- Session management
- Real-time analytics

**Avoid When:**
- Primary data store needed
- Need durability guarantees
- Complex queries required

## Decision Matrix

| Use Case | Recommended Database |
|----------|---------------------|
| E-commerce catalog | DynamoDB |
| User sessions | ElastiCache |
| Financial transactions | Aurora DSQL |
| Social network | Neptune |
| Analytics/BI | Redshift |
| Content management | DocumentDB |
| Time-series data | Keyspaces |
| Multi-tenant SaaS | Aurora DSQL + DynamoDB |
