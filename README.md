Ì∫Ä Flask Application Deployment on Kubernetes (k3s) using AWS EC2
Ì≥å Project Overview

This project demonstrates how to containerize a simple Flask application and deploy it on a Kubernetes cluster (k3s) running on an AWS EC2 instance.

The goal of this project is to showcase core DevOps concepts such as Docker, Kubernetes deployments, services, and application scaling ‚Äî all using a cloud-based environment without relying on local machine admin privileges.

Ìª†Ô∏è Technologies Used

AWS EC2 ‚Äì Cloud compute instance

Ubuntu 22.04 ‚Äì Server operating system

Docker ‚Äì Containerization

Kubernetes (k3s) ‚Äì Container orchestration

Flask ‚Äì Python web framework

kubectl ‚Äì Kubernetes command-line tool

Ì≥Ç Project Structure
flask-k8s-project/
‚îú‚îÄ‚îÄ app.py
‚îú‚îÄ‚îÄ Dockerfile
‚îú‚îÄ‚îÄ deployment.yaml
‚îú‚îÄ‚îÄ service.yaml
‚îî‚îÄ‚îÄ README.md

‚öôÔ∏è Application Description

The Flask application exposes a single endpoint:

GET / ‚Üí returns a welcome message served from a Kubernetes-managed container.

Ì∑± Architecture Overview

A Flask app is packaged into a Docker image.

The image is deployed to Kubernetes using a Deployment.

Kubernetes manages multiple replicas of the application pods.

A NodePort Service exposes the application to the internet via the EC2 public IP.

Ì∫Ä Setup & Deployment Steps
1Ô∏è‚É£ Launch AWS EC2 Instance

AMI: Ubuntu 22.04

Instance type: t2.micro (Free Tier)

Open ports:

SSH (22)

HTTP / NodePort access

2Ô∏è‚É£ Install Docker on EC2
sudo apt update
sudo apt install docker.io -y
sudo systemctl start docker
sudo systemctl enable docker

3Ô∏è‚É£ Install Kubernetes (k3s)
curl -sfL https://get.k3s.io | sh -


Verify cluster:

kubectl get nodes

4Ô∏è‚É£ Build Docker Image
sudo docker build -t flask-k8s .

5Ô∏è‚É£ Deploy Application to Kubernetes
kubectl apply -f deployment.yaml
kubectl apply -f service.yaml


Check status:

kubectl get pods
kubectl get svc

6Ô∏è‚É£ Access the Application

Open in your browser:

http://<EC2_PUBLIC_IP>:30007


Expected output:

Hello from Kubernetes Ì∫Ä

Ì≥à Scaling the Application

Kubernetes allows horizontal scaling with a single command:

kubectl scale deployment flask-app --replicas=3


Verify:

kubectl get pods

Ì∑π Cleanup

To remove all Kubernetes resources:

kubectl delete -f service.yaml
kubectl delete -f deployment.yaml


Stop the EC2 instance when not in use to avoid unnecessary costs.

ÌæØ Key DevOps Concepts Demonstrated

Containerization with Docker

Kubernetes Deployments & Services

Cloud-based Kubernetes cluster

Application scaling

Infrastructure troubleshooting without local admin access

Ì≥Ñ Future Improvements

Add CI/CD using GitHub Actions

Implement Ingress with a domain name

Add monitoring with Prometheus & Grafana

Use Helm for deployment templating

# Flask K8s App

![Build Status](https://img.shields.io/github/actions/workflow/status/USERNAME/REPO/ci.yml)
![Docker Image](https://img.shields.io/docker/v/USERNAME/flask-k8s)

![App Screenshot](screenshots/app.png)


Ì±§ Author

Ian Collins
Aspiring DevOps Engineer
Focused on cloud-native applications, automation, and scalable systems
