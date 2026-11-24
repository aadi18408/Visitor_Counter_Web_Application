# Visitor Counter Web Application Using Cloud Computing

## 1. Project Overview
This project demonstrates a Flask-based Visitor Counter application deployed using Docker, Redis and Kubernetes.

Redis stores the visitor count, while Flask provides the web interface and handles visitor requests.

## 2. Objectives
- Containerize the Flask application using Docker.
- Manage multiple containers using Docker Compose.
- Deploy the application on Kubernetes.
- Implement automatic scaling using HPA.
- Demonstrate pod self-healing.
- Simulate failover using a backup deployment.
- Monitor resource usage and apply cost optimization techniques.

## 3. Technologies Used
- Python
- Flask
- Redis
- Docker
- Docker Compose
- Kubernetes
- Minikube
- Horizontal Pod Autoscaler

## 4. Project Files
- app.py – Flask application
- requirements.txt – Python dependencies
- Dockerfile – Docker image configuration
- docker-compose.yml – Multi-container configuration
- k8s.yaml – Kubernetes deployment and services
- backup.yaml – Backup deployment and service
- hpa.yaml – Autoscaling configuration

## 5. Run Using Docker Compose
Start the application:

    docker compose up --build -d

Check containers:

    docker compose ps

Open http://localhost:5000

Stop containers:

    docker compose down

## 6. Kubernetes Deployment
Build the application image:

    minikube image build -t visitor-counter:1.0 .

Apply Kubernetes configurations:

    kubectl apply -f k8s.yaml
    kubectl apply -f backup.yaml
    kubectl apply -f hpa.yaml

Check pods:

    kubectl get pods

Check services:

    kubectl get services

## 7. Autoscaling
The Horizontal Pod Autoscaler is configured with:
- Minimum replicas: 2
- Maximum replicas: 5
- Target CPU utilization: 50%

## 8. Failover Simulation
A separate backup deployment is used to demonstrate local failover. The main service selector can be switched to backup pods.

This is a local Minikube simulation, not a deployment across real public cloud providers.

## 9. Cost Optimization
- CPU and memory requests and limits are configured.
- HPA adjusts replicas according to CPU demand.
- Backup replicas can be reduced when not required.
- A lightweight Python slim base image is used.

## 10. Conclusion
The project demonstrates containerization, orchestration, autoscaling, monitoring, self-healing and local failover using cloud-native technologies.
