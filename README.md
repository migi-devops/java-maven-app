### 🚀 Production-Style CI/CD Pipeline with Jenkins

Automated Jenkins pipeline for building, versioning, and containerizing Java applications with operational debugging, pipeline stabilization, Docker lifecycle management, and production-style CI/CD practices.

---

#### 📌 Project Overview

This project demonstrates a production-oriented CI/CD pipeline designed to automate application builds while improving deployment consistency, artifact traceability, and pipeline reliability.

The implementation focuses not only on successful builds, but also on operational stability and troubleshooting real pipeline failures encountered during development.

The pipeline automates:

- Maven application builds
- Automated version incrementing
- Docker image creation & tagging
- Jenkins multibranch pipeline execution
- GitHub webhook automation
- Docker image publishing
- Pipeline recovery & cleanup operations

Unlike tutorial-only implementations, this project includes real operational issues involving recursive pipeline execution, disk space exhaustion, Docker cleanup, and Jenkins stabilization.

---

#### 💼 Business Problem

Manual application packaging and deployment workflows often create:

- Inconsistent build outputs
- Lack of deployment traceability
- Human error during releases
- Difficult rollback tracking
- Pipeline instability
- Uncontrolled infrastructure usage

This project addresses those problems by implementing an automated CI/CD workflow capable of producing repeatable and traceable application builds.

---

#### ⚙️ DevOps Engineering Value

This project demonstrates practical DevOps engineering capabilities across:

- CI/CD automation
- Jenkins Pipeline as Code
- Automated version management
- Docker containerization
- GitHub integration
- Operational troubleshooting
- Build traceability
- Docker lifecycle management
- Pipeline stabilization
- Infrastructure cleanup operations

The implementation emphasizes operational reliability and debugging rather than only successful pipeline execution.

---

#### 🏗️ Architecture

```text
GitHub Repository
        ↓
Webhook Trigger
        ↓
Jenkins Multibranch Pipeline
        ↓
Maven Build & Version Increment
        ↓
Docker Build & Tagging
        ↓
Docker Hub Registry
        ↓
Container Deployment
```

---

#### ⚙️ Tech Stack

| Area | Technologies |
|------|--------------|
| CI/CD | Jenkins |
| Build Tool | Apache Maven |
| Language | Java |
| Runtime | Spring Boot |
| Containerization | Docker |
| Source Control | Git & GitHub |
| Automation | Jenkinsfile |
| IDE | VS Code |

---

#### 📂 Repository Structure

```bash
java-maven-app/
│
├── Jenkinsfile
├── pom.xml
├── Dockerfile
├── src/
├── assets/
└── README.md
```

---

#### 🔄 CI/CD Pipeline Workflow

#### 1️⃣ Source Control Integration

- GitHub repository connected to Jenkins Multibranch Pipeline
- Automatic pipeline execution through GitHub webhooks
- Branch isolation used for safer pipeline testing
- Pipeline execution defined entirely as code using Jenkinsfile

Example branches:

```bash
jenkins-jobs
jenkins-shared-lib
master
starting-code
```

---

#### 2️⃣ Automated Maven Build

The pipeline compiles and packages the Java application using Maven.

Pipeline stages include:

- Dependency resolution
- Test execution
- Artifact packaging
- Build verification

The build process also integrates automated version management for traceable releases.

---

#### 3️⃣ Automated Version Incrementing

One of the key engineering improvements in this project was implementing automated version management directly inside the Jenkins pipeline.

The pipeline:

- Parses the current Maven version
- Increments versions automatically
- Commits updated versions back to Git
- Maintains build traceability

Example Maven commands used:

```bash
mvn build-helper:parse-version versions:set \
-DnewVersion=$VERSION.$BUILD_NUMBER \
versions:commit
```

This improves:

- Release consistency
- Artifact tracking
- Build reproducibility
- Deployment traceability

---

#### 4️⃣ Docker Image Build & Tagging

Docker images are built automatically during Jenkins execution.

Example build:

```bash
docker build -t miguelprint/demo-app:1.0 .
```

Images are tagged dynamically using version and build identifiers.

Example image tags:

```bash
1.1.2-98
java-maven-1.0
```

The project uses:

```dockerfile
amazoncorretto:17-alpine-jdk
```

as the container base image for lightweight Java runtime support.

