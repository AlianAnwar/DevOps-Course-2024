# 🛠️DevOps Tooling Operations for [Sample Project](https://github.com/shivamsinghal1301/restro-project)


This document outlines the DevOps tooling operations that I have implemented in this project using **Kyverno policies** and **GitHub Actions CI/CD pipeline**.

## 1. Applying Kyverno Policies

To ensure that Kubernetes resources are properly managed, I applied **Kyverno policies** to enforce resource requests and limits for all Pods in the project.

### Kyverno Policy for Resource Limits

This policy checks that all Pods have resource requests and limits for CPU and memory. It helps ensure that Pods are not scheduled without defined resource allocations, improving cluster stability and resource management.

**Policy YAML (`k8s/policies/resource-limits.yml`):**
```yaml
apiVersion: kyverno.io/v1
kind: ClusterPolicy
metadata:
  name: pod-resource-limits
spec:
  rules:
    - name: check-resource-limits
      match:
        resources:
          kinds:
            - Pod
      validate:
        message: "Pod should have resource requests and limits"
        pattern:
          spec:
            containers:
              - resources:
                  requests:
                    memory: "128Mi"
                    cpu: "100m"
                  limits:
                    memory: "256Mi"
                    cpu: "200m"
```


## Applying the Kyverno Policy:
I applied the policy to the Kubernetes cluster using the following command:

```
kubectl apply -f k8s/policies/resource-limits.yml
```

## 2. Automating with CI/CD Using GitHub Actions
I automated the build, push, and deployment processes for both the backend and frontend using GitHub Actions. This allows for continuous integration and continuous deployment (CI/CD), streamlining the process and ensuring that the latest changes are always deployed to the cluster.

## GitHub Actions Workflow for CI/CD
The CI/CD pipeline is defined in the .github/workflows/ci-cd.yml file. This file contains the steps to build Docker images for both the backend and frontend applications, push them to Docker Hub, and deploy them to Kubernetes.

CI/CD Workflow YAML (.github/workflows/ci-cd.yml):
```
name: CI/CD Pipeline

on:
  push:
    branches:
      - main

jobs:
  build-and-deploy:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout code
        uses: actions/checkout@v2

      - name: Build and Push Backend Docker Image
        run: |
          docker build -t ahsan-docker/backend-app ./backend
          docker push ahsan-docker/backend-app

      - name: Build and Push Frontend Docker Image
        run: |
          docker build -t alian-docker/frontend-app ./frontend
          docker push alian-docker/frontend-app

      - name: Deploy to Kubernetes
        run: |
          kubectl apply -f k8s/backend-deployment.yml
          kubectl apply -f k8s/frontend-deployment.yml
```

## Explanation of the Workflow:
#### Trigger: The workflow is triggered every time I push changes to the main branch.
#### Checkout Code: The workflow checks out the latest code from the repository.
#### Build and Push Docker Images: It then builds the Docker images for the backend and frontend, tags them, and pushes them to my Docker Hub account.
#### Deploy to Kubernetes: Finally, the workflow deploys the updated Docker images to the Kubernetes cluster by applying the deployment YAML files for both backend and frontend.


With these integrations in place, I have successfully set up a Kyverno policy to enforce resource limits and a GitHub Actions CI/CD pipeline to automate my project’s Kubernetes deployment process. These steps streamline the workflow, ensure resource management, and reduce the potential for errors during deployment.
