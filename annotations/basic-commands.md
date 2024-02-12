## Basic Commands, Kubectl with Minikube

### Kubectl
- Kubectl is a command line tool for interacting with Kubernetes clusters.
- It allows you to run commands against Kubernetes clusters.
- You can use kubectl to deploy applications, inspect and manage cluster resources, and view logs.
- Kubectl is a powerful tool that can be used to perform a wide range of operations on Kubernetes clusters.
- Kubectl is a command line tool that is used to interact with the Kubernetes API.

### Minikube
- Minikube is a tool that makes it easy to run Kubernetes locally.
- Minikube runs a single-node Kubernetes cluster inside a virtual machine on your laptop.
- Minikube is a tool that makes it easy to run Kubernetes locally.

#### Basic Commands


#### Quicks

- `kubectl version` - Display the Kubernetes version.
- `kubectl cluster-info` - Display the cluster information.
- `kubectl get all` - List all resources in the cluster.
- `kubectl get all -A` - List all resources in all namespaces.
- `kubectl config view --minify --output 'jsonpath={..namespace}'` - See the name of the current namespace.

#### Get Commands

- `kubectl get nodes` - List all nodes in the cluster.
- `kubectl get pods` - List all pods in the cluster.
- `kubectl get pods -A` - List all pods in all namespaces.
- `kubectl get services` - List all services in the cluster.
- `kubectl get deployments` - List all deployments in the cluster.
- `kubectl get namespaces` - List all namespaces in the cluster.
- `kubectl get configmaps` - List all configmaps in the cluster.
- `kubectl get secrets` - List all secrets in the cluster.
- `kubectl get pv` - List all persistent volumes in the cluster.
- `kubectl get pvc` - List all persistent volume claims in the cluster.
- `kubectl get events` - List all events in the cluster.
- `kubectl get all` - List all resources in the cluster.

#### Describe Commands

- `kubectl describe pod <pod-name>` - Describe a specific pod.
- `kubectl describe service <service-name>` - Describe a specific service.
- `kubectl describe deployment <deployment-name>` - Describe a specific deployment.
- `kubectl describe namespace <namespace-name>` - Describe a specific namespace.
- `kubectl describe configmap <configmap-name>` - Describe a specific configmap.
- `kubectl describe secret <secret-name>` - Describe a specific secret.
- `kubectl describe pv <pv-name>` - Describe a specific persistent volume.
- `kubectl describe pvc <pvc-name>` - Describe a specific persistent volume claim.
- `kubectl describe events` - Describe all events in the cluster.
- `kubectl describe all` - Describe all resources in the cluster.
- `kubectl describe nodes` - Describe all nodes in the cluster.
- `kubectl describe all --all-namespaces` - Describe all resources in all namespaces.
- `kubectl describe all -n <namespace-name>` - Describe all resources in a specific namespace.
- `kubectl describe all -n <namespace-name> <resource-name>` - Describe a specific resource in a specific namespace.
- `kubectl describe all -n <namespace-name> <resource-name> <resource-name>` - Describe multiple specific resources in a specific namespace.

