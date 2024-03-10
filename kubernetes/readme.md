# kubernetes

## General


## Minikube
### Changing to the docker driver
```bash
minikube start --driver=docker
```

- Reference: https://minikube.sigs.k8s.io/docs/drivers/docker/

### Enabling Metrics on `minikube`
```bash
minikube addons enable metrics-server
