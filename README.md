# 🚀 Nginx Deployment on AWS ECS (EC2 Launch Type) using Terraform

This project provisions a production-ready ECS cluster on EC2 launch type using Terraform. It includes a custom VPC, ALB, Auto Scaling Group, ECS Capacity Provider, EFS for persistent storage, CloudWatch Logs, and ECR integration for the custom Nginx image.

---

## 📦 Project Overview

The infrastructure includes:

- Custom VPC with public and private subnets across multiple AZs
- Internet Gateway and NAT Gateways for outbound access
- Route tables with public and private routing
- Security Groups for ALB, ECS tasks, EFS access
- ECS Cluster with EC2 launch type
- Auto Scaling Group and ECS Capacity Provider
- Application Load Balancer (ALB) with listeners and target groups
- EFS (Elastic File System) for persistent storage mounted in tasks
- CloudWatch Logs for container logging
- Amazon ECR for storing the custom Nginx Docker image
- IAM Roles and Policies for ECS tasks and EC2 instances

---

## 🖼 Architecture Diagram

![ecs_efs_ec2_private](https://github.com/user-attachments/assets/25daf4bf-80e0-43d8-b2ec-fb1ddae20b71)

---

## 🛠 Technologies Used

- **Terraform** for Infrastructure as Code
- **AWS ECS (EC2 launch type)**
- **AWS Auto Scaling** for managing EC2 instances
- **AWS ALB** for load balancing
- **AWS EFS** for persistent storage
- **AWS ECR** for container images
- **CloudWatch Logs** for logging
- **IAM Roles** for fine-grained permissions
- **Docker** for building custom images

---

## 📁 Project Structure

```bash
.
├── main.tf               # All infrastructure definitions
├── variables.tf          # Input variables
├── nginx-dockerfile/     # Custom NGINX image context
│   ├── Dockerfile
│   └── index.html
└── README.md             # Project documentation
```

---

## ⚙️ Deployment Notes

**IMPORTANT:**  
Before running `terraform apply`, make sure to replace the following placeholders in your code:

- `<aws_account_id>` with your AWS account ID
- `<region>` with your chosen AWS region (e.g. `us-east-2`)
- `<repo-name>` with your ECR repository name

These appear in:

- ECS Task Definition image URIs
- `aws ecr get-login-password` command in `null_resource`

---

## 🚀 Getting Started

### ✅ Prerequisites

- Terraform v1.x installed
- AWS CLI configured (`aws configure`)
- Docker installed and running
- Sufficient AWS permissions (IAM, ECS, EC2, ECR, VPC)

---

### ⚡ Deployment Steps

1. **Clone the repository**
   ```bash
   git clone https://github.com/AhmadMudassir/highly-available-ecs-ec2-infra.git
   cd highly-available-ecs-ec2-infra
   ```

2. **Initialize Terraform**
   ```bash
   terraform init
   ```

3. **Review the execution plan**
   ```bash
   terraform plan
   ```

4. **Apply the configuration**
   ```bash
   terraform apply
   ```

5. **Verify the deployment**
   - Go to the ECS console → Clusters → Services
   - Check that EC2 instances are registered and tasks are running
   - Confirm the ALB DNS name and test it in your browser

---

## 📝 Verifying EFS Integration

- Your ECS tasks mount EFS at `/mnt/efs`
- The EFS File System is automatically provisioned with mount targets in private subnets
- Verify mounts in container logs or via application access

---

## 🧹 Cleanup

To tear down **all** resources:

```bash
terraform destroy
```

---
