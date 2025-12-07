---
name: "specialized-services"
displayName: "Specialized Services"
description: "Specialized AWS services - Data processing, AWS diagrams, IoT SiteWise, Location Services, Core utilities, and Timestream for InfluxDB"
keywords: ["specialized", "iot", "location", "diagrams", "timestream", "data-processing", "utilities"]
author: "Zen"
---

# Specialized Services Power

## Overview

Access to specialized AWS services for specific use cases including IoT, location services, data processing, architecture diagrams, and time-series data.

## Available MCP Servers

### data-processing
**Package:** `awslabs.aws-dataprocessing-mcp-server@latest`
**Purpose:** Data transformation and processing utilities

### aws-diagram
**Package:** `awslabs.aws-diagram-mcp-server@latest`
**Purpose:** Generate AWS architecture diagrams

### iot-sitewise
**Package:** `awslabs.aws-iot-sitewise-mcp-server@latest`
**Purpose:** Manage IoT SiteWise assets and data

### location
**Package:** `awslabs.aws-location-mcp-server@latest`
**Purpose:** Location-based services and mapping

### core
**Package:** `awslabs.core-mcp-server@latest`
**Purpose:** Core AWS utilities and helpers

### timestream-influxdb
**Package:** `awslabs.timestream-for-influxdb-mcp-server@latest`
**Purpose:** Time-series database with InfluxDB compatibility

## Best Practices

### ✅ Do:
- Use diagrams for documentation
- Leverage location services for geospatial data
- Use IoT SiteWise for industrial data
- Choose Timestream for time-series workloads

### ❌ Don't:
- Don't use general databases for time-series
- Don't skip diagram documentation
- Don't ignore IoT security

---

**Source:** AWS Labs
**License:** Apache-2.0
