# Flask Application Deployment on Kubernetes (k3s) using AWS EC2

![Build Status](https://img.shields.io/badge/build-passing-brightgreen)
![Docker Image](https://img.shields.io/badge/docker-ready-blue)

## Project Overview

This project demonstrates how to containerize a simple Flask application and deploy it on a Kubernetes cluster (k3s) running on an AWS EC2 instance.

The goal is to showcase core DevOps concepts such as Docker, Kubernetes deployments, services, and application scaling — all in a cloud environment without relying on local machine admin privileges.

## Technologies Used

- **AWS EC2** – Cloud compute instance  
- **Ubuntu 22.04** – Server operating system  
- **Docker** – Containerization  
- **Kubernetes (k3s)** – Container orchestration  
- **Flask** – Python web framework  
- **kubectl** – Kubernetes CLI  

## Project Structure

flask-k8s-project/
├── app.py
├── Dockerfile
├── deployment.yaml
├── service.yaml
└── README.md


## Application Description

The Flask application exposes a single endpoint:


## Architecture Overview

1. Flask app is packaged into a Docker image.  
2. The image is deployed to Kubernetes using a Deployment.  
3. Kubernetes manages multiple replicas of the application pods.  
4. A NodePort Service exposes the application via the EC2 public IP.  

## Setup & Deployment Steps

### 1️⃣ Launch AWS EC2 Instance
- AMI: Ubuntu 22.04  
- Instance type: t2.micro (Free Tier)  
- Open ports:  
  - SSH (22)  
  - HTTP / NodePort access  

### 2️⃣ Install Docker
```bash
sudo apt update
sudo apt install docker.io -y
sudo systemctl start docker
sudo systemctl enable docker
```

### 3️⃣ Install Kubernetes (k3s)

curl -sfL https://get.k3s.io | sh -
kubectl get nodes

4️⃣ Build Docker Image
sudo docker build -t flask-k8s .

5️⃣ Deploy Application to Kubernetes
kubectl apply -f deployment.yaml
kubectl apply -f service.yaml

kubectl get pods
kubectl get svc

6️⃣ Access the Application

http://<EC2_PUBLIC_IP>:30007

