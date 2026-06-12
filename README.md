
# Project Overview

This project is a Python-based web application built with the Flask framework, designed for lightweight, service-oriented analytics workloads running in Kubernetes.

## Technology Stack

- **Language:** Python  
- **Framework:** Flask  
- **Containerization:** Docker  
- **CI/CD:** AWS CodeBuild  
- **Container Registry:** Amazon ECR (`194849407325.dkr.ecr.us-east-1.amazonaws.com/coworking`)  
- **Orchestration:** Amazon EKS (`app-cluster`)  
- **Database:** PostgreSQL (deployed inside the same EKS cluster)  

## Build Process

The application is containerized using the Dockerfile located at `analytics/Dockerfile`.  
AWS CodeBuild executes the build pipeline using `buildspec.yaml`, which defines the build lifecycle.  
The pipeline builds the Docker image, tags it, and pushes it to the designated ECR repository.

## Deployment

Kubernetes manifests are stored in the `deployments/` folder and define workloads and services for both the application and database.  
The PostgreSQL database must be deployed and seeded before deploying the application.  
Deploy resources to the `app-cluster` EKS cluster using standard Kubernetes tooling.

## Configuration

The application requires the following environment variables to connect to the database:  
- `DB_NAME`  
- `DB_USERNAME`  
- `DB_HOST`  
- `DB_PORT`  
- `DB_PASSWORD`  

## Release Process

Update application code and Dockerfile as needed, then push changes to trigger the CodeBuild pipeline.  
A new image is built and published to the ECR repository with the appropriate tag.  
Update the image tag in the Kubernetes manifests if required.  
Apply the manifests to the cluster to perform a rolling deployment.

## Notes

Ensure database readiness and seed data availability before application startup.  
Use consistent versioning for Docker images to enable traceability and rollback.
