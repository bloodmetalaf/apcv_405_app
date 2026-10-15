# README APCV 405 Class Project
## CI/CD Pipeline

This project includes an automated CI/CD pipeline using Jenkins that:

1. Pulls code from GitHub
2. Runs automated tests
3. Builds a Docker image
4. Pushes the image to DockerHub
5. Deploys the container locally
6. Performs health checks

### Pipeline Status
- Build: [![Build Status]([http://localhost:8080/buildStatus/icon?job=devops-pipeline-project](http://localhost:8080/job/devops-pipeline-project/22/stages/))](http://localhost:8080/job/devops-pipeline-project/)

### Manual Deployment
```bash
docker pull burdettbloodz/apcv_405_app:latest
docker run -p 9090:8080 burdettbloodz/apcv_405_app:latest
