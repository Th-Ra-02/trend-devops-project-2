Guvi Project 2 (trend-app)
CI/CD with EKS, Jenkins and Terraform 

This project demonstrates a complete DevOps CI/CD pipeline where a web application is containerized using Docker, deployed to Amazon EKS, and automated using Jenkins, with all infrastructure provisioned via Terraform.

** The goal is to show:
Infrastructure as Code (IaC)
Containerization
CI/CD automation
Kubernetes deployment on AWS

** Infrastructure Architecture:
Terraform provisions the following resources:
VPC
Public subnets
Internet Gateway
Amazon EKS
Managed Kubernetes cluster
Managed node group
EC2 Instance
Jenkins server
Configured with IAM role to access EKS
IAM Roles & Policies
Jenkins EC2 → EKS access
Security Groups
Jenkins: SSH (22), Jenkins UI (8080)
Application LoadBalancer is Created automatically by Kubernetes Service

** Tools & Technologies Used:
Terraform – Infrastructure provisioning
AWS EKS – Kubernetes cluster
Docker – Application containerization
Jenkins – CI/CD automation
Kubernetes – Application orchestration
AWS CLI v2 and kubectl

** Repository Structure
--dist/
--tf/
---main.tf
--k8s/
---deployment.yaml
---service.yaml
-Dockerfile
-Jenkinsfile
-README.md

** Infrastructure Setup (commands to be used in the tf folder)
terraform init (to initialize terraform)
terraform validate (to validate the configuration)
terraform plan (shows all the aws services to be used)
terraform apply (starts all the aws services {may take 10 - 20 mins})

* Terraform outputs:
EKS cluster name
EKS endpoint
Jenkins public IP
Access Jenkins using http://<jenkins_public_ip>:8080

* Install required plugins:
Docker Pipeline
Git
Kubernetes CLI

* Configure credentials:
DockerHub credentials
AWS IAM Role (attached to EC2)

* CI/CD Pipeline Flow
The Jenkins pipeline performs the following steps:
Checkout Code
Build Docker Image
Push Image to DockerHub
Deploy Application to EKS
Pipeline definition is stored in Jenkinsfile.

* Kubernetes Deployment:
Kubernetes manifests are located in the k8s/ directory:
Deployment
Runs the application container on port 3000
Service
Type: LoadBalancer
Exposes application externally via AWS ELB
Apply manually using 'kubectl apply -f k8s/'

* Application Verification
Get service endpoint using 'kubectl get svc'

* Access the application using 'http://<EXTERNAL-LOADBALANCER-DNS>'
If the webpage loads successfully, deployment is complete.

** Project Outcome:
Infrastructure created using Terraform
Jenkins automates Docker build and deployment
Application runs on EKS and is publicly accessible
End-to-end DevOps workflow achieved

* Notes:
Jenkins EC2 instance assumes IAM role for EKS access (no static AWS keys)
kubectl access is managed via AWS CLI v2
LoadBalancer service handles external traffic
