# Jenkins 90 Days of DevOps

This repository documents my journey through a 90-day DevOps learning path, focusing on key technologies and practices. This project specifically demonstrates a basic Continuous Integration (CI) pipeline using **Jenkins** and **Docker**.

## Project Overview

The primary goal of this project is to automate the build and run process for a simple Node.js application.

The pipeline is configured to perform the following steps:

1.  **Source Code Management**: Jenkins polls this GitHub repository for new commits to the `main` branch.
2.  **Docker Image Build**: When a new change is detected, Jenkins pulls the code and builds a Docker image using the `Dockerfile` in the root directory.
3.  **Container Deployment**: The pipeline stops any existing container and then runs a new container from the newly built Docker image.

## Getting Started

### Prerequisites

* A running instance of Jenkins.
* A Jenkins agent configured with Docker access and the `docker` label.
* Git and Docker installed on the Jenkins agent.

### Pipeline Configuration

The pipeline is a **Freestyle project** in Jenkins with the following key configurations:

* **Repository URL**: `https://github.com/debsinthecloud/Jenkins-90days-of-devops`
* **Branches to build**: `main`
* **Build Trigger**: Configured to poll for changes on a schedule (`H * * * *`).
* **Build Step (Execute shell)**:
    ```sh
    echo "Building the Docker image..."
    docker build -t app-build .
    echo "Stopping and removing any old container..."
    docker stop app-build-container || true
    docker rm app-build-container || true
    echo "Running the new container..."
    docker run -d --name app-build-container -p 3000:3000 app-build
    ```

## Application

The application is a simple Node.js Express server that listens on port `3000` and serves "Hello World!".

* `package.json`
* `index.js`
* `Dockerfile`
