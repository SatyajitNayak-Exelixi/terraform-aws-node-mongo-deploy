# terraform-aws-node-mongo-deploy
# Node.js + MongoDB on AWS ECS (EC2)

**Region:** us-east-1  
**MongoDB:** Self-managed on EC2

## What this repo contains
- `app/` — Node.js application and Dockerfile
- `terraform/` — Terraform code (root + modules)
  - Modules: `network`, `ecr`, `alb`, `mongo`, `ecs_ec2`
- `ecs-ec2-vs-fargate.md` — comparison doc

## Prerequisites
- AWS account & credentials configured locally (`aws configure`) or via env vars
- Terraform v1.2+
- Docker
- An S3 bucket and DynamoDB table for Terraform state locking (or create with Terraform bootstrap). Bucket and table names must be unique.

> For this example, set `tfstate_bucket` and `tfstate_lock_table` variables in `terraform/variables.tf` or pass them via CLI.

## Build & push Docker image to ECR
1. Build locally:
```bash
cd app
docker build -t devops-tech-test-app:latest .
