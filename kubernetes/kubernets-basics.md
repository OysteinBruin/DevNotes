## Kubernetes Basics
[Kubernetes](https://kubernetes.io/docs/concepts/overview/) is a portable, extensible, open source platform for orchestrating containers. It manages the lifecycle and networking of containers that are scheduled to run, so you don't have to worry if your app crashes or becomes unresponsive - Kubernetes will automatically tear it down and start a new container.

---
From the great blog series [Andrew Lock | .NET Escapades - An Introduction to Kubernetes](https://andrewlock.net/deploying-asp-net-core-applications-to-kubernetes-part-1-an-introduction-to-kubernetes/) :
### Basic Kubernetes components

#### Nodes
Nodes in a Kubernetes cluster are Virtual Machines or physical hardware. It's where Kubernetes actually runs your containers. There are typically 2 types of Nodes:

- The master node, which contains all the "control plane" services required to run a cluster. Typically the master node only handles this management access, and doesn't run any of your containerised app workloads.

- Other nodes, which are used to run your applications. A single node can run many containers, depending on the resource constraints (memory, CPU etc) of the node.

#### Pods
tl;dr; Pods are a collection of containers that Kubernetes schedules as a single unit. Initially your pods will likely contain a single container, one for each API or app you're deploying.

#### Deployments
tl;dr; Deployments are used to define how Pods are deployed, which Docker images they should use, how many replicas should be running, and so on. They represent the desired state for the cluster, which Kubernetes works to maintain.

Sample deployment manifest file:
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment
  labels:
    app: nginx
spec:
  replicas: 3
  strategy: 
    type: RollingUpdate
    rollingUpdate:
      maxUnavailable: 1
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx
        image: nginx:1.7.9
        ports:
        - containerPort: 80
```

#### Services
tl;dr; Services are internal load balancers for a set of identical pods. They are assigned DNS records to make it easier to call them from other pods in the cluster.

Sample service manifest file:
```yaml
```

#### Ingress
tl;dr; Ingresses are used to expose services at HTTP endpoints. They act as reverse proxies for your services, load-balancing requests between different services running on different nodes.

Sample ingress manifest file:
```yaml
```
---