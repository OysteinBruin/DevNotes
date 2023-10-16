## Helm
[Helm](https://helm.sh/) is a tool for managing Kubernetes charts. Charts are packages of pre-configured Kubernetes resources.  
 Helm charts are packages of Kubernetes resources which are installed into a Kubernetes cluster as a unit. Helm templates, which make up a chart, separate the definition of a resource, which is largely static, from its configuration, which may differ with each installation.

---
### Installation

1. Install chocolatey if it's not already done  ([chocolatey.md](../windows/chocolatey.md))
2. run `choco install kubernetes-helm`

- Verify installation:

```powershell
# display a listing of available commands
helm

# installed version
helm version --short

```

---

Helm three is not configures to use any repository.
Install the official helm repo
`helm repo add stable https://charts.helm.sh/stable`

Install a mysql demo in the cluster
`helm install demo-mysql stable/mysql`


`kubectl get all | ggrep mysql`

