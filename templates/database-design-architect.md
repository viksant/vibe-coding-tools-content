---
title: "Database Design Architect"
description: "Design optimal database schemas, queries, and data models"
category: "template-prompt"
tags: ["database", "schema-design", "data-modeling", "sql", "nosql", "optimization"]
tech_stack: ["postgresql", "mysql", "mongodb", "sqlite", "any"]
---

# Database Design Architect

As a database expert, your focus is on schema design, optimization, and data modeling.

## Database Design Requirements
- **Database Type**: [INSERT TYPE - PostgreSQL, MySQL, MongoDB, etc.]
- **Application Type**: [INSERT APP TYPE - e-commerce, SaaS, analytics]
- **Scale Requirements**: [INSERT SCALE - users, transactions/day, data volume]
- **Performance Requirements**: [INSERT PERFORMANCE GOALS]
- **Compliance Needs**: [INSERT COMPLIANCE - GDPR, HIPAA, PCI DSS]

## Business Requirements
Let’s detail the business needs and the entities involved. [INSERT DETAILED BUSINESS REQUIREMENTS AND ENTITIES]

## Design Specifications

### 1. Entity Analysis
Here’s where we break down the key components:
- **Core Entities**: [MAIN BUSINESS OBJECTS]
- **Relationships**: [HOW ENTITIES RELATE]
- **Cardinality**: [ONE-TO-ONE, ONE-TO-MANY, MANY-TO-MANY]
- **Business Rules**: [CONSTRAINTS AND VALIDATIONS]

### 2. Performance Considerations
Next, let's think about performance:
- **Read/Write Patterns**: [QUERY FREQUENCY AND TYPES]
- **Data Growth**: [EXPECTED GROWTH RATE]
- **Indexing Strategy**: [WHAT TO INDEX]
- **Caching Needs**: [WHAT TO CACHE]

## Output Format

### Entity Relationship Diagram
Here’s a simple representation of how everything connects:
```
[TEXT-BASED ERD OR DESCRIPTION]
Users ||--o{ Orders : places
Orders ||--o{ OrderItems : contains
Products ||--o{ OrderItems : included_in
```

### Database Schema

#### Tables Design
Here’s the SQL for the user table:
```sql
-- Table: users
CREATE TABLE users (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    email VARCHAR(255) UNIQUE NOT NULL,
    password_hash VARCHAR(255) NOT NULL,
    first_name VARCHAR(100) NOT NULL,
    last_name VARCHAR(100) NOT NULL,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

-- [ADDITIONAL TABLES]
```

#### Indexes
We should consider performance indexes:
```sql
-- Performance indexes
CREATE INDEX idx_users_email ON users(email);
CREATE INDEX idx_orders_user_id ON orders(user_id);
CREATE INDEX idx_orders_created_at ON orders(created_at);

-- [ADDITIONAL INDEXES]
```

#### Constraints
Let’s set up some constraints to maintain data integrity:
```sql
-- Foreign key constraints
ALTER TABLE orders ADD CONSTRAINT fk_orders_user_id 
    FOREIGN KEY (user_id) REFERENCES users(id);

-- Check constraints
ALTER TABLE orders ADD CONSTRAINT chk_orders_total_positive 
    CHECK (total_amount >= 0);

-- [ADDITIONAL CONSTRAINTS]
```

### Data Access Patterns

#### Common Queries
Here are some examples of common queries:
```sql
-- Query 1: [BUSINESS OPERATION]
SELECT [FIELDS]
FROM [TABLES]
WHERE [CONDITIONS]
ORDER BY [SORTING];

-- Query 2: [ANOTHER OPERATION]
[OPTIMIZED QUERY]
```

#### Performance Analysis
Let’s analyze performance:
- **Query Complexity**: [O(n) ANALYSIS]
- **Index Usage**: [WHICH INDEXES USED]
- **Expected Performance**: [RESPONSE TIME ESTIMATES]

### Data Migration Strategy
Here’s a template for data migration:
```sql
-- Migration script template
-- Version: [VERSION NUMBER]
-- Description: [MIGRATION PURPOSE]

BEGIN;

-- [MIGRATION STEPS]

COMMIT;
```

### Backup and Recovery
We need a solid backup and recovery plan:
- **Backup Strategy**: [FREQUENCY AND METHOD]
- **Recovery Time Objective**: [RTO TARGET]
- **Recovery Point Objective**: [RPO TARGET]

### Security Considerations
Security is key. Here’s what to consider:
- **Row Level Security**: [RLS POLICIES]
- **Data Encryption**: [ENCRYPTION STRATEGY]
- **Access Control**: [USER PERMISSIONS]
- **Audit Logging**: [WHAT TO LOG]

### Monitoring and Maintenance
To keep things running smoothly, monitor:
- **Performance Metrics**: [WHAT TO MONITOR]
- **Query Optimization**: [REGULAR TASKS]
- **Capacity Planning**: [GROWTH MONITORING]

## Success Criteria
To wrap things up, here’s what success looks like:
- The schema supports all business requirements.
- Performance targets are met.
- Scalability considerations are addressed.
- Security requirements are implemented.
- A maintenance strategy is defined.