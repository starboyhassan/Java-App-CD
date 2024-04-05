# Continuous Deployment (CD) Pipeline for Java application on AWS EKS cluster

## Overview
The Continuous Deployment (CD) pipeline automates the deployment process of our application to Kubernetes clusters. Upon successful completion of the Continuous Integration (CI) pipeline, the CD pipeline is triggered to deploy the application changes to the target environment.

- For more details about CI: [CI Repo](https://github.com/starboyhassan/Java-App-CI)
---
## Tools
- **ArgoCD**: Continuous delivery tool for managing Kubernetes deployments.
- **kubectl**: Command-line tool for interacting with Kubernetes clusters.
- **Prometheus and Grafana**: Monitoring tools for tracking application metrics and performance.
---
## Deployment Process
- **Trigger**: The CD pipeline is triggered automatically after the CI pipeline successfully builds and tests the application.
- **Update Deployment Manifests**: The CD pipeline updates Kubernetes deployment manifests with the new Docker image tag from the Elastic Container Registry (ECR).
- **Sync with ArgoCD**: The updated deployment manifests are pushed to the CD repository, triggering ArgoCD to sync with the Kubernetes cluster and apply the changes.
- **Monitoring**: Prometheus and Grafana provide monitoring and observability for the deployed application.

---
## ArgoCD Deployment 
- ArgoCD plays a pivotal role in managing the deployment of our application to Kubernetes clusters. It ensures that the desired state of the cluster matches the configuration stored in the Git repository. By continuously monitoring the Git repository for changes, ArgoCD automates the deployment process, reducing manual intervention and ensuring consistency across environments.

## Monitoring and Observability
- **Prometheus**: Collects metrics from the deployed application, including performance metrics, resource utilization, and error rates.
- **Grafana**: Visualizes metrics collected by Prometheus and provides customizable dashboards for monitoring application performance. Grafana's flexible querying and visualization capabilities enable teams to gain insights into application behavior and diagnose issues effectively.




