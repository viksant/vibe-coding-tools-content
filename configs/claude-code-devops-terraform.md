---
title: "Claude Code DevOps Terraform"
description: "Streamlines Infrastructure as Code with Terraform for AWS/Azure provisioning and CI/CD pipelines."
category: "configuration"
tags: ["claude-code", "devops", "terraform", "infrastructure", "aws", "azure", "cicd", "kubernetes", "docker", "github-actions"]
tech_stack: ["terraform", "aws", "azure", "kubernetes", "docker", "github-actions"]
---

This configuration streamlines Infrastructure as Code with Terraform for AWS/Azure provisioning and CI/CD pipelines.

### Configuration Overview
This setup provides a complete DevOps infrastructure configuration using Terraform for provisioning cloud resources on AWS and Azure, managing Kubernetes clusters, containerizing applications with Docker, and automating CI/CD pipelines with GitHub Actions.

### Prerequisites
- **Terraform**: Version 1.0 or higher
- **AWS CLI**: Version 2.x
- **Azure CLI**: Version 2.x
- **Docker**: Version 20.x or higher
- **kubectl**: Version compatible with your Kubernetes cluster
- **GitHub Account**: For CI/CD integration
- **Node.js**: Version 14.x or higher (if using Node.js applications)

### Installation & Setup
1. **Install Terraform**:
   - Download Terraform from the [official site](https://www.terraform.io/downloads.html) and follow the installation instructions.
   - Verify installation: 
     ```bash
     terraform -version
     ```

2. **Install AWS CLI**:
   - Follow the installation guide on the [AWS CLI documentation](https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html).
   - Configure AWS credentials:
     ```bash
     aws configure
     ```

3. **Install Azure CLI**:
   - Follow the installation instructions from the [Azure CLI documentation](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli).
   - Log in to your Azure account:
     ```bash
     az login
     ```

4. **Install Docker**:
   - Follow the installation guide on the [Docker website](https://docs.docker.com/get-docker/).
   - Verify installation:
     ```bash
     docker --version
     ```

5. **Install kubectl**:
   - Follow the installation instructions from the [Kubernetes documentation](https://kubernetes.io/docs/tasks/tools/install-kubectl/).

6. **Set Up GitHub Actions**:
   - Create a new repository on GitHub for your project.
   - Add a `.github/workflows/ci.yml` file for CI/CD configuration.

### File Structure
```
project-root/
├── terraform/
│   ├── main.tf
│   ├── variables.tf
│   ├── outputs.tf
│   └── provider.tf
├── kubernetes/
│   ├── deployment.yaml
│   └── service.yaml
├── docker/
│   ├── Dockerfile
│   └── .dockerignore
└── .github/
    └── workflows/
        └── ci.yml
```

### Key Configuration Files
- **`main.tf`**: Main Terraform configuration file.
  ```hcl
  provider "aws" {
    region = var.aws_region
  }

  resource "aws_instance" "app" {
    ami           = var.ami_id
    instance_type = "t2.micro"
  }
  ```

- **`variables.tf`**: Define variables used in Terraform.
  ```hcl
  variable "aws_region" {
    description = "AWS region"
    default     = "us-east-1"
  }

  variable "ami_id" {
    description = "AMI ID for the instance"
    type        = string
  }
  ```

- **`outputs.tf`**: Outputs from Terraform.
  ```hcl
  output "instance_id" {
    value = aws_instance.app.id
  }
  ```

- **`Dockerfile`**: Docker configuration for your application.
  ```dockerfile
  FROM node:14
  WORKDIR /app
  COPY package*.json ./
  RUN npm install
  COPY . .
  CMD ["npm", "start"]
  ```

- **`.github/workflows/ci.yml`**: GitHub Actions CI/CD configuration.
  ```yaml
  name: CI

  on:
    push:
      branches:
        - main

  jobs:
    build:
      runs-on: ubuntu-latest
      steps:
        - name: Checkout code
          uses: actions/checkout@v2
        - name: Set up Docker Buildx
          uses: docker/setup-buildx-action@v1
        - name: Build and push Docker image
          uses: docker/build-push-action@v2
          with:
            context: .
            push: true
            tags: user/app:latest
  ```

### Advanced Options
- **Terraform Backend**: Use remote state storage (e.g., S3 or Azure Blob Storage) for better collaboration.
- **Docker Multi-Stage Builds**: Optimize Docker images by using multi-stage builds to reduce image size.
- **Kubernetes Helm Charts**: Use Helm for managing Kubernetes applications for easier deployments and versioning.

### Troubleshooting
- **Terraform Initialization Issues**: Run `terraform init` to ensure all providers and modules are downloaded.
- **AWS CLI Errors**: Check your AWS credentials and permissions. Ensure the IAM user has the necessary policies attached.
- **Docker Build Failures**: Ensure Docker daemon is running and check for syntax errors in the `Dockerfile`.

### Best Practices
- **Version Control**: Use Git for version control of all configuration files.
- **Environment Variables**: Store sensitive information (like API keys) in environment variables or use a secrets manager.
- **Modular Terraform**: Break down Terraform configurations into modules for better organization and reusability.
- **Regular Updates**: Keep all tools and dependencies updated to the latest stable versions for security and performance improvements.

### Performance Optimizations
- **Terraform State Management**: Use state locking and versioning to prevent conflicts during concurrent operations.
- **Docker Caching**: Leverage Docker layer caching to speed up build times by minimizing changes in the `Dockerfile`.
- **Kubernetes Resource Requests**: Define resource requests and limits for containers to optimize resource allocation in the cluster.