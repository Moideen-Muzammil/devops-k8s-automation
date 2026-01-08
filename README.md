# DevOps Kubernetes Automation

## Overview

This project demonstrates an end-to-end DevOps workflow for deploying a simple web application to a managed Kubernetes cluster using modern DevOps practices.

The solution automates infrastructure provisioning, containerization, deployment, and continuous delivery using **AWS, Terraform, Docker, Kubernetes (EKS), and GitHub Actions**.  
A simple **Hello World** web application is automatically built and deployed whenever changes are pushed to the `main` branch.

---

## Architecture & Design Choices

- **Cloud Provider:** AWS
- **Kubernetes Platform:** Amazon EKS (managed Kubernetes service)
- **Infrastructure as Code:** Terraform
- **Container Registry:** Amazon ECR
- **CI/CD Tool:** GitHub Actions
- **Web Server:** Nginx

### Key Design Decisions

- **Terraform** is used to provision the EKS cluster in a reproducible and version-controlled manner.
- **Amazon EKS** is chosen to avoid manual Kubernetes control-plane management.
- **Docker** is used to package the application into a lightweight container image.
- **GitHub Actions** provides automated CI/CD triggered on every push to the `main` branch.
- **Kubernetes Service of type LoadBalancer** is used to expose the application publicly via an AWS-managed Elastic Load Balancer.
- **Secrets and credentials** are handled securely using GitHub Secrets.

---

## Repository Structure

```
.
├── .github/workflows/ # GitHub Actions CI/CD pipeline
│ └── deploy.yaml
├── app/ # Application source
│ └── index.html
├── k8s/ # Kubernetes manifests
│ ├── deployment.yaml
│ └── service.yaml
├── terraform/ # Terraform code to provision EKS
│ ├── main.tf
│ ├── variables.tf
│ ├── outputs.tf
│ └── .terraform.lock.hcl
├── Dockerfile # Docker image definition
├── .gitignore
└── README.md
```


---


## How to Run the Project

### 1. Infrastructure Provisioning (Terraform)

```bash
cd terraform
terraform init
terraform apply
```

This provisions:

* Amazon EKS cluster
* Managed worker node group
* Required networking resources

## CI/CD Pipeline (Automated Deployment)

The CI/CD pipeline is automatically triggered on every push to the main branch.

Pipeline steps:
* Checkout source code
* Authenticate to AWS using GitHub Secrets
* Build Docker image
* Push Docker image to Amazon ECR
* Update kubeconfig for Amazon EKS
* Deploy application using Kubernetes manifests

No manual deployment steps are required after the pipeline is configured.


## Live Application URL

The application is publicly accessible via an AWS LoadBalancer: http://a76974f2db45942dfb4360e9be46f36a-1763358169.us-east-1.elb.amazonaws.com


## Summary

This project showcases a complete DevOps automation workflow including:
* Infrastructure as Code
* Containerization
* Kubernetes orchestration
* Secure CI/CD automation
* Cloud-native deployment

It demonstrates how modern DevOps tools can be combined to deliver scalable, repeatable, and production-ready application deployments.
