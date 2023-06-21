# Flux CD
### GitOps:
- GitOps stands for "Git Operations" or "Git Operations Paradigm."
- In the context of GitOps, the term "operations paradigm" refers to a set of principles and practices that guide the management and operation of applications and infrastructure. It represents a specific approach or methodology for handling operations-related tasks.
- GitOps is a methodology for managing and automating the deployment and operation of applications and infrastructure in a declarative and version-controlled manner using Git as the single source of truth. It aims to bring the principles of software development, such as version control, collaboration, and code review, to the domain of infrastructure and operations.
- In the GitOps methodology, the desired state of the system is defined and stored in a Git repository. This includes the configuration, application code, and infrastructure specifications. Any changes to the desired state are made through Git commits, following a pull-based model.
  - **Declarative Infrastructure**: The desired state of the system is declared using configuration files, which are version-controlled in a Git repository. This allows for reproducibility and auditability of the infrastructure.
  - **Git as a Single Source of Truth**: The Git repository serves as the single source of truth for the system's desired state. It includes all the configuration files, application code, and any other resources required for the deployment and operation of the system.
  - **Pull-based Continuous Deployment**: The system's desired state is continuously monitored by a GitOps tool, such as Flux CD. When changes are detected in the Git repository, the tool pulls the changes and automatically applies them to the target environment. This ensures that the actual state of the system aligns with the desired state.
  - **Automated Synchronization**: GitOps tools reconcile the actual state of the system with the desired state by automatically applying any changes made in the Git repository. This automated synchronization eliminates the need for manual interventions and reduces the chances of configuration drift.
  - **Rollback and Auditing**: Since all changes are version-controlled in Git, it becomes straightforward to roll back to a previous known state in case of issues or failures. Additionally, Git provides a complete audit trail of all changes, enabling easy traceability and accountability.
### Flux CD:
- Flux CD (Continuous Delivery) is an open-source tool used for automating the deployment and lifecycle management of applications and infrastructure in Kubernetes clusters. It follows the GitOps methodology, where the desired state of the system is declared and version-controlled in a Git repository. Flux CD monitors this repository for changes and reconciles the cluster's state with the desired state, ensuring that applications and configurations are automatically deployed and kept in sync.
- Key features of Flux CD include:
  - GitOps Workflow: Flux CD uses the GitOps approach, allowing you to manage your Kubernetes resources and configurations through Git repositories. This promotes declarative and auditable infrastructure management.
  - Automated Deployment: Flux CD monitors the desired state of your applications and infrastructure stored in the Git repository. When changes are detected, it automatically deploys and updates the resources in your Kubernetes cluster.
  - Continuous Delivery: With Flux CD, you can achieve continuous delivery by automating the deployment pipeline. It integrates with CI/CD systems, such as Jenkins or GitLab CI, to trigger deployments based on the changes made to the Git repository.
  - Release Management: Flux CD supports multiple environments and release strategies, allowing you to manage different stages of your application's lifecycle. You can define specific rules and policies for deploying new versions or promoting releases across different environments.
  - Automated Rollbacks: In case of failures or issues, Flux CD enables automated rollbacks by reverting to the last known good state. This helps in maintaining the stability of your applications and reducing downtime.
  - Multi-Cluster Management: Flux CD can manage multiple Kubernetes clusters, making it suitable for complex environments with distributed applications and multiple teams.
- Flux CD has gained popularity in the Kubernetes ecosystem as a reliable tool for implementing GitOps workflows and automating continuous delivery. It simplifies the deployment and management of applications, ensuring that your Kubernetes cluster remains in sync with your desired state defined in the Git repository.

### [Manage Helm Releases](https://fluxcd.io/flux/guides/helmreleases/) 

## [How to connect a new or pre-existing cluster with github repo using FluxCD](https://fluxcd.io/flux/installation/)

### Resources:
- [Getting Started](https://fluxcd.io/flux/get-started/)
- [Flux for Helm Users](https://fluxcd.io/flux/use-cases/helm/)