---

#### 5️⃣ Docker Registry Integration

The pipeline supports optional Docker Hub publishing using Jenkins-managed credentials.

This allows:

- Centralized image storage
- Versioned deployment artifacts
- Consistent image distribution
- Future cloud deployment readiness

---

#### 🧪 Real-World Operational Troubleshooting

A major focus of this project was operational debugging and CI/CD pipeline stabilization.

The implementation intentionally documents production-style issues encountered during development and the recovery steps used to resolve them.

---

#### ❌ Challenge — Recursive Pipeline Trigger Loop

#### Problem

The Jenkins pipeline entered a recursive execution loop where builds continuously triggered themselves.

#### Impact

This caused:

- Multiple back-to-back pipeline executions
- Rapid Jenkins disk consumption
- Unnecessary Docker image creation
- Increased infrastructure resource usage
- Pipeline instability

Example operational symptoms included:

- Repeated Jenkins build executions
- Node disk space exhaustion
- Docker image accumulation

---

#### 🔍 Root Cause

The issue originated from a misconfiguration involving:

- GitHub webhook triggers
- Jenkins pipeline commits/pushes inside the pipeline itself

The pipeline was unintentionally triggering additional builds after each automated Git operation.

---

#### ✅ Resolution

The pipeline was stabilized by:

- Identifying recursive trigger behavior
- Adjusting Jenkins pipeline logic
- Cleaning Jenkins workspaces
- Removing unused Docker images
- Improving pipeline execution flow

Docker cleanup operations included:

```bash
docker system prune
docker image prune
```

This restored build stability and reduced unnecessary resource consumption.

---

#### 💡 Operational Insight

CI/CD pipelines must be designed carefully to avoid self-triggering automation loops.

In production environments, this type of issue can lead to:

- Infrastructure instability
- Increased cloud costs
- Storage exhaustion
- Deployment failures
- Pipeline reliability problems

The troubleshooting process reinforced the importance of operational observability and infrastructure cleanup practices within automated CI/CD systems.

---

#### 🌐 Integrated Application Context

In addition to the Java Maven application, the project also included lightweight JavaScript application testing used during Docker and container workflow validation.

This helped validate:

- Docker image behavior
- Port mappings
- Container networking
- Registry testing workflows

The implementation provided additional hands-on experience with multi-application container workflows commonly seen in real deployment environments.

---

#### ☁️ Cloud Readiness

Although this implementation runs primarily in a local Jenkins environment, the architecture aligns directly with modern AWS deployment workflows.

The same CI/CD design can later integrate with:

- Amazon EC2
- Amazon ECR
- Amazon EKS
- AWS CodePipeline
- IAM-based authentication

This project later evolved into a more advanced AWS deployment pipeline involving remote EC2 deployments and Docker registry integration.

---

#### 🔗 Related Project

This CI/CD implementation later evolved into a production-style AWS deployment pipeline involving:

- AWS EC2 deployments
- Docker Hub registry integration
- SSH deployment automation
- Jenkins multibranch deployments
- Infrastructure troubleshooting
- Remote Docker lifecycle management

➡️ Repository:
https://github.com/migi-devops/aws-devops-pipeline

---

#### 📈 DevOps Concepts Demonstrated

This project demonstrates practical implementation of:

- CI/CD Automation
- Jenkins Pipeline as Code
- Automated Versioning
- Docker Containerization
- GitHub Webhook Integration
- Docker Image Management
- Build Automation
- Operational Troubleshooting
- Infrastructure Cleanup
- Pipeline Stabilization
- Artifact Traceability

---

#### 🔮 Future Improvements

Planned next steps:

- Push images to AWS ECR
- Kubernetes deployment with EKS
- Jenkins Shared Libraries
- Automated testing stages
- Infrastructure as Code with Terraform
- Monitoring & logging integration
- GitOps deployment workflows

---

#### 👨‍💻 Author

**Miguel — DevOps Engineer**

Focused on building production-oriented DevOps projects involving CI/CD automation, cloud infrastructure, containerization, and operational troubleshooting.

---

#### 📚 Learning Source

This project was built while completing the DevOps Bootcamp by TechWorld with Nana.

The implementation extends the original concepts through additional operational debugging, CI/CD stabilization, Docker lifecycle management, and production-style pipeline improvements.
