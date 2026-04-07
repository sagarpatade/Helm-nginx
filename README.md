# Day 23: Helm Package Manager & Custom Charts 

As part of my 30 Days of AWS & DevOps challenge, this project explores **Helm**, the industry-standard package manager for Kubernetes. 

The goal of this phase was to transition from writing static, manual YAML files to using dynamic templates, allowing for automated, scalable, and easily configurable application deployments.

## 🎯 Key Milestones Achieved
- Installed and configured Helm.
- Deployed public charts using the Bitnami repository.
- Mastered the Helm architecture (`Chart.yaml`, `values.yaml`, and `templates/`).
- Built a custom Helm chart from scratch.
- Dynamically injected configuration into an Nginx container using Helm templating.

## 🏗️ Architecture: The Custom Chart

I built a custom Helm chart named `helm-day-23` that deploys an Nginx web server. Instead of a static deployment, the HTML content, replica count, and network ports are fully dynamic and controlled entirely by a central `values.yaml` file.

### Directory Structure
```text
helm-day-23/
├── Chart.yaml           # Metadata and versioning
├── values.yaml          # The control panel for user-defined variables
└── templates/           # Kubernetes manifests containing {{ .Values }} placeholders
    ├── deployment.yaml  # Configures the Nginx pods and mounts the ConfigMap
    ├── service.yaml     # Configures the NodePort for local Minikube access
    └── configmap.yaml   # Dynamically generates the HTML webpage based on values.yaml


Deployment Guide
1. Start the Minikube Cluster

minikube start --driver=docker

2. Install the Custom Helm Release
Navigate to the root directory containing the my-simple-chart folder and deploy the release:

helm install my-day23-release ./helm-day-24

3. Verify the Infrastructure
Helm will automatically generate the Deployment, Service, and ConfigMap based on the provided templates.

kubectl get pods

kubectl get svc

4. Access the Application
Use Minikube's built-in tunneling to expose the dynamic NodePort service to the local browser:

minikube service my-day23-release-service
