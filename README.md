Sure, here is a README.md file for the repository `simple-nginx-deployment-kubernetes`:

```markdown
# Simple NGINX Deployment on Kubernetes

This repository contains the configuration files for deploying a simple NGINX application on a Kubernetes cluster.

## Prerequisites

- Kubernetes cluster
- kubectl configured to interact with your cluster
- Docker
- Git

## Getting Started

### 1. Clone the Repository

```bash
git clone https://github.com/bungyan-cyber/simple-nginx-deployment-kubernetes.git
cd simple-nginx-deployment-kubernetes
```

### 2. Build and Push Docker Image

1. Build the Docker image:

```bash
docker build -t <your-dockerhub-username>/simple-nginx:latest .
```

2. Push the Docker image to Docker Hub:

```bash
docker push <your-dockerhub-username>/simple-nginx:latest
```

### 3. Update Kubernetes Deployment

1. Open the `deployment.yaml` file and update the image field with your Docker Hub image:

```yaml
containers:
  - name: nginx
    image: <your-dockerhub-username>/simple-nginx:latest
```

### 4. Deploy to Kubernetes

1. Apply the deployment and service configuration:

```bash
kubectl apply -f deployment.yaml
kubectl apply -f service.yaml
```

### 5. Verify Deployment

1. Check the status of the pods:

```bash
kubectl get pods
```

2. Check the service:

```bash
kubectl get services
```

### 6. Access the NGINX Application

1. Get the external IP address of the service (if using a LoadBalancer service):

```bash
kubectl get svc simple-nginx
```

2. Open a web browser and navigate to the external IP address.

## Repository Structure

- `Dockerfile`: Dockerfile for building the NGINX image
- `deployment.yaml`: Kubernetes deployment configuration for NGINX
- `service.yaml`: Kubernetes service configuration for NGINX

## Cleanup

To remove the deployment and service:

```bash
kubectl delete -f deployment.yaml
kubectl delete -f service.yaml
```

## Contributing

Feel free to open issues or submit pull requests for any improvements or bug fixes.

## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.
```

Replace `<your-dockerhub-username>` with your actual Docker Hub username. This README.md file provides a comprehensive guide for setting up and deploying a simple NGINX application on a Kubernetes cluster.
