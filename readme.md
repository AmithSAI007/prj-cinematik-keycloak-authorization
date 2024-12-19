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

## Deployment

Follow the steps below to deploy keycloak to your kubernetes cluster.

**1. Clone the Repository**
```bash
    git clone git@github.com:AmithSAI007/prj-cinematik-keycloak-authorization.git
    cd prj-cinematik-keycloak-authorization
```

**2. Configure Kubernetes Secerts**

Keycloak requires some secrets for its configuration, such as admin username and password. You can create the necessary secrets using the following commands.

```bash
    kubectl create secret generic keycloak-secrets \
      --from-literal=KC_BOOTSTRAP_ADMIN_USERNAME=admin \
    --from-literal=KC_BOOTSTRAP_ADMIN_PASSWORD=admin_password \
    --from-literal=KC_DB_USERNAME=keycloak_user \
    --from-literal=KC_DB_PASSWORD=db_password \
    -n default
```

**3. Create TLS Secret for HTTPS**

Keycloak can be accessed securely over HTTPS using a TLS certificate. Create the `keycloak-tls-secret`

```bash
    kubectl create secret tls keycloak-tls-secret \
      --cert=/path/to/tls.crt \
      --key=/path/to/tls.key \
      -n default
```

**4. Apply the Kubernets Manifest**

To deploy keycloak apply the kubernetes resources:

```bash
    kubectl apply -k k8s/overlays/production
```

**5. Verify Deployment**

Check the status of the deployment.

```bash
    kubectl get pods -n default
    kubectl get svc -n default
    kubectl get ingress -n default
```

**6. Access Keycloak**

Once the deployment is successful, access the keycloa via your browser.

- URL: `https://houseofllm.com/auth/admin`
- Admin Console: `https://houseofllm.com/auth/admin/master/console/`

Login with admin credentials you set in the secrets.

## Troubleshooting

- **Ingress Issues:** If the health check fail, ensure the backend service is exposing the health check port (`9000`) and verify that your DNS is correctly pointing to the external IP.
- **TLS Issues:** If you encounter SSL errors, verify that the `keycloak-tls-secret` contains valid certificates and the secret is correctly references in the ingress.

## Security Considerations

- **Secrets Management:** Ensure sensitive data (e.g. passwords, certificates) are managed securely. Use tools like `Vault` for secret management in production environments.
- **Ingress Security:** For production environments, ensure that the ingress controller is properly secured and configure additional security features such as rate-limiting and whitelisting.

## Additional Configuration

- **Database Configuration:** Keycloak can be configured to use diffrent database (e.g., PostgreSQL, MySQL). You can update the `keycloak-configmap` to specify the database connection settings.
- **Scaling:** To scale keycloak, update the `Statefulset` replica count or use helm for better control over scaling and upgrades.

## Contribution

Contriubtions are welcome! Please follow the steps to contribute.
1. Fork the repository.
2. Create a new branch for your changes.
3. Commit your changes with clear and concise commit messages.
4. Push your changes and open a pull request.

## License

This project is licensed under **MIT License**.
