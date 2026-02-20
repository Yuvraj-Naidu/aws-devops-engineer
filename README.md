# AWS DevOps Engineer ☁️🚀

Hands-on AWS and DevOps engineering implementations focused on cloud infrastructure, server management, networking, and deployment practices.

This repository documents practical infrastructure setups and real-world troubleshooting scenarios while building production-ready DevOps capabilities.

---

## 📅 Implementation Log

---

## Day 1 — AWS Account Foundation & Identity Management

### Infrastructure Setup
- Provisioned AWS account
- Created dedicated IAM Administrator user
- Enforced Multi-Factor Authentication (MFA)
- Reviewed AWS Regions and Availability Zones architecture

### Engineering Considerations
- Avoided daily use of root account for security best practices
- Implemented IAM-based access control model
- Understood regional isolation and high availability design principles

### Outcome
Established secure foundational cloud environment aligned with AWS best practices.

---

## Day 2 — EC2 Provisioning & Web Server Deployment

### Infrastructure Provisioned
- Launched Ubuntu EC2 instance
- Configured key pair authentication
- Connected via SSH securely
- Installed and configured Nginx web server

### Networking & Security Configuration
- Diagnosed initial website inaccessibility
- Identified Security Group inbound rule restriction
- Configured inbound rules:
  - SSH (Port 22)
  - HTTP (Port 80)

### Technical Challenge
The web server was running, but the application was not publicly accessible.

### Root Cause
Inbound HTTP traffic was blocked at the Security Group (AWS firewall) level.

### Resolution
Modified Security Group rules to allow HTTP traffic from 0.0.0.0/0.

### Outcome
Successfully hosted and accessed live web server using EC2 public IP.

---

## 🎯 Repository Objective

This repository will progressively demonstrate implementation of:

- Linux Administration
- AWS Infrastructure
- Networking & Firewalls
- Containerization (Docker)
- Infrastructure as Code (Terraform)
- CI/CD Pipelines
- Kubernetes Deployments
