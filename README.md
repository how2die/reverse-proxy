# Reverse Proxy

Reverse proxy using [Træfik](https://traefik.io/) as an ingress controller.

## Getting started

Based on the [official guide](https://docs.traefik.io/user-guide/kubernetes/) and [this guide](https://medium.com/@dusansusic/traefik-ingress-controller-for-k8s-c1137c9c05c4).

### Prerequisites

* A Kubernetes cluster
* kubectl

### Namespace

Create a dedicated namespace:

```
kubectl create namespace traefik
```

### TLS Secret

Create a TLS certificate:

```
openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout ./tls.key -out ./tls.crt -subj "/CN=*.how2die.com"
```

Create a secret object:

```
kubectl create secret tls traefik-ui-tls-cert --key ./tls.key --cert ./tls.crt
```

### Security

For the sake of simplicity, use a ClusterRoleBinding for privileges

```
kubectl apply -f traefik-rbac.yaml
```

### Configuration

Configure Træfik to use HTTPS (generated by Let's Encrypt), and redirect HTTP traffic to HTTPS

```
kubectl apply -f traefik-config.yaml
```

### Deployment

```
kubectl apply -f traefik-deployment.yaml
```

A traefik-ingress-controller pod should now be running. Confirm by typing

```
kubectl get pods
```

You should also be able to see the service

```
kubectl get services
```

Remember to route HTTP (80) and HTTPS (443) traffic to the ports exposed by traefik-ingress-service

### Ingress

Write ingress rules to *ingress.yaml* and apply

```
kubectl apply -f ingress.yaml
```
