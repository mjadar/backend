# KUBERNETES

https://www.youtube.com/watch?v=s_o8dwzRlu4

## What is Kubernetes

- is an open source container orchestration tool
- developed by Google
- helps manage containerized applications in different deployment environments

## What problems does Kubernetes solve

- trend from Monolith to Microservices
- increased usage of containers
- demand for a proper way of managing hundreds of containers

## What features do orchestration tools offer

- high availability or no downtime
- scalability or high performance
- disaster recovery (backup and restore)

## Kubernetes Architecture

- 1 master node connected to **worker nodes**
- each worker node has a Kubelet process that let the worker nodes communicate with each others, and execute some tasks on these nodes.
- applications are running on worker nodes
- the master node runs several kubernetes processes that are necessary to manage the cluster of nodes properly.
- eg of kubernetes processes run on master are :
  - `API Server` = Entrypoint to K8s cluster
  - `Controller Manager` = keeps track of what is happening in the cluster
  - `Scheduler` = decides on which node new container will be scheduled on based on the available resources on the worker node and the load the container needs.
  - `etcd` = Kubernetes backing store, holds at any time the current state of kubernetes cluster.
- (look at associated picture on the folder Kubernetes-architecture.PNG)

## Node and Pod

- [Node] = virtual or physical machine
- [Pod] = smallest unit in Kubernetes, Abstraction over container. Kubernetes create an abstraction layer on top of container
- [Pod] usually meant to run 1 application per Pod.
- **How these Pod communicates between each other** ?
  - in a virtual network each pod gets its own IP address
  - Pods are ephemeral, can die easilly
  - if a pod dies, upon re-creation it gets assigned a new IP address, which is not good in the case of databases for example (you have to adjust url every time)
    - Thats why anoter component called **service** is used

## Service and Ingress$

- [Service] :

  - is a static IP address that will be assigned to each pod.
  - lifecycle of POD and Service are not connected.
  - App should be accessible through browser, so we define an external service or internal service.

a result of service is just url with port, but we want secure communication with domain, etc ... For that we use Ingress.

- [Ingress] :
  - instead of service, the request go first to ingress, and it does the forwarding to the service.

## ConfigMap and Secret

- used to store data externally, and avoid store it in app inside container to avoid rebuild each time.

## Volumes

- it basically attaches a physical storage on local machineor remote, outside of the K8S cluster.
- Though data is persisted.

## Deployment and statful states

manage replication

## Kubernetes Configuration

- all the K8S configuration goes from the Master
