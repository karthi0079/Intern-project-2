# CI/CD Pipeline with GitHub Actions & Docker

## Project Overview

This project demonstrates an automated Continuous Integration and Continuous Delivery (CI/CD) pipeline for a Python Flask web application using GitHub Actions and Docker.

Whenever code is pushed to the `main` branch, GitHub Actions automatically runs application tests, builds a Docker image and publishes it to Docker Hub.

The published Docker image can then be pulled and deployed in any Docker-supported environment.

## Architecture

```text
Developer
    |
    | Git Push
    v
GitHub Repository
    |
    v
GitHub Actions
    |
    +----> Install Dependencies
    |
    +----> Run Pytest
    |
    v
Tests Passed?
    |
    v
Docker Buildx
    |
    v
Docker Hub
    |
    v
Pull Docker Image
    |
    v
Docker Container Deployment
```

## Technologies Used

| Technology | Purpose |
|---|---|
| Python 3.12 | Application development |
| Flask | Web framework |
| Gunicorn | Application server |
| Pytest | Automated testing |
| Docker | Containerization |
| Docker Compose | Container management |
| Git & GitHub | Version control |
| GitHub Actions | CI/CD automation |
| Docker Hub | Container image registry |
| Git Bash | Command-line environment |

## Project Structure

```text
devops-cicd-project/
│
├── .github/
│   └── workflows/
│       └── ci-cd.yml
│
├── tests/
│   └── test_app.py
│
├── app.py
├── requirements.txt
├── Dockerfile
├── docker-compose.yml
├── .dockerignore
├── .gitignore
└── README.md
```

## Application Features

- Flask-based web application.
- Home endpoint displaying application information.
- Health-check endpoint for application availability.
- Automated testing using Pytest.
- Docker-based application deployment.

### Application Endpoints

| Endpoint | Description |
|---|---|
| `/` | Application information |
| `/health` | Application health status |

## CI/CD Pipeline Implementation

### 1. Continuous Integration (CI)

GitHub Actions performs the following operations:

1. Checks out the source code.
2. Sets up Python 3.12.
3. Installs application dependencies.
4. Executes automated tests using Pytest.

### 2. Continuous Delivery (CD)

After successful testing on pushes to the `main` branch:

1. Docker Buildx is initialized.
2. GitHub Actions authenticates with Docker Hub using GitHub Secrets.
3. Docker image tags are generated.
4. Docker image is built.
5. Image is published to Docker Hub.

The workflow generates:
- `latest` – Latest application image.
- `sha-*` – Commit-specific image version.

### 3. Security Configuration

Docker Hub credentials are securely stored in GitHub repository secrets.

| Secret | Description |
|---|---|
| `DOCKERHUB_USERNAME` | Docker Hub username |
| `DOCKERHUB_TOKEN` | Docker Hub access token |

Credentials are not hardcoded in the workflow.

## Installation and Execution

### Prerequisites

- Windows operating system
- Git Bash
- Git
- Docker Desktop
- GitHub account
- Docker Hub account

### Step 1: Clone Repository

```bash
git clone https://github.com/karthi2801/devops-cicd-project.git

cd devops-cicd-project
```

### Step 2: Build Docker Image

```bash
docker compose build
```

### Step 3: Start Application

```bash
docker compose up -d
```

### Step 4: Verify Container

```bash
docker ps
```

### Step 5: Test Application

```bash
curl http://localhost:5000/
```

```bash
curl http://localhost:5000/health
```

### Step 6: Run Automated Tests

```bash
docker compose exec web python -m pytest -v
```

## Deploying the Published Docker Image

Pull the image from Docker Hub:

```bash
docker pull karthi2801/devops-cicd-project:latest
```

Run the container:

```bash
docker run -d \
  --name cicd-production \
  -p 5001:5000 \
  --restart unless-stopped \
  karthi2801/devops-cicd-project:latest
```

Verify deployment:

```bash
docker ps
```

Test the deployed application:

```bash
curl http://localhost:5001/
curl http://localhost:5001/health
```

## Project Results

The following results were achieved during implementation:

- Successfully developed and containerized a Flask application.
- Implemented two automated test cases using Pytest.
- Both automated tests passed successfully.
- Configured GitHub Actions for automated testing and Docker image publishing.
- Successfully built and published Docker images to Docker Hub.
- Deployed the published Docker image locally.
- Verified application functionality and health-check endpoints.

## Project Links

**GitHub Repository:**  
https://github.com/karthi2801/devops-cicd-project

**Docker Hub Repository:**  
https://hub.docker.com/r/karthi2801/devops-cicd-project

## Conclusion

This project demonstrates the practical implementation of a CI/CD pipeline using GitHub Actions and Docker. It helped develop hands-on experience in automated testing, containerization, Docker image management, CI/CD automation and application deployment.

The implementation demonstrates how automated workflows can simplify application delivery, improve consistency and reduce manual deployment effort.

---

**Project Domain:** DevOps Engineering  
**Project Title:** CI/CD Pipeline with GitHub Actions & Docker  
**Author:** Karthigai Selvan M