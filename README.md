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

<img width="901" height="111" alt="Image" src="https://github.com/user-attachments/assets/c3462378-595e-4b99-b333-9203d4729f75" />

Verify they exist:

kubectl get namespaces

<img width="779" height="184" alt="Image" src="https://github.com/user-attachments/assets/703df4ca-e85d-483d-b31f-c3d1fd1f4839" />

You can also create a namespace from a manifest:

<img width="505" height="120" alt="Image" src="https://github.com/user-attachments/assets/23a5f334-3cb2-4e74-b1d8-376bb6ea1e5e" />

kubectl apply -f namespace.yaml

<img width="809" height="42" alt="Image" src="https://github.com/user-attachments/assets/1f29de83-2d42-4505-be80-22c1815ca6e9" />

Now run a pod in a specific namespace:

kubectl run nginx-dev --image=nginx:latest -n dev

kubectl run nginx-staging --image=nginx:latest -n staging

<img width="965" height="82" alt="Image" src="https://github.com/user-attachments/assets/4d496fd8-8c38-485f-8f74-38ffd35ef42f" />

List pods across all namespaces:

kubectl get pods -A

<img width="1093" height="504" alt="Image" src="https://github.com/user-attachments/assets/21711cd7-b934-4555-94a0-e614ba2e7893" />

## Task 3: Create Your First Deployment

A Deployment tells Kubernetes: "I want X replicas of this Pod running at all times." If a Pod crashes, the Deployment controller recreates it automatically.

Create a file nginx-deployment.yaml:

Key differences from a standalone Pod:

- kind: Deployment instead of kind: Pod
- apiVersion: apps/v1 instead of v1
- replicas: 3 tells Kubernetes to maintain 3 identical pods
- selector.matchLabels connects the Deployment to its Pods
- template is the Pod template — the Deployment creates Pods using this blueprint

Apply it:

kubectl apply -f nginx-deployment.yaml

<img width="1019" height="52" alt="Image" src="https://github.com/user-attachments/assets/26effa56-4fc6-44b2-8147-cf54561ee90e" />

Check the result:

kubectl get deployments -n dev

<img width="991" height="217" alt="Image" src="https://github.com/user-attachments/assets/d730f4fe-62a6-491a-a3dd-6f6160f52728" />

kubectl get pods -n dev

<img width="951" height="160" alt="Image" src="https://github.com/user-attachments/assets/5eda8442-9006-4756-acba-50c824d4a0a2" />





