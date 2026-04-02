# Day-52-Kubernetes-Namespaces-and-Deployments

## Task

Yesterday you created standalone Pods. The problem? Delete a Pod and it is gone forever — no one recreates it. Today you fix that with Deployments, the real way to run applications in Kubernetes. You will also learn Namespaces, which let you organize and isolate resources inside a cluster.

## Expected Output

- At least 2 namespaces created and used
- A Deployment running with multiple replicas
- A scaled Deployment and a rolling update performed
- A markdown file: day-52-namespaces-deployments.md
- Screenshot of kubectl get deployments and kubectl get pods across namespaces

 ## Challenge Tasks
 
## Task 1: Explore Default Namespaces
Kubernetes comes with built-in namespaces. List them:

kubectl get namespaces

You should see at least:

- default — where your resources go if you do not specify a namespace
- kube-system — Kubernetes internal components (API server, scheduler, etc.)
- kube-public — publicly readable resources
- kube-node-lease — node heartbeat tracking

  Check what is running inside kube-system:

  kubectl get pods -n kube-system
