Create a secret for the image pull policy:

```bash
kubectl create secret docker-registry ghcr-secret \
  --docker-server=ghcr.io \
  --docker-username=YOUR_USERNAME \
  --docker-password=YOUR_PAT \
  --namespace default
```

minikube start
helm list --all-namespaces
helm upgrade --install iguideme .
kubectl get pods

helm uninstall iguideme
kubectl delete pod --all --grace-period=0 --force

kubectl get svc
kubectl port-forward svc/api 8000:8000
kubectl port-forward svc/frontend 3000:3000