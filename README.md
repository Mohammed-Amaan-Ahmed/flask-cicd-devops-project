# Flask CI/CD Pipeline using Jenkins, Docker, AWS ECR and EC2

## Project Overview

This project demonstrates a complete end-to-end CI/CD pipeline for a Python Flask application using Jenkins, Docker, Amazon Elastic Container Registry (ECR), and Amazon EC2.

The pipeline automatically builds a Docker image from source code hosted on GitHub, pushes the image to Amazon ECR, and deploys the application on an EC2 instance.

---

## Architecture

```text
Developer
    |
    v
 GitHub
    |
    v
 Jenkins Pipeline
    |
    v
 Docker Build
    |
    v
 Amazon ECR
    |
    v
 AWS EC2
    |
    v
 Flask Container
    |
    v
 Flask Web Application
```

---

## Technologies Used

* Python Flask
* Docker
* Jenkins
* Git & GitHub
* AWS EC2
* AWS ECR
* Ubuntu Linux
* AWS CLI

---

## Repository Structure

```text
flask-cicd-devops-project/

├── app.py
├── Dockerfile
├── Jenkinsfile
├── requirements.txt
├── .dockerignore
├── .gitignore
├── screenshots/
├── docs/
└── README.md
```

---

## CI/CD Workflow

1. Developer pushes code to GitHub.
2. Jenkins pulls the latest source code.
3. Jenkins builds a Docker image.
4. Jenkins tags the image using the Jenkins build number.
5. Jenkins authenticates with Amazon ECR.
6. Jenkins pushes the Docker image to ECR.
7. EC2 pulls the latest image.
8. Docker container starts automatically.
9. Flask application becomes accessible through the EC2 public IP.

---

## Jenkins Pipeline Stages

### Build Docker Image

Builds a Docker image from the application source code.

### Tag Docker Image

Tags the Docker image with the ECR repository URI.

### Login to Amazon ECR

Authenticates Jenkins with AWS ECR using AWS CLI.

### Push Image to ECR

Pushes the generated Docker image to Amazon ECR.

---

## AWS Services Used

### Amazon EC2

Used as the Jenkins server and Docker host.

### Amazon ECR

Used as a private Docker image repository.

---

## Challenges Faced

### Jenkinsfile Syntax Error

Issue:
Unexpected Groovy compilation errors caused by Markdown backticks accidentally added inside Jenkinsfile.

Resolution:
Removed Markdown formatting and corrected Jenkins Pipeline syntax.

---

### Docker Not Found Inside Jenkins

Issue:
Jenkins container could not execute Docker commands.

Resolution:
Mounted Docker socket and installed Docker CLI inside Jenkins container.

---

### Docker Permission Denied

Issue:
Jenkins failed to access Docker daemon.

Resolution:

```bash
sudo chmod 666 /var/run/docker.sock
```

---

### Low Memory on Free Tier EC2

Issue:
Jenkins occasionally became unstable due to memory limitations.

Resolution:

```bash
sudo fallocate -l 1G /swapfile
sudo chmod 600 /swapfile
sudo mkswap /swapfile
sudo swapon /swapfile
```

---

## Results

* Successfully built Docker images through Jenkins.
* Successfully pushed Docker images to Amazon ECR.
* Successfully deployed Flask container on EC2.
* Verified application availability using EC2 Public IP.
* Implemented complete CI/CD workflow.

---

## Future Enhancements

* SonarQube Code Quality Analysis
* Trivy Container Security Scanning
* Terraform Infrastructure as Code
* Kubernetes Deployment (Amazon EKS)
* Prometheus Monitoring
* Grafana Dashboards
* Automated Deployment Stage

---

## Screenshots

Add screenshots inside the screenshots folder:

* GitHub Repository
* Jenkins Dashboard
* Successful Jenkins Build
* Amazon ECR Repository
* EC2 Instance
* Docker Images
* Running Containers
* Flask Application

---

## Author

**Mohammed Amaan Ahmed**

DevOps Engineer | AWS | Docker | Jenkins | CI/CD | Linux