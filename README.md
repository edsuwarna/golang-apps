# Golang Hello World App

A simple Golang HTTP server application with Docker support and automated CI/CD pipeline using GitHub Actions.

## Features

- Simple HTTP server written in Go
- Returns "Hello, World!" message with timestamp
- Containerized with Docker
- Automated Docker image builds and publishing via GitHub Actions
- Semantic versioning support

## Prerequisites

- Go 1.23 or higher (for local development)
- Docker (for containerized deployment)
- Docker Compose (optional, for easy container management)

## Running Locally

### Without Docker

```bash
go run main.go
```

The server will start on `http://localhost:8080`

### With Docker

Build and run the Docker container:

```bash
docker build -t golang-hello-world .
docker run -p 8080:8080 golang-hello-world
```

### With Docker Compose

```bash
docker-compose up
```

## Testing the Application

Once the server is running, test it with:

```bash
curl http://localhost:8080
```

Expected response:
```
Hello, World! The time is: 2026-01-14 12:34:56
```

## CI/CD Pipeline

This repository uses GitHub Actions to automatically build and push Docker images to Docker Hub.

### Workflow Triggers

The pipeline runs on:
- Pushes to `main` or `master` branches
- Version tags (format: `v*.*.*`)
- Manual workflow dispatch
- Release publications

### Creating a Release

To create a new release and trigger the Docker build:

1. Create and push a version tag:
```bash
git tag v1.0.0
git push origin v1.0.0
```

2. The GitHub Actions workflow will automatically:
   - Build the Docker image
   - Tag it with the version number (e.g., `1.0.0`)
   - Push it to Docker Hub

### Docker Image

The Docker image is available at:
```
docker pull <your-dockerhub-username>/golang-hello-world:1.0.0
```

## Project Structure

```
.
├── .github/
│   └── workflows/
│       └── docker-build-push.yml  # CI/CD pipeline configuration
├── main.go                         # Main application code
├── go.mod                          # Go module definition
├── Dockerfile                      # Docker image configuration
├── docker-compose.yml              # Docker Compose configuration
└── README.md                       # This file
```

## Configuration

### GitHub Secrets

To use the CI/CD pipeline, configure these secrets in your GitHub repository:

- `DOCKER_USERNAME`: Your Docker Hub username
- `DOCKER_PASSWORD`: Your Docker Hub password or access token

Go to: Repository Settings → Secrets and variables → Actions → New repository secret

## License

This project is created for DevOps training purposes.
