# Keycloak Deployment for GKE

This repository contains the configuration files for deploying keycloak in kubernetes cluster. Keycloak is an open-source identity and access management solution that provides authentication and authorization services.

## Project Structure

- **k8s/**
    - **base/** - Contains the base kubernetes manifest for keycloak and associated components.
    - **overlays/** - Contains environment-specific configurations and overrides.
- **Readme.md** - Project documentation.

## Keycloak Features

- **Authentication:** secure login for applications and services.
- **Authorization:** Role based access control.
- **Single Sign-On:** Enables users to log in once and access multiple applications.
- **Federated Identity:** Integration with external identity providers.
- **User Management:** Self-service user registration, login and account creation.

## Prerequisites

Before deploying keycloak, ensure you have the following:
- **Kubernetes Cluster:** A running kubernetes cluster.
- **Kubectl:** Kubernetes command-line tool configured to communicate with the cluster
