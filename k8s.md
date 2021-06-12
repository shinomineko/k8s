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

# To understand Kubernetes, we must first understand 2 things

class: middle

- Containers
- Orchestration

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

.center[![containers](https://www.poweradmin.com/blog/wp-content/uploads/2019/02/linux-operating-systems.png)]

---

class: middle, center

# Container orchestration

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

Greek for "pilot" or "Helmsman of a ship"

.center[![:img kubernetes logo, 50%](https://kubernetes.io/images/kubernetes-horizontal-color.png)]

---

# What is Kubernetes?

- A production-grade container orchestration system made by Google, based on Borg, systems that run inside of Google
- Google spawns billions of containers per week with these systems

---

# Kubernetes architecture

## Node

- A machine that run containerized applications
	* Worker nodes
	* Control plane

## Cluster

- A set of nodes

---

# Kubernetes Control Plane components

.center[![:img control plane, 50%](https://d33wubrfki0l68.cloudfront.net/2475489eaf20163ec0f54ddc1d92aa8d4c87c96b/e7c81/images/docs/components-of-kubernetes.svg)]
