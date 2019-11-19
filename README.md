# Reverse Proxy

Reverse proxy using [Træfik](https://traefik.io/) as an ingress controller.

## Getting started

Based on the [official guide](https://docs.traefik.io/user-guide/kubernetes/).

### Prerequisites

* A Kubernetes cluster
* kubectl

### Namespace

Create a dedicated namespace:

```
kubectl create namespace traefik
```

### Custom resource definitions

Install custom resource definitions used by Traefik:

```
kubectl apply -f resource-definitions.yaml
```

### Security

For the sake of simplicity, use a ClusterRoleBinding for privileges

```
kubectl apply -f rbac.yaml
```

### Deployment

```
kubectl apply -f deployment.yaml
```

A traefik-ingress-controller pod should now be running. Confirm by typing

```
kubectl -n traefik get pods
```

You should also be able to see the service

```
kubectl -n traefik get services
```

Remember to route HTTP (80) and HTTPS (443) traffic to the ports exposed by traefik-ingress-service

### Ingress

Write ingress rules to *ingress.yaml* and apply

```
kubectl apply -f ingress.yaml
```
