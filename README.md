# GitHub Actions — From Fundamentals to Real-World DevOps

## About This Repository

This repository documents my journey of learning GitHub Actions, from fundamental concepts to building real-world CI/CD pipelines.

My goal is to understand not only how to write GitHub Actions workflows, but also how they work internally, how to troubleshoot failures, and how they integrate with tools used in real DevOps environments.

The focus is on hands-on implementation, practical use cases, and production-oriented practices.

## Learning Objectives

- Understand GitHub Actions architecture and workflow execution.
- Learn YAML syntax and workflow configuration.
- Automate application builds, tests, and quality checks.
- Build and publish Docker images.
- Integrate GitHub Actions with AWS and Terraform.
- Automate deployments to Kubernetes using Helm.
- Implement secure authentication and secret management.
- Learn workflow debugging, optimization, and failure recovery.
- Understand CI/CD design decisions used in real-world projects.


## Learning Roadmap

### 01. GitHub Actions Fundamentals

- Introduction to GitHub Actions
- What is GitHub Actions?
- Continuous Integration vs Continuous Delivery vs Continuous Deployment
- GitHub Actions vs Jenkins

### 02. Workflow Basics

- Workflow files
- Events and triggers
- Jobs and steps
- Actions and `uses`
- GitHub-hosted and self-hosted runners

### 03. Workflow Syntax

- YAML fundamentals
- Workflow syntax
- Environment variables
- Contexts and expressions
- Conditions and status checks

### 04. Workflow Control

- Job dependencies and `needs`
- Job outputs
- Artifacts
- Dependency caching
- Matrix strategies
- Reusable workflows

### 05. Security

- Secrets and variables
- `GITHUB_TOKEN` and permissions
- Least-privilege access
- OpenID Connect (OIDC)
- Secure third-party actions
- Environment protection rules

### 06. Docker CI/CD

- Build and test Docker images
- Docker image tagging and versioning
- Push images to container registries
- GitHub Container Registry (GHCR)
- Amazon Elastic Container Registry (ECR)
- Image scanning and build optimization

### 07. Deployment

- Deployment environments
- Approval gates
- Deploy to AWS
- Deploy to Kubernetes
- Helm-based deployments
- Health checks and rollback strategies

### 08. Advanced GitHub Actions

- Composite actions
- Custom actions
- Self-hosted runners
- Workflow debugging
- Workflow optimization
- Release automation

### 09. Real-World DevOps Project

Build an automated application delivery pipeline that combines:

- Git and GitHub for source control
- GitHub Actions for CI/CD automation
- Docker for application packaging
- Terraform for infrastructure provisioning
- AWS for cloud infrastructure
- Kubernetes and Helm for application deployment
- Prometheus and Grafana for monitoring

The project will be developed incrementally, starting with a simple workflow and adding integrations as the underlying concepts are understood.


## Practical Approach

The examples in this repository are intended for learning and experimentation.

Before using workflows in production, review permissions, protect credentials, validate infrastructure changes, and introduce appropriate deployment approvals.

Cloud resources and managed runners may incur costs. Hands-on exercises should use suitable permissions and cost controls.

## Official Resources

- [GitHub Actions Documentation](https://docs.github.com/en/actions)
- [GitHub Actions Workflow Syntax](https://docs.github.com/en/actions/reference/workflows-and-actions/workflow-syntax)
- [GitHub Actions Security](https://docs.github.com/en/actions/security-for-github-actions)
- [GitHub Actions Starter Workflows](https://github.com/actions/starter-workflows)

## Goal

The goal of this repository is to develop a practical understanding of GitHub Actions and build secure, maintainable, and reliable CI/CD pipelines that reflect real-world DevOps engineering practices.