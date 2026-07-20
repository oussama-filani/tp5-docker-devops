# TP5 - Docker & Jenkins

A simple DevOps project demonstrating how to build and publish a Docker image automatically using a Jenkins Pipeline.

## Project Structure

```text
.
├── Dockerfile
├── Jenkinsfile
├── index.html
└── README.md
```

## Technologies

- Jenkins
- Docker
- Nginx
- HTML

## Project Overview

This project contains a simple HTML page served by an Nginx container. Jenkins automates the CI/CD pipeline by:

1. Building the Docker image.
2. Logging in to Docker Hub.
3. Publishing the image to Docker Hub.

## Dockerfile

The Docker image is based on the official Nginx image.

```dockerfile
FROM nginx
COPY index.html /usr/share/nginx/html
EXPOSE 80
```

## Jenkins Pipeline

The pipeline performs the following stages:

### 1. Build Image

```bash
docker build -t filani07/jenkins:<BUILD_NUMBER> .
```

### 2. Publish Image

- Authenticate with Docker Hub using Jenkins Credentials.
- Push the generated image.

```bash
docker push filani07/jenkins:<BUILD_NUMBER>
```

## Jenkins Credentials

Configure a **Username with password** credential in Jenkins.

| Field | Value |
|--------|-------|
| Kind | Username with password |
| Username | Docker Hub Username |
| Password | Docker Hub Password or Access Token |
| ID | Your Credentials ID |

Update the `registryCredential` value in the `Jenkinsfile` with your Jenkins Credential ID.

## Build Pipeline

```text
Checkout Source
        │
        ▼
Build Docker Image
        │
        ▼
Docker Login
        │
        ▼
Push Image to Docker Hub
```

## Run the Container

Pull the image:

```bash
docker pull filani07/jenkins:<TAG>
```

Run the container:

```bash
docker run -d -p 8080:80 filani07/jenkins:<TAG>
```

Open your browser:

```
http://localhost:8080
```

## Docker Hub Repository

```
filani07/jenkins
```

## Learning Objectives

- Create a Docker image using a Dockerfile.
- Serve a static website with Nginx.
- Automate Docker builds with Jenkins.
- Push Docker images to Docker Hub.
- Understand a basic CI/CD workflow using Jenkins and Docker.
