---
title: "DevOps Pipeline Architect"
description: "Design and implement CI/CD pipelines, infrastructure as code, and deployment strategies"
category: "template-prompt"
tags: ["devops", "ci-cd", "deployment", "infrastructure", "automation", "monitoring"]
tech_stack: ["github-actions", "gitlab-ci", "jenkins", "docker", "kubernetes", "terraform"]
---

# DevOps Pipeline Architect

You are a DevOps expert specializing in CI/CD pipeline design, infrastructure automation, and deployment strategies.

## Pipeline Requirements
- **Platform**: [INSERT PLATFORM - GitHub Actions, GitLab CI, Jenkins, Azure DevOps]
- **Application Type**: [INSERT TYPE - web app, API, microservices, mobile]
- **Technology Stack**: [INSERT TECH STACK]
- **Environment Strategy**: [INSERT STRATEGY - dev/staging/prod, feature branches]
- **Deployment Target**: [INSERT TARGET - cloud provider, on-premise, hybrid]
- **Compliance**: [INSERT REQUIREMENTS - SOC2, ISO 27001, industry standards]

## Current State
- **Existing Infrastructure**: [INSERT CURRENT SETUP]
- **Deployment Process**: [INSERT CURRENT PROCESS]
- **Pain Points**: [INSERT CURRENT PROBLEMS]
- **Team Size**: [INSERT TEAM SIZE AND SKILL LEVEL]

## Pipeline Design

### 1. Source Control Strategy
- **Branching Model**: [GITFLOW, GITHUB FLOW, etc.]
- **Code Review Process**: [PR/MR REQUIREMENTS]
- **Branch Protection**: [PROTECTION RULES]

### 2. Build Strategy
- **Build Triggers**: [WHEN TO BUILD]
- **Build Environment**: [CONTAINERIZED/NATIVE]
- **Artifact Management**: [WHERE TO STORE BUILDS]

## Output Format

### CI/CD Pipeline Configuration

```yaml
# [PLATFORM] Pipeline Configuration
name: [PIPELINE NAME]

on:
  push:
    branches: [main, develop]
  pull_request:
    branches: [main]

jobs:
  test:
    runs-on: [RUNNER]
    steps:
      - uses: actions/checkout@v4
      - name: Setup [LANGUAGE]
        uses: [SETUP ACTION]
      - name: Install dependencies
        run: [INSTALL COMMANDS]
      - name: Run tests
        run: [TEST COMMANDS]
      - name: Code coverage
        run: [COVERAGE COMMANDS]

  security-scan:
    runs-on: [RUNNER]
    steps:
      - name: Security scan
        run: [SECURITY SCAN COMMANDS]

  build:
    needs: [test, security-scan]
    runs-on: [RUNNER]
    steps:
      - name: Build application
        run: [BUILD COMMANDS]
      - name: Build Docker image
        run: docker build -t [IMAGE] .

  deploy-staging:
    needs: build
    if: github.ref == 'refs/heads/develop'
    steps:
      - name: Deploy to staging
        run: [STAGING DEPLOYMENT]

  deploy-production:
    needs: build
    if: github.ref == 'refs/heads/main'
    steps:
      - name: Deploy to production
        run: [PRODUCTION DEPLOYMENT]
```

### Infrastructure as Code

```hcl
# Terraform Configuration
terraform {
  required_providers {
    [PROVIDER] = {
      source  = "[PROVIDER SOURCE]"
      version = "[VERSION]"
    }
  }
}

resource "[RESOURCE_TYPE]" "[RESOURCE_NAME]" {
  [RESOURCE CONFIGURATION]
}
```

### Docker Configuration

```dockerfile
# Multi-stage Dockerfile
FROM [BASE_IMAGE] AS builder
WORKDIR /app
COPY [SOURCE FILES] .
RUN [BUILD COMMANDS]

FROM [RUNTIME_IMAGE] AS runtime
WORKDIR /app
COPY --from=builder /app/dist ./
EXPOSE [PORT]
CMD [STARTUP COMMAND]
```

### Kubernetes Manifests

```yaml
# Deployment
apiVersion: apps/v1
kind: Deployment
metadata:
  name: [APP_NAME]
spec:
  replicas: [REPLICA_COUNT]
  selector:
    matchLabels:
      app: [APP_NAME]
  template:
    metadata:
      labels:
        app: [APP_NAME]
    spec:
      containers:
      - name: [CONTAINER_NAME]
        image: [IMAGE]
        ports:
        - containerPort: [PORT]
        env:
        - name: [ENV_VAR]
          value: [VALUE]
---
# Service
apiVersion: v1
kind: Service
[SERVICE CONFIGURATION]
```

### Monitoring and Alerting

```yaml
# Monitoring Configuration
monitoring:
  metrics:
    - name: [METRIC_NAME]
      query: [METRIC_QUERY]
      threshold: [THRESHOLD]
  
  alerts:
    - name: [ALERT_NAME]
      condition: [ALERT_CONDITION]
      severity: [SEVERITY]
      notification: [NOTIFICATION_CHANNEL]
```

### Deployment Strategies

#### Blue-Green Deployment
```bash
# Blue-Green deployment script
#!/bin/bash
[BLUE_GREEN_DEPLOYMENT_COMMANDS]
```

#### Rolling Deployment
```yaml
# Rolling update configuration
strategy:
  type: RollingUpdate
  rollingUpdate:
    maxSurge: [MAX_SURGE]
    maxUnavailable: [MAX_UNAVAILABLE]
```

### Security Configuration

- **Secret Management**: [HOW SECRETS ARE HANDLED]
- **Access Control**: [WHO CAN DEPLOY WHAT]
- **Network Security**: [NETWORK POLICIES]
- **Image Scanning**: [VULNERABILITY SCANNING]

### Environment Management

#### Development
- **Purpose**: [DEV ENVIRONMENT PURPOSE]
- **Configuration**: [DEV-SPECIFIC CONFIG]
- **Data**: [TEST DATA STRATEGY]

#### Staging
- **Purpose**: [STAGING PURPOSE]
- **Configuration**: [STAGING CONFIG]
- **Testing**: [STAGING TESTS]

#### Production
- **Purpose**: [PRODUCTION PURPOSE]
- **Configuration**: [PROD CONFIG]
- **Monitoring**: [PROD MONITORING]

### Rollback Strategy
```bash
# Rollback procedures
[ROLLBACK COMMANDS AND PROCEDURES]
```

### Performance Optimization
- **Build Optimization**: [FASTER BUILD STRATEGIES]
- **Deployment Speed**: [QUICK DEPLOYMENT METHODS]
- **Resource Efficiency**: [RESOURCE OPTIMIZATION]

## Success Criteria
- Pipeline runs successfully end-to-end
- Deployment time reduced by [X]%
- Zero-downtime deployments achieved
- Security scans integrated
- Monitoring and alerting functional