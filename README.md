### 🚀 Capstone Project 1 – CI/CD Pipeline with Jenkins, Maven & Docker

Recreated from TechWorld with Nana DevOps Bootcamp

Original reference: https://gitlab.com/twn-devops-bootcamp/latest/08-ci-cd/java-maven-app

#### 📌 Project Overview

This project demonstrates a fully automated CI/CD pipeline using Jenkins to build, version, and containerize a Java application.

The pipeline is triggered by GitHub changes and performs:

- Build automation with Maven
- Automated version incrementing
- Docker image creation
- Image tagging for traceability
- (Optional) Push to Docker Hub

#### 🎯 Goal

The goal of this project is to:

- Automate the build process of a Java Maven application
- Implement a CI/CD pipeline using Jenkins
- Apply versioning strategy for traceable releases
- Containerize the application using Docker
- Understand real-world DevOps troubleshooting (Git, Jenkins, credentials, disk issues)

#### 🏗️ Architecture

`GitHub → Webhook → Jenkins Pipeline → Maven Build → Docker Build → (Docker Hub)`

#### ⚙️ Tech Stack

- CI/CD: Jenkins
- Build Tool: Apache Maven
- Language: Java
- Containerization: Docker
- Source Control: GitHub
- IDE: Visual Studio Code

#### 📂 Repository Structure

```
java-maven-app/
│
├── Jenkinsfile              # CI/CD pipeline definition
├── pom.xml                  # Maven build configuration
├── Dockerfile               # Docker image build instructions
├── src/                     # Application source code
└── README.md                # Project documentation
```

#### 🔄 CI/CD Pipeline Breakdown

1. Increment Version
- Uses Maven plugin:
