# IguideME Helm Deployment

Deploy **IguideME** as an all-in-one service on Kubernetes using Helm.

Before you begin, update your `values.yaml` file with the correct settings for your Canvas environment and set secure passwords for all sensitive values.

---

## Prerequisites

1. **Kubernetes cluster**
   - For local development, you can start a cluster with [Minikube](https://minikube.sigs.k8s.io/):
     ```bash
     minikube start
     ```

2. **Helm installed**
   - Follow the official [Helm installation guide](https://helm.sh/docs/intro/install/) if you don’t already have it.

3. **Private package access**
   Since images are hosted on GitHub Container Registry, you must configure authentication:

   ```bash
   kubectl create secret docker-registry ghcr-secret \
     --docker-server=ghcr.io \
     --docker-username=YOUR_USERNAME \
     --docker-password=YOUR_PAT \
     --namespace default
   ```

   Replace YOUR_USERNAME with your GitHub username and YOUR_PAT with a personal access token.

## Installation

1. Check if an IguideME release already exists:
   ```bash
   helm list --all-namespaces
   ```

2. Install (or upgrade) the chart from the folder with the `Chart.yml` you're targetting:
   ```bash
   helm upgrade --install iguideme .
   ```

3. Verify that the Pods are running:
   ```bash
   kubectl get pods
   ```

## Uninstallation & Cleanup

To remove IguideME:
```bash
helm uninstall iguideme
```

To force a complete Pod rebuild (use with caution):
```bash
kubectl delete pod --all --grace-period=0 --force
```

## Accessing Services Locally (Minikube)
1. List services:
   ```bash
   kubectl get svc
   ```
2. Forward ports:
   - API service → http://localhost:8000
     ```bash
     kubectl port-forward svc/api 8000:8000
     ```
   - Frontend → http://localhost:3000
     ```bash
     kubectl port-forward svc/frontend 3000:3000
     ```
