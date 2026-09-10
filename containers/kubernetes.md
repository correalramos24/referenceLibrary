# Kubernetes

Used to scale docker containers (for 10-20 or more instances) and orchestrate it!

The kubernetes cluster scheduler puts the pots into the cluster workers.

## Kubernetes components

Control plane: API + scheduler services + etcd DBs + cloud controller manager

Node(s): Runs the kubelet (worker service) and the k-proxy (re-route traffic)

kubectl: controler of the cluster, client

