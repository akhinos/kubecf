# Foundation: Kube

A kube cluster is the foundation for deploying Helm, the CF operator
and Kubecf for development.

For local development Minikube and Kind (Kube IN Docker) are suitable,
the latter with some limitations.

In the cloud `GKE` (Google Kubernetes Engine) is one of several
suitable providers.

For more detailed instructions see the table below.

| flavor   | instructions                             |
| -------- | ---------------------------------------- |
| minikube | [minikube/README.md](minikube/README.md) |
| kind     | [kind/README.md](kind/README.md)         |
| gke      | [gke/README.md](gke.md)                  |
