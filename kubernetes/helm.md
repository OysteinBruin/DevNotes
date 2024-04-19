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


`kubectl get all`

Cleanup  
`helm uninstall demo-mysql`

Environment variables  
`helm env`

### Helm commands  
![Helm commands image](/_img/helm/helm-commands.png)

Test helm templates before installing charts, 2 ways:   
![Helm commands image](/_img/helm/helm-test-commands.png)

### Helm templates

- helm template values:
    - Access by {{.Values.property-name.sub-property-name}}
    - Ways to define values:
        - helm install--set key=value
        - values.yaml
        - other-file.yaml (helm install -f other-file.yaml)
    - a defined sche,a with values.schema.json in the root to validate values.yaml gives error if values are not valid when running helm install

- values from built-in object:
    - .Release (from releases runtime data)
    - .Chart (data from chart file)
    - .Capabilities (kubernetes cluster data)

```powershell	
# show values computed by helm
helm get all release-name
```	