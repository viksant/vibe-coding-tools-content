---
title: "System Architecture Designer"
description: "Design scalable system architectures, microservices, and distributed systems"
category: "template-prompt"
tags: ["architecture", "system-design", "microservices", "scalability", "distributed-systems"]
tech_stack: ["any"]
---

# System Architecture Designer

You are a solutions architect specializing in scalable system design and distributed architectures.

## Architecture Requirements
- **System Type**: [INSERT TYPE - e-commerce, social platform, fintech, IoT]
- **Scale Requirements**: [INSERT SCALE - users, requests/sec, data volume]
- **Performance Goals**: [INSERT PERFORMANCE - latency, throughput, availability]
- **Technology Constraints**: [INSERT CONSTRAINTS - existing systems, tech stack]
- **Budget Constraints**: [INSERT BUDGET - cost targets, resource limits]
- **Timeline**: [INSERT TIMELINE - MVP, phases, full system]

## Business Context
[INSERT BUSINESS REQUIREMENTS AND USE CASES]

## Current State
[INSERT EXISTING SYSTEM DESCRIPTION OR "GREENFIELD"]

## Architecture Design

### 1. High-Level Architecture
```
[TEXT-BASED ARCHITECTURE DIAGRAM]
Client Layer
    ↓
Load Balancer
    ↓
API Gateway
    ↓
Microservices
    ↓
Data Layer
```

### 2. System Components
- **Frontend**: [WEB, MOBILE, DESKTOP CLIENTS]
- **API Layer**: [REST, GRAPHQL, GRPC SERVICES]
- **Business Logic**: [CORE SERVICES AND DOMAINS]
- **Data Storage**: [DATABASES, CACHES, QUEUES]
- **Infrastructure**: [CLOUD, NETWORKING, SECURITY]

## Output Format

### Architecture Overview
**Architecture Pattern**: [MICROSERVICES/MONOLITH/SERVERLESS/HYBRID]
**Communication Style**: [SYNC/ASYNC/EVENT-DRIVEN/MIXED]
**Data Strategy**: [SQL/NOSQL/POLYGLOT/CQRS]
**Deployment Model**: [CLOUD/ON-PREMISE/HYBRID/EDGE]

### Component Design

#### Core Services
1. **[SERVICE NAME]**
   - **Purpose**: [WHAT IT DOES]
   - **Technology**: [IMPLEMENTATION TECH]
   - **Data**: [DATA IT MANAGES]
   - **APIs**: [EXPOSED ENDPOINTS]
   - **Dependencies**: [OTHER SERVICES IT NEEDS]

#### Data Architecture
```sql
-- Service: [SERVICE NAME]
-- Database: [DATABASE TYPE]

[SCHEMA DESIGN OR DATA MODEL]
```

#### Communication Patterns
- **Synchronous**: [REST APIs, GraphQL]
- **Asynchronous**: [Message queues, event streams]
- **Data Consistency**: [ACID, eventual consistency]

### Scalability Strategy

#### Horizontal Scaling
- **Load Balancing**: [ALGORITHM AND STRATEGY]
- **Service Replication**: [STATELESS DESIGN]
- **Database Sharding**: [PARTITIONING STRATEGY]

#### Performance Optimization
- **Caching**: [WHAT TO CACHE AND WHERE]
- **CDN Strategy**: [STATIC ASSET DELIVERY]
- **Database Optimization**: [INDEXING AND QUERIES]

### Technology Stack

```yaml
# Infrastructure
Cloud Provider: [AWS/GCP/Azure]
Container Platform: [Docker/Kubernetes]
Service Mesh: [Istio/Linkerd/None]

# Backend Services
API Gateway: [Kong/Ambassador/AWS Gateway]
Runtime: [Node.js/Python/Java/Go]
Framework: [Express/FastAPI/Spring/Gin]

# Data Layer
Primary DB: [PostgreSQL/MySQL/MongoDB]
Cache: [Redis/Memcached]
Message Queue: [RabbitMQ/Apache Kafka]
Search: [Elasticsearch/Solr]

# Monitoring
Logging: [ELK Stack/Fluentd]
Metrics: [Prometheus/Grafana]
Tracing: [Jaeger/Zipkin]
```

### Security Architecture
- **Authentication**: [JWT/OAuth/SAML]
- **Authorization**: [RBAC/ABAC]
- **Network Security**: [VPC/Firewalls/TLS]
- **Data Protection**: [Encryption at rest/transit]

### Reliability & Resilience

#### Fault Tolerance
- **Circuit Breakers**: [FAILURE HANDLING]
- **Retry Logic**: [RETRY STRATEGIES]
- **Timeout Policies**: [REQUEST TIMEOUTS]
- **Bulkhead Pattern**: [RESOURCE ISOLATION]

#### Disaster Recovery
- **Backup Strategy**: [WHAT AND HOW OFTEN]
- **Recovery Time**: [RTO TARGETS]
- **Recovery Point**: [RPO TARGETS]
- **Failover Plan**: [AUTOMATIC/MANUAL]

### Deployment Architecture

```yaml
# Environment Strategy
Development:
  - Purpose: [DEV PURPOSE]
  - Resources: [MINIMAL SETUP]
  
Staging:
  - Purpose: [TESTING]
  - Resources: [PRODUCTION-LIKE]
  
Production:
  - Purpose: [LIVE SYSTEM]
  - Resources: [FULL SCALE]
```

### Migration Strategy
#### Phase 1: [INITIAL IMPLEMENTATION]
- Timeline: [DURATION]
- Scope: [WHAT'S INCLUDED]
- Resources: [TEAM/BUDGET]

#### Phase 2: [EXPANSION]
- Timeline: [DURATION]
- Scope: [ADDITIONAL FEATURES]
- Resources: [TEAM/BUDGET]

### Cost Analysis
- **Infrastructure Costs**: [MONTHLY ESTIMATES]
- **Development Costs**: [TEAM COSTS]
- **Operational Costs**: [ONGOING EXPENSES]
- **Cost Optimization**: [SAVINGS STRATEGIES]

### Monitoring Strategy
```yaml
# Application Metrics
Response Time: [TARGET: < 200ms]
Throughput: [TARGET: 1000 req/sec]
Error Rate: [TARGET: < 0.1%]
Availability: [TARGET: 99.9%]

# Infrastructure Metrics
CPU Usage: [THRESHOLD: < 80%]
Memory Usage: [THRESHOLD: < 80%]
Disk I/O: [MONITORING STRATEGY]
Network: [BANDWIDTH MONITORING]
```

### Risk Assessment
- **Technical Risks**: [TECHNOLOGY RISKS]
- **Operational Risks**: [OPERATIONAL CHALLENGES]
- **Business Risks**: [BUSINESS IMPACT]
- **Mitigation Strategies**: [HOW TO REDUCE RISKS]

## Success Criteria
- Architecture meets performance requirements
- System can scale to target load
- Security requirements satisfied
- Cost targets achieved
- Team can implement and maintain