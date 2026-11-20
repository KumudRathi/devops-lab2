# Lab 2: Containerization & Kubernetes Orchestration

**Student Name:** Kumud Rathi  (2301010161)
**GitHub Repository:** https://github.com/KumudRathi/devops-lab2

## 1. Objective
To understand Docker containerization, image management, storage, networking, Kubernetes deployment, scaling, rolling updates, rollback, and CI/CD automation.

## 2. Tools and Technologies
- Docker
- Docker Desktop
- Ubuntu (WSL2)
- Spring Boot
- Java 21
- Maven
- Docker Hub
- Kubernetes
- Minikube
- kubectl
- GitHub Actions

## 3. Dockerfile
The Spring Boot application was containerized using the following Dockerfile:

```dockerfile
FROM eclipse-temurin:21-jre-alpine
WORKDIR /app
COPY target/*.jar app.jar
EXPOSE 8081
ENTRYPOINT ["java", "-jar", "app.jar"]
```

## 4. Docker Image and Container Management
- Built Docker image: `devops-lab2-app:1.0`
- Created and managed Docker containers.
- Listed, started, stopped, and removed containers.
- Tagged and pushed the image to Docker Hub.
- Used Docker Compose to run the application and Nginx.

## 5. Docker Storage
Three storage methods were tested:
- Container writable layer: data was lost after container removal.
- Named volume: data persisted after container removal.
- Bind mount: host directory data remained available after container removal.

## 6. Docker Networking
- Created a custom bridge network named `lab-network`.
- Connected server and client containers.
- Tested communication using container name and IP address.
- Inspected network configuration.

## 7. Kubernetes Deployment
Created Kubernetes Deployment and Service manifests.

**Deployment:** `deployment.yaml`  
**Service:** `service.yaml`

- Deployed the application using Minikube.
- Configured two replicas.
- Exposed the application through a NodePort service.
- Verified pods and services using kubectl.

## 8. Kubernetes Deployment Strategies
- Scaled deployment from 2 to 4 replicas.
- Scaled deployment back to 2 replicas.
- Performed a rolling image update from version 1.0 to 2.0.
- Practiced rollback using `kubectl rollout undo`.
- Verified deployment status and image version.

## 9. CI/CD Pipeline
Created a GitHub Actions workflow at:

`.github/workflows/ci-cd.yml`

The workflow:
- Checks out the repository.
- Sets up Java 21.
- Builds the Spring Boot JAR using Maven.
- Logs in to Docker Hub using GitHub Secrets.
- Builds and pushes the Docker image.

Kubernetes deployment was updated and verified separately using kubectl.

## 10. Important Commands

```bash
docker images
docker ps -a
docker build -t devops-lab2-app:1.0 .
docker run -d -p 8081:8081 devops-lab2-app:1.0
docker volume ls
docker network ls
docker compose up -d
kubectl get pods
kubectl get deployments
kubectl get services
kubectl scale deployment devops-lab2-deployment --replicas=4
kubectl rollout history deployment/devops-lab2-deployment
kubectl rollout undo deployment/devops-lab2-deployment
```

## 11. Observations
- Docker images package applications and their runtime dependencies.
- Containers provide isolated application execution.
- Named volumes and bind mounts provide persistent storage.
- Custom Docker networks allow containers to communicate.
- Kubernetes manages application replicas and deployment updates.
- Rolling updates and rollbacks help manage application versions.
- GitHub Actions automates image building and publishing.

## 12. Conclusion
This lab provided practical experience with Docker containerization, storage, networking, Kubernetes orchestration, deployment strategies, scaling, and CI/CD pipeline implementation.
