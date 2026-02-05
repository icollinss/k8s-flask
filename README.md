![CI](https://github.com/icollinss/k8s-flask/actions/workflows/ci.yml/badge.svg)


��� Flask Application Deployment on Kubernetes (k3s) using AWS EC2
��� Project Overview

This project demonstrates how to containerize a simple Flask application and deploy it on a Kubernetes cluster (k3s) running on an AWS EC2 instance.

The goal of this project is to showcase core DevOps concepts such as Docker, Kubernetes deployments, services, and application scaling — all using a cloud-based environment without relying on local machine admin privileges.

���️ Technologies Used

AWS EC2 – Cloud compute instance

Ubuntu 22.04 – Server operating system

Docker – Containerization

Kubernetes (k3s) – Container orchestration

Flask – Python web framework

kubectl – Kubernetes command-line tool

��� Project Structure
flask-k8s-project/
├── app.py
├── Dockerfile
├── deployment.yaml
├── service.yaml
└── README.md

⚙️ Application Description

The Flask application exposes a single endpoint:

GET / → returns a welcome message served from a Kubernetes-managed container.

��� Architecture Overview

A Flask app is packaged into a Docker image.

The image is deployed to Kubernetes using a Deployment.

Kubernetes manages multiple replicas of the application pods.

A NodePort Service exposes the application to the internet via the EC2 public IP.

��� Setup & Deployment Steps
1️⃣ Launch AWS EC2 Instance

AMI: Ubuntu 22.04

Instance type: t2.micro (Free Tier)

Open ports:

SSH (22)

HTTP / NodePort access

2️⃣ Install Docker on EC2
sudo apt update
sudo apt install docker.io -y
sudo systemctl start docker
sudo systemctl enable docker

3️⃣ Install Kubernetes (k3s)
curl -sfL https://get.k3s.io | sh -


Verify cluster:

kubectl get nodes

4️⃣ Build Docker Image
sudo docker build -t flask-k8s .

5️⃣ Deploy Application to Kubernetes
kubectl apply -f deployment.yaml
kubectl apply -f service.yaml


Check status:

kubectl get pods
kubectl get svc

6️⃣ Access the Application

Open in your browser:

http://<EC2_PUBLIC_IP>:30007


Expected output:

Hello from Kubernetes ���

��� Scaling the Application

Kubernetes allows horizontal scaling with a single command:

kubectl scale deployment flask-app --replicas=3


Verify:

kubectl get pods

��� Cleanup

To remove all Kubernetes resources:

kubectl delete -f service.yaml
kubectl delete -f deployment.yaml


Stop the EC2 instance when not in use to avoid unnecessary costs.

��� Key DevOps Concepts Demonstrated

Containerization with Docker

Kubernetes Deployments & Services

Cloud-based Kubernetes cluster

Application scaling

Infrastructure troubleshooting without local admin access

��� Future Improvements

Add CI/CD using GitHub Actions

Implement Ingress with a domain name

Add monitoring with Prometheus & Grafana

Use Helm for deployment templating

# Flask K8s App

![Build Status](https://img.shields.io/github/actions/workflow/status/USERNAME/REPO/ci.yml)
![Docker Image](https://img.shields.io/docker/v/USERNAME/flask-k8s)

![App Screenshot](screenshots/app.png)


��� Author

Ian Collins
Aspiring DevOps Engineer
Focused on cloud-native applications, automation, and scalable systems
