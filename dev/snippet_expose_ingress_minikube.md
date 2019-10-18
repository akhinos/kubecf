
### Option 2: NGINX Ingress Controller

```sh
helm install stable/nginx-ingress \
  --name ingress \
  --namespace ingress
```

#### For Minikube

Pass the flag `--set "controller.service.externalIPs={$(minikube ip)}"` to the `helm install` in
order to assign the external IP to the Ingress Controller service.
