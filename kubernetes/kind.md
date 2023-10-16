## Kind
[Kind](https://kind.sigs.k8s.io/) is a tool for running local Kubernetes clusters using Docker container “nodes”.
kind was primarily designed for testing Kubernetes itself, but may be used for local development or CI.

---
### Installation

1. Install chocolatey if it's not already done ([chocolatey.md](../windows/chocolatey.md))
2. run `choco install kind`

- Verify installation:

```powershell
choco -?
```
should display a listing of available commands

---
### Demo - deploy a sample application on a local Kubernetes cluster for development and testing

1. Create a new k8s cluster:

```powershell
kind create cluster --name my-kubernetes-app
```

2. Verify your k8s cluster:

```powershell
kubectl get all -A
# or
kubectl cluster-info --context kind-my-kubernetes-app
```
3. Using [helm](helm.md) and [bitnami](https://github.com/bitnami/charts) to deploy a ready to launch application:

```powershell
#Add Helm Repo
helm repo add bitnami https://charts.bitnami.com/bitnami

#Update Helm Repo
helm repo update

#Deploy WordPress Application
helm install myapp bitnami/wordpress

#List your Helm Chart
helm list
```

4. Run kubectl port forwarding to be able to view the app in your browser:

```powershell
#Get Pod name 
kubectl get pods

#Port forwarding 
kubectl port-forward <pod name> 8080:8080
```

Access the app in a browser on http://localhost:8080

5. Cleanup
```powershell
#uninstall helm chart
helm uninstall myapp

#delete helm repo
helm repo remove bitnami

#delete kind cluster
kind delete cluster --name my-k8s-app
```

---
### Demo - deploy a local docker image

1. Follow step 1. and 2. above
2. Loading an Image Into Your Cluster
```powershell
kind load docker-image my-custom-image-0 my-custom-image-1 --name my-kubernetes-app
```

3. Run kubectl port forwarding to be able to view the app in your browser:

```powershell
#Get Pod name 
kubectl get pods

#Port forwarding 
kubectl port-forward <pod name> 8080:8080
```

Access the app in a browser on http://localhost:8080

5. Cleanup
   Follow step 5. above


kind load docker-image test-img:1.0 --name test-cluster
