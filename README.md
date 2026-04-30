### 🚀 CI/CD Pipeline with Jenkins — Debugging Real Pipeline Failures

#### 📂 Repository Branches

This project uses multiple branches to separate concerns:

- jenkins-jobs: complete CI/CD pipeline implementation (Jenkinsfile + pipeline logic)
- jenkins-shared-lib: jenkins shared library for reusable pipeline functions
- master (default): documentation and project overview

#### 📌 Project Overview

This project demonstrates a production-style CI/CD pipeline that builds, versions, and containerizes a Java application using Jenkins — including real-world failure scenarios and fixes.

The pipeline is triggered by GitHub changes and performs:

- Build automation with Maven
- Automated version incrementing
- Docker image creation
- Image tagging for traceability
- (Optional) Push to Docker Hub

#### 🏗️ Architecture

`GitHub → Webhook → Jenkins → Maven → Docker → (Future: AWS ECR → EKS)`

#### ⚙️ Tech Stack

| Area | Technologies |
|------|--------------|
| CI/CD | Jenkins |
| Build Tool | Apache Maven |
| Language | Java |
| Containerization | Docker |
| Source Control | GitHub |
| IDE | Visual Studio Code |

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

This pipeline is designed to produce traceable, versioned Docker images on every commit while preventing recursive execution and ensuring build stability.

**1. Increment Version**
- Uses Maven plugin:

```
build-helper:parse-version
versions:set
```

- Automatically increments version on every pipeline run
- Ensures consistent and traceable builds

**2. Build Application**

- Compiles Java code
- Runs tests
- Packages application into a `.jar` file

**3. Build Docker Image**

- Uses Dockerfile based on: `amazoncorretto:17-alpine-jdk`
- Creates versioned image: `<version>-<build-number>`
Example: `1.1.2-98`

**4. Push Docker Image (Optional)**

- Pushes image to Docker Hub
- Uses Jenkins credentials for authentication

#### 🔑 Key Features

- Automated CI/CD pipeline using Jenkins
- Dynamic versioning for every build
- Docker image creation with unique tags
- GitHub webhook integration (auto-trigger builds)
- Pipeline-as-Code using Jenkinsfile
- Real-world DevOps debugging experience

Below is a successful pipeline run showing all stages executing:

<img src="assets/jenkins-stage-view.png" width="600">

#### 🧪 Real-World Challenges & Fixes

##### ❌ Issue: CI/CD Pipeline Loop (Multiple Builds Triggering Continuously)

**👉 Impact:**

- Multiple builds triggered back-to-back
- Jenkins node disk space rapidly consumed
- Dozens of Docker images pushed unnecessarily
- Risk of pipeline instability and resource exhaustion

This is the kind of issue that can quietly escalate in production and increase infrastructure cost.

This shows multiple pipeline runs including failures and disk space failure:

<img src="assets/loop-jenkins.png" alt="Build History" width="600">

<img src="assets/node-full.png" alt="Disk Space Issue" width="600">

#### 🔍 Root Cause:

The pipeline was triggering itself repeatedly due to a misconfiguration between:

- GitHub webhook triggers
- Jenkins pipeline behavior (commit/push inside pipeline)

#### ✅ Fix:

- Identified recursive trigger pattern
- Adjusted pipeline logic to prevent self-triggering
- Cleaned up Jenkins workspace and old builds
- Removed unused Docker images

Below shows cleaning up unused docker images:

<img src="assets/prune-docker.png" alt="Clean Up Images" width="600">

#### 💡 DevOps Insight:

CI/CD pipelines must be designed to avoid recursive execution.

In production environments, this can lead to:

- Uncontrolled infrastructure usage
- Increased cloud costs (compute + storage)
- System instability

**☁️ Cloud Perspective (AWS Alignment)**

Although this pipeline runs locally, the same design applies directly to AWS environments:

- Jenkins can run on EC2 or be replaced with AWS CodePipeline
- Docker images would be stored in Amazon ECR
- Pipeline execution would integrate with IAM roles instead of static credentials

This ensures the pipeline is cloud-ready and can scale beyond a local setup.

#### 🚀 How to Run the Project

**1. Clone Repository**

`git clone https://github.com/migi-devops/java-maven-app.git
cd java-maven-app`

**2. Configure Jenkins**

- Create a Multibranch Pipeline
- Connect GitHub repository
- Add credentials: GitHub PAT and Docker Hub (optional)

**3. Trigger Pipeline**

- Push code to repository OR
- Trigger manually in Jenkins

#### 📌 Project Summary (In a Nutshell)

This project demonstrates a real-world CI/CD pipeline using Jenkins that automates building, versioning, and containerizing a Java application.

It highlights core DevOps practices:

- CI/CD automation
- Pipeline as Code
- Version control integration
- Containerization
- Troubleshooting production-like issues

#### 🔮 Next Improvements (Roadmap)

- Push images to AWS ECR
- Deploy to Kubernetes (EKS)
- Use Jenkins Shared Library
- Add automated testing stages
- Implement monitoring & logging

**Author:** Miguel (DevOps Engineer)

**Learning Source:** TechWorld with Nana DevOps Bootcamp

This implementation extends the original concepts by introducing additional debugging scenarios, pipeline safeguards, and production-style improvements.
