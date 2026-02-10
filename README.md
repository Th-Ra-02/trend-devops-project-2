CI/CD Pipeline for Web Application Deployment on AWS EKS

Overview:
This project demonstrates a complete DevOps CI/CD workflow using Jenkins, Docker, Kubernetes (Amazon EKS), Terraform, and AWS CloudWatch. The goal is to automate infrastructure provisioning, application deployment, and monitoring using cloud-native tools.

Objectives:
Provision AWS infrastructure using Terraform
Build and containerize the application using Docker
Automate CI/CD using Jenkins
Deploy the application on Amazon EKS
Monitor infrastructure and application using CloudWatch

Tools & Technologies:
Cloud: AWS
IaC: Terraform
CI/CD: Jenkins
Containerization: Docker
Orchestration: Kubernetes (EKS)
Monitoring: AWS CloudWatch
SCM: GitHub
Registry: DockerHub

Architecture Flow:
Code pushed to GitHub
Jenkins pipeline triggers automatically
Docker image is built and pushed to DockerHub
Kubernetes deploys image to EKS
Application exposed via LoadBalancer
Metrics monitored using CloudWatch

CI/CD Pipeline
Stages:
Source code checkout
Docker image build
Docker image push
Secrets are managed using Jenkins Credentials Manager.
Kubernetes Deployment
Deployment: Runs the containerized application
Service: LoadBalancer exposes the application publicly

Verification:
kubectl get pods
kubectl get svc

Monitoring:
EC2 (Jenkins) metrics: CPU & network
EKS node and cluster metrics
Monitoring implemented using AWS CloudWatch

Security:
IAM roles used instead of static credentials
Jenkins secrets stored securely
Kubernetes RBAC configured
Infrastructure managed via Terraform

Outcome:
Automated CI/CD pipeline implemented successfully
Application deployed on AWS EKS
Public access via LoadBalancer
Monitoring enabled using CloudWatch
