# React App Deployment with Three-Tier Architecture on AWS

This project demonstrates the deployment of a React-based web application using a secure and scalable **three-tier architecture** on AWS, integrated with a **CI/CD pipeline** for continuous delivery.

---

## 📌 Architecture Overview

The architecture is split into three distinct tiers:

1. **Frontend (Presentation Tier)**  
   - React app served via NGINX  
   - Hosted in a **public subnet**

2. **Application Tier**  
   - Node.js/Express backend  
   - Hosted in **private subnet 1**

3. **Data Tier**  
   - MongoDB database  
   - Hosted in **private subnet 2**

---

## 🎯 Objectives

- Implement secure VPC with one public and two private subnets
- Deploy frontend in the public subnet via NGINX on Ubuntu EC2
- Host backend in private subnet 1 (internal access only)
- Deploy MongoDB in private subnet 2 (backend-only access)
- Configure automated CI/CD pipeline using:
  - AWS CodePipeline
  - AWS CodeBuild
  - AWS CodeDeploy

---

## 🗺️ Network Design (VPC)

- VPC CIDR: `10.0.0.0/16`
  - Public Subnet: `10.0.1.0/24`
  - Private Subnet 1: `10.0.2.0/24`
  - Private Subnet 2: `10.0.3.0/24`
- NAT Gateway: In public subnet
- Internet Gateway: Attached to VPC
- Route Tables: Properly configured and associated

---

## 🛠️ Configuration Details

### Frontend (Public Subnet)
- EC2 Ubuntu instance with NGINX and React build
- NGINX reverse proxy to route `/api` to backend

### Application Tier (Private Subnet 1)
- Node.js backend running on PM2
- Access restricted to frontend instance

### Database Tier (Private Subnet 2)
- MongoDB installed and secured
- Access restricted to backend instance

---

## 🔐 Security Group Rules

| Component          | Source IP       |
|-------------------|-----------------|
| Frontend (Public) | `0.0.0.0/0`      |
| Frontend (Private)| `10.0.2.214/32`  |
| Backend & DB      | `10.0.3.122/32`  |

---

## 🚀 CI/CD Pipeline

### Pipeline Stages

1. **Source**: GitHub integration with CodePipeline  
2. **Build**: CodeBuild runs tests and builds artifacts  
3. **Deploy**: CodeDeploy deploys frontend to public subnet and backend to private subnet  

---

## ✅ Deployment Verification

- Access the frontend via public IP/domain
- Frontend communicates with backend via `/api`
- Backend securely interacts with the database

---

## 📌 Conclusion

This setup ensures:
- Network isolation and tier separation
- Automated, reliable deployment through CI/CD
- Scalable and maintainable architecture on AWS

---

## 📁 Tech Stack

- React, Node.js, MongoDB
- AWS EC2, VPC, CodePipeline, CodeBuild, CodeDeploy, NGINX, PM2

---

## 📄 License

This project is licensed under the MIT License.
