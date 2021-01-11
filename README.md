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

### configuration
