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

## Day 3 — Linux Administration on EC2 Instance

### Environment Context
Performed administrative operations on a live Ubuntu EC2 instance to strengthen production-level Linux fundamentals within a cloud environment.

---

### User & Access Management

- Created a new system user (`devuser`)
- Granted sudo privileges for controlled administrative access
- Switched between users to validate permission boundaries
- Avoided direct root usage to follow production best practices

#### Engineering Insight
Modern production systems enforce privilege separation. Working through controlled sudo access reduces risk and improves auditability.

---

### File Permissions & Ownership

- Created test files and inspected permissions using `ls -l`
- Modified permissions using `chmod`
- Applied `chmod 700` to restrict file access to owner only
- Updated file ownership using `chown user:group`

#### Technical Observation
Validated Linux permission model (user/group/others) and observed how restrictive permissions prevent unauthorized access.

---

### Linux Security Model Exploration

- Encountered `Permission denied` while accessing restricted directories
- Used `sudo` to elevate privileges appropriately
- Observed default home directory protection mechanisms

#### Root Cause Understanding
Linux enforces access control at the file system level, preventing cross-user access unless explicitly permitted.

---

### Service Management (systemd)

Managed nginx service using `systemctl`:

- Checked service status
- Stopped service
- Restarted service
- Verified service state

#### Operational Understanding
Validated how services are controlled in Linux production systems using systemd. Confirmed that web availability depends on service health.

---

### Log Analysis

- Navigated to `/var/log/nginx`
- Inspected `access.log` to verify inbound HTTP traffic
- Observed real client requests hitting the EC2 instance

#### Operational Insight
Logs serve as primary debugging and monitoring mechanism in production environments.

---

### Outcome

Established foundational Linux administration capabilities including:
- User management
- Permission handling
- Service lifecycle control
- Log inspection
- Security boundary validation

These are core competencies required for DevOps and infrastructure operations roles.

---

---

## Day 4 — Amazon S3 & Static Website Hosting

### Service Overview
Implemented object storage and static website hosting using Amazon S3 to understand cloud storage architecture and public content delivery.

---

### S3 Bucket Provisioning

- Created General Purpose S3 bucket in **ap-south-1 (Mumbai)**
- Reviewed global bucket naming requirements
- Understood region selection and data locality considerations

#### Engineering Insight
S3 is a globally distributed object storage service commonly used for application assets, backups, logs and static site hosting.

---

### Public Access Configuration

- Disabled default *Block Public Access* configuration
- Implemented **Bucket Policy** allowing `s3:GetObject`
- Reviewed differences between:
  - Legacy ACLs
  - Bucket Policies (recommended approach)

#### Security Consideration
Access to S3 objects is denied by default. Explicit policies are required to safely expose public content.

---

### Object Storage Hands-On

- Uploaded image and text files
- Generated public object URLs
- Verified accessibility from the internet

#### Validation
Confirmed that objects can be accessed publicly only when policy permissions allow read access.

---

### Static Website Hosting

- Enabled **Static Website Hosting** feature
- Deployed basic `index.html`
- Accessed site using S3 website endpoint

#### Operational Understanding
Validated how S3 can host static front-end applications without requiring a traditional web server.

---

### Outcome

Successfully implemented:
- Cloud object storage
- Public access policy configuration
- Static website hosting using S3

This workflow mirrors real-world usage in CI/CD pipelines and front-end deployments.



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
