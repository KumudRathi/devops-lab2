# Lab 2 Final Report
## Containerization & Kubernetes Orchestration

**Student Name:** Kumud Rathi  
**GitHub Repository:** https://github.com/KumudRathi/devops-lab2

---

## 1. Introduction

The objective of this lab was to understand application containerization using Docker and application orchestration using Kubernetes. The lab also covered Docker storage, networking, deployment strategies, scaling, rollback, and CI/CD automation.

## 2. System Architecture

The application was developed using Spring Boot and Java 21. Maven was used to build the application JAR file. Docker was used to package the application into a container image.

The Docker image was deployed to Kubernetes using Minikube. A Kubernetes Deployment managed application replicas, while a NodePort Service exposed the application.

GitHub Actions was configured to automate the application build and Docker image publishing process.

### Architecture Flow

Developer → GitHub Repository → GitHub Actions → Maven Build → Docker Image → Docker Hub → Kubernetes (Minikube) → Spring Boot Application

## 3. Docker Containerization

A Dockerfile was created using the Eclipse Temurin Java 21 runtime image.

The application image was built and executed as a Docker container. Docker commands were used to inspect images, list containers, start and stop containers, and remove unused resources.

Docker Compose was also used to run the Spring Boot application with an Nginx reverse proxy.

## 4. Docker Storage and Networking

Three storage mechanisms were tested:

- Container writable layer: data was lost after container removal.
- Named volume: data persisted after container removal.
- Bind mount: data remained available on the host system.

A custom bridge network named `lab-network` was created. Two containers communicated using their container names and IP addresses.

## 5. Kubernetes Deployment Strategy

The Spring Boot application was deployed using a Kubernetes Deployment with two replicas.

A NodePort Service was configured to expose the application on port 30081.

The deployment was verified using kubectl commands, including:

- `kubectl get pods`
- `kubectl get deployments`
- `kubectl get services`

## 6. Scaling Strategy

Horizontal scaling was tested by increasing the number of replicas from 2 to 4 and then reducing them back to 2.

This demonstrated how Kubernetes can adjust the number of application instances according to workload requirements.

## 7. Rolling Updates and Rollback

A new image tag, version 2.0, was created and used to demonstrate a Kubernetes rolling update.

The rollout status was checked using kubectl. The rollback operation was then performed using:

`kubectl rollout undo deployment/devops-lab2-deployment`

The deployment was restored to the previous image version.

Note: Version 2.0 used the same application content with a different image tag.

## 8. CI/CD Pipeline

GitHub Actions was configured to automate the following steps:

1. Checkout source code from GitHub.
2. Set up Java 21.
3. Build the Spring Boot JAR using Maven.
4. Authenticate with Docker Hub using GitHub Secrets.
5. Build and push the Docker image to Docker Hub.

The Kubernetes deployment update was performed separately using kubectl.

## 9. Observations

- Docker simplifies application packaging and deployment.
- Containers provide an isolated execution environment.
- Docker volumes and bind mounts provide persistent storage.
- Docker bridge networks support container-to-container communication.
- Kubernetes manages application replicas and deployment updates.
- Scaling helps increase or decrease application capacity.
- Rollback provides a way to restore an earlier deployment revision.
- GitHub Actions automates build and image publishing tasks.

## 10. Challenges Faced

- Configuring Docker Desktop integration with Ubuntu WSL2.
- Resolving Docker permission issues.
- Managing port conflicts with an existing Jenkins service.
- Configuring Docker Hub authentication.
- Resolving GitHub repository file-size restrictions.
- Configuring GitHub Actions to build the Maven JAR before building the Docker image.

## 11. Conclusion

This lab provided practical experience with Docker containerization and Kubernetes orchestration. It demonstrated how applications can be packaged, deployed, scaled, updated, and managed using modern DevOps tools.

The lab also introduced CI/CD automation using GitHub Actions and Docker Hub, providing a foundation for understanding automated application delivery.
