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



### Cluster Architecture
- 


### ETCD
- Distributed reliable key-value store
- Typically runs on port `2379`




### Kubernetes Interfaces
- The following are Interfaces are:
  - CRI : Container Runtime Interface ~ work with container interfaces
	- Examples: `docker`, `rkt`, `cri-o`
  - CNI : Container Network Interface ~ work with network interface
	- Examples: `weaveworks`, `flannel`, `cilium`
  - CSI : Container Storage Interface 
	- Examples: `amazon ebs`, `glusterfs`
	- Not a kubernetes standard, it's a universal standard. RPCs that follow a specification for CSIs



### Data Visualization Manipulation in `kubectl`
#### Custom Columns
- Columns are created around the json output
  - Do `k -n <NAMESPACE> get <RESOURCE> -o json`, ex: `k -n aground get deploy -o json`

```
k -n aground get deploy -o custom-columns="DEPLOYMENT:metadata.name,IMAGE:.spec.template.spec.containers[0].image,READY_REPLICAS:status.replicas,NAMESPACE:metadata.namespace"
```

### Json Path Example in `kubectl`
- `$` is not mandatory as kubectl adds it.
  - `kubectl get pods -o=jsonpath='{ .items[0].spec.containers[0].image }'`

You can also do:
  - `kubectl get pods -o=jsonpath='{ .items[0].spec.containers[0].image } {"\n"} {.items[*].capacity.cpu}'` (rows)
  - `kubectl get pods -o=jsonpath='{range .items[*]}{.spec.containers[0].image } {"\t"} {.capacity.cpu}{"\n"}{end}'` (columns)
  - Use custom-columns instead of loop when working with columns

### kube-config show different output
- If `~/.kube/config`, you can view the output differently via: `kubectl config view --kubeconfig=~/.kube/config -o json`

- Get a nested value: ` k config view --kubeconfig=~/.kube/config -o jsonpath='{ .contexts[?(.context.user=="dara")] 
}' | jq`
```json
{
  "context": {
    "cluster": "closed-based",
    "user": "dara"
  },
  "name": "dara@closed-based"
}
```

### `Sort-by` option in `kubectl`
- :x: `k get pv --sort-by=.items[*].spec.capacity.storage`
: :heavy_check_mark: `k get pv --sort-by=.spec.capacity.storage`


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
