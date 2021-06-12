class: middle, center

# Getting Started with Kubernetes

---

# Agenda

- Kubernetes overview
	* Containers overview
	* Kubernetes architecture
- Kubernetes concepts (and a lot of YAML)
	* Pods
	* ReplicaSets
	* Deployments
- Networking in Kubernetes
- Services

---
class:  middle, center

### To understand Kubernetes, we must first understand 2 things: Containers and Orchestration

---

class: middle, center

# What are containers?

---

# Containers

- Made up of Linux primitives
	* Cgroups
	* Namespaces
	* Blah blah blah

???
Namespaces - control what a process can use.
Cgroups - control what a process can use.

---

# Containers

- Isolated environments
- As in, they can have their own processes, networks, mounts. Just like VM
- Except they can share the same kernel

more info: https://opensource.com/resources/what-are-linux-containers

---

# Containers

Linux containers have been around long before Docker

- OpenVZ
- LXC
- rkt
- runc
- ...

---

class: middle, center

# Why do you need containers?

---

# Why do you need containers?

- Compatibilities, dependencies
- Quick, repetable
- Consistency

---

class: middle, center

# Container Orchestration

---

# Container orchestration

- Your application relies on other containers
- Number of users increases/decreses, how do you scale up or down?
- Blah blah blah

---

class: middle, center

### You need an underlying platform with resources and capabilities

---

# Containers orchestration technologies

- Docker Swarm
- Apache Mesos
- Kubernetes
- ...

---

# Advantages of containers orchestration

- Your app is now highly available, kinda
- User traffic is load-balanced across containers
- Scale containers up or down seamlessly
- Self-healing
- Upgrade or rollback applications
- Even scale the orchestration nodes themselves

---

class: middle, center

# Kubernetes

---

# What does "Kubernetes" mean?

#### Greek for "pilot" or "Helmsman of a ship"

---

# What is Kubernetes?

- A production-grade container orchestration system made by Google, based on Borg, systems that run inside of Google
- Google spawns billions of containers per week with these systems

more info: https://kubernetes.io/docs/concepts/overview/what-is-kubernetes/

---

# Kubernetes architecture

### When you deploy Kubernetes, you get a cluster

- Worker node(s) host the Pods
- Control plane manages the worker nodes and the Pods in the cluster

more info: https://kubernetes.io/docs/concepts/overview/components/

---

# Kubernetes Control Plane components

- kube-apiserver
- etcd
- kube-controller-manager
- kube-scheduler
- cloud-controller-manager (optional)

---

# Kubernetes Control Plane components

### kube-apiserver

- Provide interface into the control plane
- All clients and other applications interact with kubernetes through the API server

---

# Kubernetes Control Plane components

### etcd

- Acts as the cluster datastore
- Provide a strong, consistent, and highly available key-value store for persisting cluster state
- Stores objects and config information

more info: https://etcd.io/

---

# Kubernetes Control Plane components

### kube-controller-manager

- Monitors the cluster state and steers the cluster towards the desired state
- Some types of these controllers are:
	* Node controller: Responsible for noticing and responding when nodes go down
	* Replication controller: Responsible for maintaining the correct number of pods

---

# Kubernetes Control Plane components

### kube-scheduler

- Watches newly created pods with no node assigned and selects a node for them to run on
- With many factors taken into account for scheduling decisions

---

# Kubernetes Control Plane components

### cloud-controller-manager

- Lets you link your cluster into your cloud provider's API

---

# Node components

- kubelet
- kube-proxy
- Container runtime

---

# Node components

### kubelet

- Runs on each node in the cluster
- Makes sure that containers are running in a Pod
- Takes PodSpecs, ensures that the containers in those PodSpecs are running and healthy

---

# Node components

### kube-proxy

- Maintains the network rules on each node
- These network rules allow network communication to your Pods from inside or outside of your cluster

---

# Node components

### Container runtime

- Software that is resposible for running containers
	* Docker
	* containerd
	* cri-o
	* ...

---

class: middle, center

# Kubernetes Concepts

---

# Pods

- Smallest deployable units that you can create and manage in Kubernetes
- A group of one or more containers with shared storage and network resources

more info: https://kubernetes.io/docs/concepts/workloads/pods/

---

# Pods

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: hello
spec:
  containers:
    - name: hello
      image: shinomineko/hello-service
```

---

# Pods

Each pod is meant to run a single instance of a given application. If you want to scale your
application horizontally, you should use multiple pods.

---

# ReplicaSets

- Maintain a stable set of replica Pods running at any give time

---

# ReplicaSets

```yaml
apiVersion: apps/v1
kind: ReplicaSet
metadata:
  name: hello-replicaset
  labels:
    app: hello
spec:
  template:
    metadata:
      name: hello-pod
      labels:
        app: hello
    spec:
      containers:
        - name: hello
          image: shinomineko/hello-service
  replicas: 3
  selector:
    matchLabels:
      app: hello
```

---

# Labels and Selectors

- Key-value pairs attached to objects, such as pods
- Can be used to organize and to select subsets of objects
	* "environment": "dev", "environment": : "production"
	* "tier": "frontend", "tier": "backend"

---
