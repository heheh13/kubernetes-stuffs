# Kubernetes

Kubernetes is a production-grade, open-source platform that orchestrates the placement (scheduling) and execution of application containers within and across computer clusters.

what kubernetes is?

what is a cluster?

what is a container?

Nodes, Pods, Services?

## Kubernetes as a user

### Create a cluster

`minikube start | kind create cluster`

`kubectl cluster-info`

`kubectl get nodes`

### deploying

A Deployment is responsible for creating and updating instances of your application

`kubectl get nodes`

`kubectl create deployment <name> --image=<imageLocation>`

`kubectl get deployment`

### exploring

`kubectl get pod`

`kubectl describe pod`
`kubectl port-forward <pod> <port>` established a connection between localhost and kubernetes api server.

### exposing

`kubectl expose deployment/<deployment> --type="NodePort" --port 8080` expose a node port services
`kubectl describe services/<serviceName>`

`curl <cluster internal ip>:<node_port>` to hit the base url
`kubectl delete service <name>`

### scaling

`kubectl scale deployment/<deployment> --replicas=<numberOfReplica>`

`kubectl get pods -o wide`

### updating

`kubectl set image deployment/<deploymentName> <deploymentName>=<image>`
`kubectl rollout undo deployment/<deploymentName>`

-----------

## Kubernetes Docs

### overview

### working with k8s objects

### Namespaces

Kubernetes supports multiple virtual clusters backed by the same physical cluster. These virtual clusters are called namespaces.

`kubectl run nginx --image=nginx --namespace=<insert-namespace-name-here>`

`kubectl get pods --namespace=<insert-namespace-name-here>`

`kubectl config set-context --current --namespace=<insert-namespace-name-here>` sets as default namespace

`kubectl config view --minify | grep namespace:`

`kubectl api-resources`

## label and selector

Labels are intended to be used to specify identifying attributes of objects.labels allows you to query and watch.

selectors allows you to  filter based on labels
two types of selector equality based , set based
equality based : env = prod, tier !=frontend

    environment in (production, qa)
    tier notin (frontend, backend)
    partition
    !partition
both can be mixed like:  partition in (customerA, customerB),environment!=qa.

`kubectl get pods -l environment=production,tier=frontend`

`kubectl get pods -l 'environment in (production),tier in (frontend)'`

## annotations

used to attach arbitrary metadata to objects

## field selector

allows you to query over k8s objects
kubectl get pods --field-selector status.phase=Running

## recommended label

`app.kubernetes.io/name : 'name'`

## cluster architecture

## Nodes

Nodes are responsible for running containers inside pods .It can be a vm or physical machine. There can be several nodes in cluster. A node consists of kubelet, kube-proxy and a container runtime.

`kubectl describe node <insert-node-name-here>`

`kubectl get node <nodeName> -o yaml`

## Node controller

a control plane component of k8s api server.

    * register to CIDR ??
    * kept to list of nodes up to date 
    * monitoring nodes' health

## Control Plane

The connection between nodes and the api server are secured by default they maintain some sorts of certification during communication.

kubelets provide the port forwarding functionality and responsible for fetching logs and running pods.

** need to provide some sorts of certification to established a secure connections.

## controllers

watch the states of cluster and make or request changes if needed.

There can be several controllers that create or update the same kind of object. Behind the scenes, Kubernetes controllers make sure that they only pay attention to the resources linked to their controlling resource.

## Cloud control manager

let you link your cluster and cloud provider api server.

Components:

        Node controller
        Route controller
        Service controller
