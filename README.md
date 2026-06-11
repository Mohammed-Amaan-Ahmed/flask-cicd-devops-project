# DevOps CI/CD Pipeline Project

## Overview
This project demonstrates a complete CI/CD pipeline using:

- Git
- GitHub
- Docker
- Jenkins
- AWS EC2
- AWS ECR
- Python Flask

## Application

The Flask application exposes:

- `/` : Home endpoint
- `/health` : Health check endpoint

## Docker Commands

Build:

```bash
docker build -t flask-app .
