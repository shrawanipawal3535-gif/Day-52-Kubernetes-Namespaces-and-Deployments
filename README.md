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

<img width="639" height="176" alt="Image" src="https://github.com/user-attachments/assets/34fbebf1-f4cd-4df1-a4ee-dd7cb883e4be" />

You should see at least:

- default — where your resources go if you do not specify a namespace
- kube-system — Kubernetes internal components (API server, scheduler, etc.)
- kube-public — publicly readable resources
- kube-node-lease — node heartbeat tracking

Check what is running inside kube-system:

kubectl get pods -n kube-system

 <img width="907" height="198" alt="Image" src="https://github.com/user-attachments/assets/25b27a63-4960-40ea-a3e9-35293d123bbd" />

## Task 2: Create and Use Custom Namespaces

Create two namespaces — one for a development environment and one for staging:

kubectl create namespace dev
kubectl create namespace staging

Verify they exist:

kubectl get namespaces

You can also create a namespace from a manifest:

kubectl apply -f namespace.yaml

Now run a pod in a specific namespace:

kubectl run nginx-dev --image=nginx:latest -n dev
kubectl run nginx-staging --image=nginx:latest -n staging

List pods across all namespaces:

kubectl get pods -A

