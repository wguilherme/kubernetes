## Basic behavior in Kubernetes Networking

### Basic Networking in Docker

With docker, we've learned that ideally, each service must be created in your own container.

For example, if we have a web application and a database, we would have two containers, one for the web application and another for the database.

Each docker container have your own IP address for each container. And them can communicate with each other using the IP address, because they are in the same network, created by docker.

### Basic Networking in Kubernetes

Resume:

- The cluster born with two IP adresses, one for the own cluster and another for api server.
- The API server address is the address that generally used to access from SSH.

```bash
kubectl get service kubernetes # show cluster-ip, port and age
kubectl cluster-info # show the cluster ip and the api server address
kubectl describe service kubernetes # show the cluster ip and the api server address (generally in Endpoints)
```

In Kubernetes, the networking fundamentals are akin to Docker, albeit with notable distinctions.

- In docker, `each container` receives an IP address.
- In Kubernetes, `each pod` receives an IP address.

To see the IP address of a pod, you can use the following command:

```bash
kubectl get pods <name>
kubectl get pods <name> -o wide # show the ip address of each pod in key IP or IPs
```

### IP Classes in Kubernetes:

- **ClusterIP**: IP class: A - Range: 0.0.0.0 to 127.255.255.255
- **PODs**: IP class: B - Range:  128.0.0.0 to 191.255.255.255
- **Nodes**: IP class: C - Range:  192.0.0.0 to 223.255.255.255

PS: It is important to note that, with the advent of CIDR, IP addresses are no longer rigidly assigned to fixed classes, and subnet prefixes can be used flexibly to allocate IP addresses in a more efficient and scalable manner.