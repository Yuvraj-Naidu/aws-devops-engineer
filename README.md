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

## Day 5 — AWS Networking Fundamentals (VPC)

### Networking Context
Explored AWS Virtual Private Cloud (VPC) to understand how cloud networking enables secure and public access to EC2 instances.

---

### VPC Architecture Exploration

Reviewed the default AWS VPC and identified core networking components:

- Virtual Private Cloud (VPC)
- Subnets
- Route Tables
- Internet Gateway

#### Engineering Insight
VPC acts as an isolated virtual network where all AWS resources operate securely.

---

### Subnet & Routing Configuration

- Inspected subnet settings and **auto-assign public IP**
- Verified default route configuration:

`0.0.0.0/0 → Internet Gateway`

#### Technical Understanding
Route tables determine how network traffic flows inside and outside the VPC.

---

### Internet Connectivity Flow

Verified Internet Gateway attachment and mapped the full traffic path:

**Internet → Internet Gateway → Route Table → Public Subnet → EC2 → Security Group**

#### Architecture Insight
Public accessibility requires correct configuration across multiple networking layers, not just instance settings.

---

### Public vs Private Subnet Design

Studied production architecture best practices:

- **Public Subnet:** Web servers, Load balancers
- **Private Subnet:** Databases, internal services

#### Security Consideration
Sensitive services should never be directly exposed to the public internet.

---

### Outcome

Established foundational understanding of AWS networking, traffic routing and subnet design principles required for secure and scalable cloud architectures.

---

## Day 6 — Docker Runtime Deployment on EC2

### Environment

Configured Docker Engine on an Ubuntu-based EC2 instance to enable containerized workload execution within the existing cloud environment.

---

### Docker Engine Installation

- Installed Docker Engine packages
- Verified Docker service status via systemd
- Confirmed daemon responsiveness

#### Access Control Issue

Non-root user execution of Docker commands failed due to socket permission restrictions.

#### Remediation

- Added active user to `docker` group
- Reinitialized session to refresh group membership
- Validated non-sudo container execution

---

### Container Validation

- Pulled `hello-world` image from Docker Hub
- Executed container to confirm runtime functionality

Verified:
- Image retrieval
- Container creation
- Successful execution lifecycle

---

### Nginx Container Deployment

- Pulled official Nginx image
- Launched container with explicit port binding:

`Host Port 8080 → Container Port 80`

Validated:
- Container state
- Port exposure
- Service response via public IP

---

### Network Layer Adjustment

Updated EC2 Security Group configuration to allow inbound traffic on TCP 8080 to align with container port mapping.

---

### Operational Outcome

Successfully transitioned from host-level service deployment to containerized workload execution.

Confirmed external accessibility of containerized Nginx service over public network interface.

---

---

## Day 7 — Docker Container Lifecycle & Operational Debugging

### Operational Context

Focused on container lifecycle management and runtime observability within the EC2-hosted Docker environment.

---

### Container Lifecycle Management

- Enumerated active containers using `docker ps`
- Inspected all containers (including stopped) using `docker ps -a`
- Executed lifecycle commands:
  - `docker stop`
  - `docker start`
  - `docker restart`

#### Operational Understanding
Validated state transitions between running and exited containers. Confirmed that container processes are ephemeral and dependent on runtime state.

---

### Runtime Observability

- Inspected container output using `docker logs`
- Analyzed log stream for application behavior and runtime events

#### Engineering Insight
Container logs serve as primary debugging surface in containerized environments, especially when external logging systems are not configured.

---

### Interactive Container Access

- Accessed running container using `docker exec`
- Explored container filesystem structure
- Reviewed application-level configuration inside runtime environment

#### Technical Observation
Confirmed container isolation model — runtime environment is isolated from host while sharing kernel resources.

---

### Container Cleanup & Resource Management

- Stopped containers prior to removal
- Removed unused containers
- Observed distinction between:
  - Stopping a container (preserves state)
  - Removing a container (deletes runtime instance)

#### Operational Insight
Proper container lifecycle management prevents resource leakage and maintains host-level stability.

---

### Outcome

Established practical control over Docker container lifecycle, runtime debugging and cleanup operations — core operational competencies in container-based DevOps workflows.

---

---

## Day 8 — Docker Image Build & Custom Container Deployment

### Build Context

Implemented custom Docker image creation using a Dockerfile to package application content into a reusable container image.

---

### Dockerfile Implementation

- Created custom `index.html` web page
- Used official **nginx base image**
- Implemented Dockerfile to copy static content into container image

#### Engineering Insight
Dockerfile instructions create immutable image layers, enabling reproducible and versioned application builds.

---

### Image Build Process

- Built custom image using `docker build`
- Verified successful image creation and local image registry presence

#### Validation
Confirmed image availability using Docker image listing prior to deployment.

---

### Custom Container Deployment

- Stopped and removed previously running containers
- Deployed container from custom image
- Configured port binding:

`Host Port 8080 → Container Port 80`

---

### Connectivity Verification & Debugging

- Verified local container response using `curl localhost`
- Diagnosed external access path
- Confirmed Security Group alignment with exposed port

---

### Operational Outcome

Successfully packaged application content into a reusable Docker image and deployed it as a publicly accessible containerized web service.

This establishes the foundation for repeatable container-based deployments and future CI/CD automation.

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
