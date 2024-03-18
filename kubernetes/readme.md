# kubernetes

## General

### Speed-ups
- **https://youtu.be/8VK9NJ3pObU?si=8-NiSu2s_akQZL34**

### Aliases
```ini
alias k='kubectl'
alias kaf='kubectl apply -f'

```


### Get Yaml Config from Running Kubernetes Service
```sh
# kubectl get <TYPE> <NAME> -o yaml
kubectl get deploy deploymentName -o yaml
```


### Run Debian from Kubernetes
```sh
# kubectl run -i --tty --image <CONTAINER>:<TAG> --restart=Never -- <POD_NAME>

kubectl run -i --tty --image debian:bookworm --restart=Never -- <POD_NAME>
```
- Reference: https://blog.flowlab.no/running-a-debian-pod-on-kubernetes-with-kubectl-beb349b40ff2

## Minikube
### Changing to the `docker` driver
```bash
minikube start --driver=docker
```

- Reference: https://minikube.sigs.k8s.io/docs/drivers/docker/

### Changing to the `qemu` driver
```sh
minikube start --driver=qemu
```

### Enabling Metrics on `minikube`
```bash
minikube addons enable metrics-server


## Virtctl


### Resources
- https://www.youtube.com/watch?v=MBvm48v43g0
- https://kubevirt.io/user-guide/virtual_machines/accessing_virtual_machines/#graphical-and-serial-console-access
- https://subscription.packtpub.com/book/cloud-and-networking/9781788294676/1/ch01lvl1sec18/connecting-to-a-running-instance-with-vnc
- https://github.com/kubevirt
- https://www.getambassador.io/blog/how-to-run-virtual-machine-vm-local-kubernetes-cluster-guide
- https://opensource.com/article/20/9/vms-kubernetes-kubevirt
- https://gist.github.com/dghubble/c2dc319249b156db06aff1d49c15272e
- https://youtu.be/8VK9NJ3pObU?si=8-NiSu2s_akQZL34
- https://github.com/ascode-com/wiki/tree/main/certified-kubernetes-administrator
