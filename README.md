# Kubernetes-Based CI/CD and Application Monitoring System

##  Project Overview

This project demonstrates an end-to-end DevOps workflow for deploying and monitoring a containerized web application using Jenkins, Docker, Kubernetes, Prometheus, and Grafana.

The application source code is maintained in GitHub. Jenkins automates the build and deployment process, while Prometheus and Grafana are used to monitor the Kubernetes environment and application health.

## Architecture

GitHub
   ↓
Jenkins
   ↓
Docker
   ↓
Kubernetes (Minikube)
   ↓
Prometheus
   ↓
Grafana
   ↓
Alerts

## Technologies Used

- AWS EC2
- Linux
- Git & GitHub
- Jenkins
- Docker
- Kubernetes
- Minikube
- Kubectl
- Helm
- Nginx
- Prometheus
- Grafana

##  CI/CD Workflow

The CI/CD pipeline automates the process of building and deploying the application.

### Workflow

1. Developer pushes code to GitHub.
2. Jenkins checks out the latest source code.
3. Jenkins builds the Docker image.
4. Jenkins loads the Docker image into Minikube.
5. Jenkins deploys the application to Kubernetes.
6. Jenkins verifies the Kubernetes pods and service.
7. The application becomes available through the Kubernetes Service.

### Jenkins Pipeline Stages

- **Checkout** – Retrieves the source code from GitHub.
- **Build Docker Image** – Builds the application Docker image.
- **Deploy to Kubernetes** – Deploys the application using Kubernetes manifests.
- **Verify Deployment** – Checks the status of pods and services.

##  Docker

The application is containerized using Docker with Nginx as the web server.

Docker image:

`devops-monitoring:v1`

The Dockerfile:

- Uses `nginx:alpine` as the base image.
- Copies the application `index.html` into the Nginx web directory.
- Exposes port `80`.

## Kubernetes

The application is deployed on a Kubernetes cluster running with Minikube.

### Kubernetes Deployment

Deployment name:

`devops-monitoring`

The Deployment manages the application pod and ensures the required number of replicas are running.

### Kubernetes Service

Service name:

`devops-monitoring`

Service type:

`NodePort`

Application port:

`80`

NodePort:

`31131`

The Service provides access to the application running inside the Kubernetes cluster.

## 📊 Monitoring with Prometheus

Prometheus is used to collect metrics from the Kubernetes environment.

The monitoring stack was installed using Helm and includes:

- Prometheus
- Alertmanager
- Node Exporter
- Kube State Metrics
- Prometheus Operator

Prometheus acts as the metrics source for Grafana.

## 📈 Grafana

Grafana is connected to Prometheus as a data source and is used to visualize Kubernetes metrics through dashboards.

The Grafana dashboard provides information such as:

- CPU utilization
- Memory utilization
- CPU usage
- Pods
- Workloads
- Kubernetes cluster resources

A Prometheus query such as:

`up`

can be used in Grafana Explore to verify the availability of monitored targets.

## 🚨 Alerting

A Grafana alert rule was configured to monitor the health of the application pod.

### Alert Rule

`DevOps Monitoring - Application Pod Down`

The alert monitors the readiness status of the application pod using the following PromQL query:

```promql
kube_pod_status_ready{namespace="default", pod=~"devops-monitoring-.*", condition="true"}

## 📁 Project Structure

```text
kubernetes-CI-CD-monitoring/
├── Dockerfile
├── Jenkinsfile
├── deployment.yaml
├── service.yaml
├── index.html
├── README.md
└── .gitignore

## File Description

Dockerfile
Builds the Docker image for the application.

Jenkinsfile
Defines the Jenkins CI/CD pipeline.

deployment.yaml
Defines the Kubernetes Deployment.

service.yaml
Defines the Kubernetes Service.

index.html
Contains the web application.

README.md
Contains project documentation.

.gitignore
Specifies files that should not be tracked by Git.

## Key Outcomes

- Automated CI/CD pipeline using Jenkins and GitHub.
- Containerized the application using Docker.
- Deployed the application using Kubernetes.
- Implemented Kubernetes monitoring using Prometheus.
- Created Grafana dashboards for monitoring cluster resources.
- Configured Grafana alerting for application pod health.
- Integrated CI/CD and monitoring into a single DevOps workflow.

## Project Result

GitHub -> Jenkins -> Docker -> Kubernetes -> Prometheus -> Grafana -> Alerts

The project successfully demonstrates an automated deployment and monitoring workflow for a containerized application running on Kubernetes.

## Skills Demonstrated

AWS EC2, Linux, Git, GitHub, Jenkins, Docker, Kubernetes, Minikube, Kubectl, Helm, Nginx, Prometheus, Grafana, CI/CD, Monitoring, Alerting
