# 🛠️ DevOps Tooling Operations for [Sample To-Do App](https://github.com/someuser/sample-todo-app)

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
