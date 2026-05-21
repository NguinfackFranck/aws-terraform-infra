☁️ AWS Cloud Infrastructure – Terraform IaC

Course: Cloud Programming | IU International University of Applied Sciences
Author: Nguinfack Franck-Styve

A production-grade, secure, and highly available cloud infrastructure deployed on Amazon Web Services, fully provisioned using modular Terraform (Infrastructure as Code).

🎯 Project Overview
This project designs and deploys a complete AWS infrastructure for hosting a static web application, built with the following goals:
GoalImplementationHigh AvailabilityMulti-AZ deployment with Auto Scaling GroupsLow LatencyAmazon CloudFront CDN at global edge locationsSecurityPrivate subnets, Security Groups, IAM rolesAutomationFully automated via Terraform modules

🏗️ Architecture Overview
<img width="980" height="714" alt="image" src="https://github.com/user-attachments/assets/f869d7ea-29f2-4a90-8dda-3d31ee592237" />



🔧 AWS Services Used

Amazon EC2 – Compute instances in private subnets within an Auto Scaling Group
Application Load Balancer (ALB) – Distributes traffic across AZs from public subnets
Amazon CloudFront – Global CDN caching content at edge locations worldwide
Amazon Route 53 – DNS with latency-based routing and Alias records to CloudFront
NAT Gateway – Secure outbound internet access for private EC2 instances
Amazon CloudWatch – Metrics, alarms, and auto-scaling triggers
IAM Roles & Policies – Least-privilege access control across all resources


🌐 Networking Setup

Component	         CIDR / Details
VPC	                10.0.0.0/16
Public Subnet A	    10.0.1.0/24 (us-east-2a)
Public Subnet B	    10.0.3.0/24 (us-east-2b)
Private Subnet	    10.0.2.0/24 (us-east-2a)
Internet Gateway    Attached to VPC for ALB public access
NAT Gateway	Private   subnet outbound access

🔒 Security Design

Subnet Isolation – EC2 instances live exclusively in private subnets; only ALBs are internet-facing
Security Groups – ALBs accept HTTP/HTTPS; EC2 only accepts traffic from ALBs
NAT Gateway – Instances access internet for updates without exposing private IPs
IAM Roles – Principle of least privilege enforced across all resources


📦 Terraform Modular Structure
terraform/
├── modules/
│   ├── network/        # VPC, subnets, route tables, gateways
│   ├── compute/        # ASG, EC2, security groups
│   ├── load_balancing/ # ALB, target groups, listeners
│   └── cloudfront_dns/ # CloudFront distribution, Route 53 records
├── main.tf
├── variables.tf
└── outputs.tf
Each module is independently reusable, testable, and updatable.

🚀 How to Deploy
bash# 1. Configure AWS credentials
aws configure

# 2. Initialise Terraform
terraform init

# 3. Preview changes
terraform plan

# 4. Apply infrastructure
terraform apply

# 5. Destroy when done
terraform destroy

📈 Monitoring & Auto Scaling

CloudWatch Alarms – Trigger on CPU utilization, network traffic, and latency thresholds
ASG Scaling Policies – Automatically adds/removes EC2 instances based on demand
Health Checks – ALB health checks automatically replace unhealthy instances


🛠️ Tech Stack
AWS Terraform EC2 ALB CloudFront Route 53 CloudWatch NAT Gateway IAM Auto Scaling
