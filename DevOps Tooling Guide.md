# 🛠️ DevOps Tooling Operations for [Sample Project](https://github.com/shivamsinghal1301/restro-project)

This document outlines the DevOps tooling I’ve implemented in this project, leveraging **Kyverno policies** and **GitHub Actions CI/CD pipeline** to automate deployment and ensure smooth operations.

---

## 1️⃣ Enforcing Kyverno Policies

To maintain effective management of Kubernetes resources, I applied **Kyverno policies** that enforce specific resource requests and limits for all Pods in the project.

### Kyverno Policy to Enforce Resource Allocation

This policy ensures that each Pod has clearly defined resource requests and limits for CPU and memory. This setup prevents Pods from being scheduled without proper resource allocations, which improves cluster stability and optimizes resource usage.

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
To apply the policy to the Kubernetes cluster, I used the following command:

```
kubectl apply -f k8s/policies/resource-limits.yml
```

## 2. Automating with CI/CD Using GitHub Actions
I automated the processes of building, pushing, and deploying the backend and frontend components using GitHub Actions. This enables continuous integration and deployment (CI/CD), ensuring that the latest changes are always deployed to the Kubernetes cluster.

## GitHub Actions Workflow for CI/CD
The CI/CD pipeline is defined in the .github/workflows/ci-cd.yml file. It automates the creation of Docker images for both the backend and frontend, pushes them to Docker Hub, and deploys the images to the Kubernetes cluster.

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
          docker build -t alian-docker/backend-app ./backend
          docker push alian-docker/backend-app

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
#### Trigger: 
The pipeline is triggered whenever changes are pushed to the main branch.
#### Checkout Code: 
The workflow starts by checking out the latest code from the repository.
#### Build and Push Docker Images: 
The pipeline then builds Docker images for the backend and frontend applications, tags them accordingly, and pushes them to my Docker Hub account.
#### Deploy to Kubernetes: 
Finally, the updated Docker images are deployed to the Kubernetes cluster by applying the deployment YAML files for both the backend and frontend.


By integrating Kyverno policies for resource management and setting up an automated GitHub Actions CI/CD pipeline, I've streamlined the deployment process for my project. These steps help ensure consistent resource management and reduce the chance of errors during deployment.
