# Jenkins for Secure CI/CD
This project implements a **CI/CD (Continuous Integration and Continuous Deployment)** pipeline that automates building, testing, and deploying software using industry-standard DevOps tools while incorporating security best practices.

---

## Pipeline Overview

1. **Source Code Management (GitHub)**
   - Developers push code changes to a GitHub repository.
   - Webhooks trigger the CI/CD pipeline automatically.

2. **Continuous Integration (Jenkins & Maven)**
   - Jenkins orchestrates the pipeline execution.
   - Maven builds the project inside a **Docker agent** to isolate dependencies and reduce attack surface.

3. **Code Quality & Security (SonarQube & Tests)**
   - SonarQube scans the code for **quality issues and security vulnerabilities**.
   - Only code passing security checks is allowed to proceed.
   - Automated tests ensure functionality and mitigate regressions.

4. **Containerization & Image Deployment (DockerHub)**
   - Docker images are built in isolated environments.
   - Images are pushed to DockerHub for deployment.
   - Using Docker agents reduces privilege escalation risks on the host.

5. **Continuous Deployment (Kubernetes & Argo CD)**
   - Deployment manifests are updated automatically in a Git repository.
   - Argo CD detects changes and deploys updates to Kubernetes.
   - Minikube and Argo CD ensure containerized workloads are isolated and manageable.

---

## Security Highlights

- **Isolated Build Environment:** Jenkins pipelines run inside Docker containers to prevent host contamination.
- **Static Analysis:** SonarQube ensures code does not contain vulnerabilities before deployment.
- **Controlled Access:** Jenkins, SonarQube, DockerHub, and Argo CD credentials are stored securely and used via tokens.
- **Network Security:** Ports (Jenkins 8080, SonarQube 9000, Argo CD NodePort) are restricted to authorized access.
- **Immutable Deployments:** Docker images are versioned and pulled from trusted repositories, preventing unverified code from running in production.
- **Secrets Management:** Argo CD retrieves passwords and tokens securely using Kubernetes secrets (base64-encoded).

---

## Quick Start

1. **EC2 Setup**
   - Install Jenkins, SonarQube, Docker.
   - Open required inbound ports for web access.
2. **Jenkins Configuration**
   - Install pipeline and Docker plugins.
   - Connect Jenkins to GitHub, DockerHub, and SonarQube using credentials/tokens.
3. **Pipeline Execution**
   - Jenkinsfile defines CI/CD stages:
     - Build (Maven)
     - Code analysis (SonarQube)
     - Docker image creation
     - Deployment (Argo CD)
4. **Argo CD Deployment**
   - Run Argo CD controller using Operator.
   - Pull the latest manifests from Git and deploy to Kubernetes.
   - Access Argo CD UI securely using NodePort and credentials.

---

## Tools Used

- **CI/CD:** Jenkins, Maven
- **Code Quality & Security:** SonarQube
- **Containerization:** Docker
- **Orchestration & Deployment:** Kubernetes, Argo CD
- **Source Control:** GitHub

---

This CI/CD pipeline ensures **secure, automated, and reliable software delivery** while minimizing risks to infrastructure and production environments.


