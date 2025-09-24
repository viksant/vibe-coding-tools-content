---
title: "Claude Code DevOps Terraform"
description: "Streamlines Infrastructure as Code with Terraform for AWS/Azure provisioning and CI/CD pipelines."
category: "configuration"
tags: ["claude-code", "devops", "terraform", "infrastructure", "aws", "azure", "cicd", "kubernetes", "docker", "github-actions"]
tech_stack: ["terraform", "aws", "azure", "kubernetes", "docker", "github-actions"]
---

This setup simplifies Infrastructure as Code using Terraform for provisioning resources in AWS and Azure, along with managing CI/CD pipelines.

### Configuration Overview
This configuration gives you a complete DevOps infrastructure using Terraform to provision cloud resources on AWS and Azure. It helps you manage Kubernetes clusters, package applications with Docker, and automate CI/CD pipelines using GitHub Actions.

### Prerequisites
Before you start, make sure you have the following installed:
- **Terraform**: Version 1.0 or higher
- **AWS CLI**: Version 2.x
- **Azure CLI**: Version 2.x
- **Docker**: Version 20.x or higher
- **kubectl**: Version that matches your Kubernetes cluster
- **GitHub Account**: Needed for CI/CD integration
- **Node.js**: Version 14.x or higher if your application uses Node.js

### Installation & Setup
1. **Install Terraform**:
   - Download Terraform from the [official site](https://www.terraform.io/downloads.html) and follow the installation instructions.
   - Confirm the installation by running:
     ```bash
     terraform -version
     ```

2. **Install AWS CLI**:
   - Follow the guide on the [AWS CLI documentation](https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html).
   - Set up your AWS credentials with:
     ```bash
     aws configure
     ```

3. **Install Azure CLI**:
   - Check the installation instructions in the [Azure CLI documentation](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli).
   - Log into your Azure account using:
     ```bash
     az login
     ```

4. **Install Docker**:
   - Follow the guide on the [Docker website](https://docs.docker.com/get-docker/).
   - Verify the installation by running:
     ```bash
     docker --version
     ```

5. **Install kubectl**:
   - Follow the installation instructions from the [Kubernetes documentation](https://kubernetes.io/docs/tasks/tools/install-kubectl/).

6. **Set Up GitHub Actions**:
   - Create a new repository on GitHub for your project.
   - Add a `.github/workflows/ci.yml` file to configure CI/CD.

### File Structure
Here's an example of how your project directory should look:
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
- **`main.tf`**: This is your main Terraform configuration file.
  ```hcl
  provider "aws" {
    region = var.aws_region
  }

  resource "aws_instance" "app" {
    ami           = var.ami_id
    instance_type = "t2.micro"
  }
  ```

- **`variables.tf`**: This file defines the variables used in Terraform.
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

- **`outputs.tf`**: This file specifies the outputs from Terraform.
  ```hcl
  output "instance_id" {
    value = aws_instance.app.id
  }
  ```

- **`Dockerfile`**: This is the Docker configuration for your application.
  ```dockerfile
  FROM node:14
  WORKDIR /app
  COPY package*.json ./
  RUN npm install
  COPY . .
  CMD ["npm", "start"]
  ```

- **`.github/workflows/ci.yml`**: This file configures GitHub Actions for CI/CD.
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
Here are some options to enhance your setup:
- **Terraform Backend**: Use remote state storage like S3 or Azure Blob Storage for better collaboration.
- **Docker Multi-Stage Builds**: Optimize your Docker images by employing multi-stage builds to reduce their size.
- **Kubernetes Helm Charts**: Utilize Helm for managing Kubernetes applications to simplify deployments and versioning.

### Troubleshooting
If you encounter issues, try the following:
- **Terraform Initialization Issues**: Run `terraform init` to ensure all providers and modules are downloaded.
- **AWS CLI Errors**: Check your AWS credentials and permissions. Make sure your IAM user has the needed policies.
- **Docker Build Failures**: Ensure that the Docker daemon is running and look for syntax errors in your `Dockerfile`.

### Best Practices
Keep these tips in mind:
- **Version Control**: Use Git to manage version control for all your configuration files.
- **Environment Variables**: Secure sensitive information like API keys by using environment variables or a secrets manager.
- **Modular Terraform**: Organize your Terraform configurations into modules for better structure and reusability.
- **Regular Updates**: Keep your tools and dependencies up to date to enhance security and performance.

### Performance Optimizations
Consider these strategies:
- **Terraform State Management**: Use state locking and versioning to avoid conflicts during concurrent operations.
- **Docker Caching**: Take advantage of Docker layer caching to speed up build times by minimizing changes in your `Dockerfile`.
- **Kubernetes Resource Requests**: Set resource requests and limits for containers to optimize resource allocation in your cluster.