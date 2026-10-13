# Securing CI/CD Pipeline with Automated Security Monitoring for Kubernetes-Hosted Applications

This repository contains the DevSecOps project implementation for **ShopPro Online** (an e-commerce platform). It demonstrates a secure, production-grade CI/CD pipeline that automates microservice deployment on Amazon EKS with integrated security testing at every stage of the pipeline.

---

## 🎯 Objective
To automate application deployment to Amazon EKS while shifting security left—detecting container vulnerabilities, code issues, and compliance misconfigurations before code reaches production.

---

## 🛠️ Tech Stack & Tools
- **Cloud & Orchestration:** Amazon EKS, AWS ECR, AWS VPC, IAM Roles for Service Accounts (IRSA)
- **CI/CD:** GitHub Actions
- **Containerization:** Docker
- **Security Scanning:** Snyk (SAST & SCA), Trivy (Container Vulnerability Scanning)
- **Monitoring & Compliance:** AWS Security Hub, AWS CloudTrail, AWS CloudWatch, Pod Security Standards

---

## 📁 Repository Structure
```text
.
├── .github/
│   └── workflows/
│       └── ci-cd.yml      # CI/CD Pipeline with integrated Snyk & Trivy scans
├── k8s/
│   └── deployment.yaml    # Kubernetes manifests with non-root security context
├── Dockerfile             # Multi-stage Docker build using non-root user
├── package.json           # Node.js dependencies
└── app.js                 # Sample microservice application

⚡ Key Pipeline Stages
Source Code & Dependency Scanning: Snyk scans the repository for SAST and SCA vulnerabilities on code commit.

Container Security: Docker image is built and scanned with Trivy before pushing to Amazon ECR. Pipeline breaks if high/critical vulnerabilities are found.

Automated EKS Deployment: Authenticates securely with AWS, updates kubeconfig, and deploys the application onto Amazon EKS.

Least Privilege Access: Workloads run under specific IAM Roles for Service Accounts (IRSA) and Kubernetes Pod Security Standards.

Continuous Audit: Operations and API activity are logged via CloudTrail and monitored through AWS CloudWatch.

🔑 Setup Instructions (GitHub Secrets)
To execute the pipeline, configure the following secrets in Settings > Secrets and variables > Actions:

AWS_ACCESS_KEY_ID: AWS IAM access key with deployment permissions

AWS_SECRET_ACCESS_KEY: AWS IAM secret key

SNYK_TOKEN: Snyk API authentication token
