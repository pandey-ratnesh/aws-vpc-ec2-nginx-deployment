# Secure Web Application Deployment on AWS (Custom VPC + EC2 + S3)

A cloud infrastructure project demonstrating network isolation, least-privilege access, and static web serving using Nginx on an AWS EC2 instance integrated with Amazon S3.

## Architecture Overview
- **VPC & Networking**: Custom VPC (`10.0.0.0/16`), isolated public subnet, custom Route Table pointing `0.0.0.0/0` to an Internet Gateway.
- **Compute**: AWS EC2 t3.micro running Ubuntu 24.04 LTS.
- **Web Server**: Nginx configured to host static web content from `/var/www/html/`.
- **Security & IAM**:
  - Security Groups restricting inbound ingress to SSH (22) and HTTP (80).
  - IAM Instance Profile (`EC2-S3-ReadOnly-Role`) granting temporary credentials for Amazon S3 read operations without long-lived secret keys.
- **Storage**: Private Amazon S3 bucket for decoupling asset management from the compute layer.

## Key Troubleshooting Highlights
- Diagnosed and resolved asymmetric network reachability by debugging Route Table target associations and Security Group rule states[cite: 13, 15].
- Enforced credential-free AWS CLI authorization using IAM Instance Profiles.
