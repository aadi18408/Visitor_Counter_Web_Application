# CLOUD COMPUTING PROJECT REPORT

## Project Title
Deployment of a Visitor Counter Web Application Using Docker and Kubernetes

## 1. Introduction
Cloud computing provides scalable and flexible computing resources for hosting applications. This project demonstrates how a web application can be containerized, deployed, monitored and scaled using cloud-native technologies.

The project uses a Flask-based Visitor Counter application. Redis is used to store visitor counts, Docker provides containerization and Kubernetes manages application deployment.

## 2. Problem Statement
Traditional application deployment can make scaling, resource management and recovery difficult. This project addresses these challenges by using containers and Kubernetes orchestration.

## 3. Objectives
1. Develop a visitor counter using Flask and Redis.
2. Containerize the application using Docker.
3. Run multiple services using Docker Compose.
4. Deploy the application using Kubernetes.
5. Demonstrate automatic scaling using HPA.
6. Demonstrate self-healing and backup failover.
7. Monitor resource usage and study cost optimization.

## 4. Technologies Used
- Python and Flask
- Redis
- Docker
- Docker Compose
- Kubernetes
- Minikube
- kubectl
- Horizontal Pod Autoscaler

## 5. System Architecture
User
  |
  v
Kubernetes NodePort Service
  |
  v
Flask Visitor Counter Deployment
  |
  v
Redis Service
  |
  v
Redis Pod

Additional components:
- Metrics Server monitors CPU usage.
- HPA adjusts the number of application replicas.
- Backup Deployment provides a separate set of application pods.
- Service selector switching demonstrates local failover.

## 6. Implementation

### 6.1 Flask and Redis
The Flask application handles visitor requests. Redis stores the visitor count so that the count is maintained outside the application container.

### 6.2 Docker
A Dockerfile was created using the Python slim base image. The application runs using Gunicorn.

### 6.3 Docker Compose
Docker Compose runs two services:
- Flask web application
- Redis database

Both containers were verified in the running state.

### 6.4 Kubernetes
Kubernetes deployments and services were created for Redis and the visitor counter application.

The primary application deployment was configured with two replicas. A NodePort service exposes the application.

### 6.5 Self-Healing
Kubernetes Deployment maintains the desired number of replicas. When an application pod is deleted, Kubernetes creates a replacement pod automatically.

### 6.6 Horizontal Pod Autoscaling
HPA was configured with:
- Minimum replicas: 2
- Maximum replicas: 5
- Target CPU utilization: 50%

During the load test, the application scaled up to five replicas. After the load reduced, the replica count returned to two.

### 6.7 Backup and Failover
A separate backup deployment and backup service were created.

The main service selector was switched to backup pods to simulate failover. This experiment was performed locally using Minikube and does not represent a real multi-cloud deployment.

## 7. Testing and Results

### Docker Compose
Both Redis and Flask web containers were verified as running.

### Kubernetes
The Redis pod and two primary visitor-counter pods were running successfully.

### Backup Deployment
The backup deployment was also verified with running pods.

### HPA
The final HPA status showed:
- CPU utilization: 1% / 50%
- Minimum replicas: 2
- Maximum replicas: 5
- Current replicas: 2

A previous load test demonstrated scaling up to five replicas.

### Resource Monitoring
The following measurements were recorded using kubectl top pods:

| Component | CPU Usage | Memory Usage |
| Redis | 8m | 9Mi |
| Visitor Counter Pod 1 | 1m | 38Mi |
| Visitor Counter Pod 2 | 1m | 39Mi |
| Backup Pod | 1m | 37Mi |

These are local measurements taken during project execution.

## 8. Cost Optimization Techniques

1. Horizontal Autoscaling:
   HPA adjusts application replicas according to CPU demand. This avoids keeping the maximum number of application replicas active during low traffic.

2. Backup Replica Optimization:
   The backup deployment was reduced from two replicas to one during an earlier configuration test. This reduced the backup pod count by 50%.

3. Resource Monitoring and Right-Sizing:
   CPU and memory usage were monitored using kubectl top pods. Resource requests and limits were configured in Kubernetes to support controlled resource allocation.

4. Lightweight Container Image:
   The Python slim base image was used to avoid unnecessary packages in the application image.

Note: These optimizations demonstrate resource-management techniques. Actual monetary savings were not calculated because the project was executed locally using Minikube rather than a paid cloud provider.

## 9. Limitations
- The Kubernetes environment uses local Minikube.
- No actual public cloud provider was used.
- Failover is demonstrated through a local backup deployment.
- Cloud billing savings were not measured.

## 10. Future Scope
- Deploy the application on AWS, Azure or Google Cloud.
- Configure real multi-region or multi-cloud failover.
- Add persistent monitoring dashboards.
- Integrate automated CI/CD pipelines.
- Perform larger-scale performance testing.

## 11. Conclusion
The project successfully demonstrates the deployment and management of a Flask and Redis visitor counter application using Docker and Kubernetes.

It covers containerization, orchestration, self-healing, horizontal autoscaling, resource monitoring and local failover simulation. The project provides practical experience with important cloud computing concepts and cloud-native tools.
