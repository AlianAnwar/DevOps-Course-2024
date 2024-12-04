# 🚀 1. Automating Kubernetes Deployments: CI/CD Pipeline with Jenkins and GitLab on Amazon EKS

This guide by Alian Anwar provides a comprehensive walkthrough on setting up a CI/CD pipeline for Kubernetes deployments using Jenkins and GitLab on Amazon EKS. It simplifies the deployment process, ensuring faster and more reliable software delivery.

### 📌Key Takeaways:
- **Prerequisites**: Ensure you have an Amazon EKS cluster, Docker, Kubernetes CLI (kubectl), Jenkins/GitLab Runner, and AWS CLI installed.
- **Pipeline Overview**: Automate continuous integration (CI) and continuous deployment (CD) using Jenkins or GitLab, building Docker images and deploying them to EKS.
- **Jenkins Setup**:
  - Install and configure Jenkins with necessary plugins.
  - Create a Jenkinsfile to define pipeline stages: checkout code, build Docker image, push to ECR, and deploy to EKS.
- **GitLab CI Setup**:
  - Install and configure GitLab Runner.
  - Create a .gitlab-ci.yml file to define build and deploy stages: build Docker image, push to ECR, and deploy to EKS.
- **Key Considerations**: Proper AWS IAM roles, Kubernetes RBAC, and AWS credentials management are crucial.
- **Monitoring and Scaling**: Implement monitoring tools like Prometheus and Grafana, and utilize Kubernetes Horizontal Pod Autoscaler (HPA) for automatic scaling.

## Read More

- [Automating Kubernetes Deployments: CI/CD Pipeline with Jenkins and GitLab on Amazon EKS](https://medium.com/@i210730/automating-kubernetes-deployments-ci-cd-pipeline-with-jenkins-and-gitlab-on-amazon-eks-4be9be1895ad)


# 🚀 2. Serverless with Docker: Running Containers in AWS Lambda

This guide by Alian Anwar explores the integration of serverless architectures and containerization, specifically running Docker containers in AWS Lambda. It highlights the benefits and limitations of this approach, providing insights into leveraging containers in serverless environments.

### 📌Key Takeaways:
- **Serverless Computing**: AWS Lambda allows developers to run code without managing servers, automatically handling provisioning, scaling, and maintenance.
- **Docker Containers**: Containers package applications and dependencies for consistent performance across environments, offering portability, scalability, and efficiency.
- **AWS Lambda and Docker Integration**:
  - **Create a Docker Image**: Use a Dockerfile to build container images with application code and dependencies.
  - **Upload to Amazon ECR**: Push Docker images to Amazon Elastic Container Registry (ECR) for easy storage and deployment.
  - **Deploy to AWS Lambda**: Create a Lambda function using the container image as the deployment package, benefiting from serverless scalability and management.
- **Benefits**:
  - **Enhanced Flexibility**: Custom binaries, dependencies, and runtime environments in Docker containers.
  - **Simplified DevOps**: Consistent development, testing, and production environments.
  - **Scalability and Cost Efficiency**: Automatic scaling and pay-per-use pricing.
  - **Streamlined Deployment**: Simplified deployment process for complex applications with multiple dependencies.
- **Limitations**:
  - **Cold Start Latency**: Potential additional latency when a new container instance is created.
  - **Resource Limits**: AWS Lambda's memory and execution time limits may not suit resource-intensive applications.
  - **Networking Constraints**: Potential performance impacts due to VPC configurations.
  - **Monitoring and Debugging**: Additional challenges in monitoring and debugging containerized applications.

## Read More

- [Serverless with Docker: Running Containers in AWS Lambda](https://medium.com/@i210730/serverless-with-docker-running-containers-in-aws-lambda-191927819a78)

