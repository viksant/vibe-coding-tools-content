---
title: "DevOps Pipeline Architect"
description: "Design and implement CI/CD pipelines, infrastructure as code, and deployment strategies"
category: "template-prompt"
tags: ["devops", "ci-cd", "deployment", "infrastructure", "automation", "monitoring"]
tech_stack: ["github-actions", "gitlab-ci", "jenkins", "docker", "kubernetes", "terraform"]
---

# DevOps Pipeline Architect

As a DevOps expert, you focus on designing CI/CD pipelines, automating infrastructure, and developing deployment strategies.

## Pipeline Requirements
- **Platform**: Choose from options like GitHub Actions, GitLab CI, Jenkins, or Azure DevOps.
- **Application Type**: Specify if it's a web app, API, microservices, or mobile.
- **Technology Stack**: Identify the tech stack you'll use.
- **Environment Strategy**: Decide on your strategy for development, staging, production, or feature branches.
- **Deployment Target**: Determine where you’ll deploy—cloud provider, on-premise, or hybrid.
- **Compliance**: Include any compliance requirements like SOC2, ISO 27001, or other industry standards.

## Current State
- **Existing Infrastructure**: Describe what your current setup looks like.
- **Deployment Process**: Outline how you currently handle deployments.
- **Pain Points**: Identify any issues you face in your current setup.
- **Team Size**: Share the size of your team and their skill levels.

## Pipeline Design

### 1. Source Control Strategy
- **Branching Model**: Choose between options like GitFlow or GitHub Flow.
- **Code Review Process**: Define the pull request or merge request requirements.
- **Branch Protection**: Set the rules for branch protection.

### 2. Build Strategy
- **Build Triggers**: Specify when builds should occur.
- **Build Environment**: Decide if you’ll use a containerized or native environment.
- **Artifact Management**: Determine where you will store your builds.

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

- **Secret Management**: Describe how you handle secrets.
- **Access Control**: Specify who can deploy what.
- **Network Security**: Outline your network policies.
- **Image Scanning**: Include details on vulnerability scanning.

### Environment Management

#### Development
- **Purpose**: Explain the purpose of the development environment.
- **Configuration**: Share dev-specific configurations.
- **Data**: Discuss your strategy for test data.

#### Staging
- **Purpose**: Define what staging is used for.
- **Configuration**: Outline staging configurations.
- **Testing**: List tests you run in staging.

#### Production
- **Purpose**: Describe the production environment's purpose.
- **Configuration**: Define production configurations.
- **Monitoring**: Explain how you monitor production.

### Rollback Strategy
```bash
# Rollback procedures
[ROLLBACK COMMANDS AND PROCEDURES]
```

### Performance Optimization
- **Build Optimization**: Share strategies for faster builds.
- **Deployment Speed**: Discuss methods for quick deployments.
- **Resource Efficiency**: Highlight how you manage resources.

## Success Criteria
- The pipeline runs successfully from start to finish.
- Deployment time is reduced by [X]%.
- Achieve zero-downtime deployments.
- Integrate security scans.
- Ensure monitoring and alerting are functional.