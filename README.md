# Register App

This project demonstrates a complete CI/CD workflow for deploying a Java-based Register Application using modern DevOps practices.

The application is built with Maven, containerized using Docker, and integrated with Jenkins for Continuous Integration. Code quality is validated through SonarQube, container images are scanned using Trivy, and the deployment process is automated through a separate Continuous Deployment (CD) pipeline.

## Project Overview

The CI pipeline automates the following tasks:

* Clone the application source code from GitHub
* Build the application using Maven
* Execute unit tests
* Perform static code analysis with SonarQube
* Build a Docker image
* Push the image to Docker Hub
* Scan the Docker image for vulnerabilities using Trivy
* Trigger the GitOps-based CD pipeline

## Tech Stack

* Java 17
* Maven
* Jenkins
* Docker
* Docker Hub
* SonarQube
* Trivy
* GitHub

## CI/CD Workflow

```text
GitHub
   │
   ▼
Jenkins CI
   │
   ├── Checkout Source Code
   ├── Build Application
   ├── Run Unit Tests
   ├── SonarQube Analysis
   ├── Build Docker Image
   ├── Push Image to Docker Hub
   ├── Trivy Security Scan
   └── Trigger CD Pipeline
```

## Features

* Automated Continuous Integration
* Maven-based Java build
* Unit testing
* Static code analysis
* Docker image creation
* Docker Hub integration
* Container vulnerability scanning
* Automated deployment pipeline trigger

## Repository Structure

```text
.
├── Jenkinsfile          # CI Pipeline
├── src/                 # Application source code
├── pom.xml              # Maven configuration
└── README.md
```

## Notes

This project focuses on implementing a production-style CI pipeline by integrating build automation, code quality checks, containerization, security scanning, and deployment automation into a single workflow.

