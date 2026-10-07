Kubernetes Cluster Architecture
Kubernetes is an open-source platform used to deploy, manage, and scale containerized applications. It provides a framework for running workloads across a group of machines while automating tasks such as scheduling, scaling, service discovery, and maintaining the desired state of applications.
A Kubernetes environment is called a cluster. A cluster is made up of a control plane and one or more worker nodes. The control plane coordinates the cluster, while worker nodes provide the computing resources required to run application workloads.
🏗️ Overview of Kubernetes Architecture
Kubernetes can broadly be divided into two major parts:
1. Control Plane
The control plane is responsible for managing the overall state of the cluster. It decides where workloads should run, stores cluster information, and continuously works to ensure that the actual state matches the configuration specified by the user.
2. Worker Nodes
Worker nodes are the machines where application workloads actually execute. They contain the components required to start containers, maintain Pods, and provide networking between workloads.
A simplified flow is:
              Kubernetes Cluster
                     │
          ┌──────────┴──────────┐
          │                     │
     Control Plane          Worker Nodes
          │                     │
   ┌──────┼──────┐        ┌─────┼─────┐
   │      │      │        │     │     │
 API    etcd  Scheduler  Kubelet Proxy Runtime
Server
          │
    Controllers

🧠 Control Plane Components
The control plane contains the main services that manage the Kubernetes cluster.
1. kube-apiserver
The kube-apiserver acts as the main entry point to Kubernetes.
It exposes the Kubernetes API through which users, command-line tools, and other Kubernetes components communicate with the cluster.
Main responsibilities
- Receives API requests from users and applications.
- Validates Kubernetes objects and configuration.
- Processes operations such as creating, updating, and deleting resources.
- Provides a common communication interface for other Kubernetes components.
- Can be scaled horizontally when required.
For example, when you run:
kubectl create deployment nginx --image=nginx

the request ultimately goes through the API server.
2. etcd
etcd is the distributed key-value database used by Kubernetes to store important cluster information.
It contains information such as:
- Cluster configuration
- Pod and Deployment state
- Service information
- Secrets and ConfigMaps
- Metadata about Kubernetes resources
The control plane relies on etcd to remember the desired and current state of the cluster.
Because etcd contains critical cluster data, regular backups are important in production environments.
3. kube-scheduler
The kube-scheduler decides which worker node should run a newly created Pod.
When a Pod does not yet have a node assigned to it, the scheduler evaluates available nodes and chooses an appropriate one.
Its decision can consider factors such as:
- CPU and memory availability
- Node restrictions
- Pod affinity and anti-affinity
- Hardware requirements
- Data locality
- Resource requests
- Scheduling policies
For example:
Pod created
     ↓
kube-scheduler
     ↓
Evaluates available nodes
     ↓
Selects suitable node
     ↓
Pod assigned to node

4. kube-controller-manager
The kube-controller-manager runs several controllers that continuously monitor the cluster.
Controllers compare the desired state specified by the user with the current state of the cluster and take corrective action when they differ.
Some important controllers include:
- Node Controller – monitors the health and availability of nodes.
- Job Controller – manages Pods created for Jobs.
- EndpointSlice Controller – maintains EndpointSlice information used by Services.
- ServiceAccount Controller – creates default ServiceAccounts for namespaces.
For example, if a Deployment requires three replicas but only two Pods are running, Kubernetes controllers work to create the missing Pod.
5. cloud-controller-manager
The cloud-controller-manager provides integration between Kubernetes and cloud platforms.
It allows Kubernetes to interact with cloud-provider-specific services without putting cloud-specific logic into the core Kubernetes components.
Depending on the cloud provider, it can handle tasks such as:
- Creating cloud load balancers
- Managing cloud-based routes
- Detecting cloud infrastructure nodes
- Integrating Kubernetes networking with cloud infrastructure
This component is mainly relevant when Kubernetes is deployed using a cloud provider.
💻 Worker Node Components
Worker nodes provide the environment in which Kubernetes workloads actually run.
Each worker node generally contains the following components.
1. kubelet
The kubelet is the main Kubernetes agent running on a worker node.
It receives Pod specifications and ensures that the required containers are running correctly.
Its responsibilities include:
- Starting containers through the container runtime.
- Monitoring container health.
- Reporting node and Pod status.
- Restarting containers when required.
- Ensuring the Pod configuration is being followed.
For example:
Control Plane
      ↓
Pod specification
      ↓
kubelet
      ↓
Container Runtime
      ↓
Containers

The kubelet primarily manages containers that are part of Kubernetes-managed workloads.
2. kube-proxy
kube-proxy is responsible for implementing part of Kubernetes networking and the Service abstraction.
It maintains networking rules on worker nodes so that traffic can be directed to the appropriate Pods.
It helps provide connectivity between:
- Pods
- Services
- Nodes
- External clients
Depending on the environment and configuration, kube-proxy can use the operating system's packet-filtering capabilities to handle network traffic.
3. Container Runtime
The container runtime is the software responsible for actually running containers on a worker node.
Kubernetes communicates with the runtime through the Container Runtime Interface (CRI).
Examples include:
- containerd
- CRI-O
- Other CRI-compatible runtimes
The runtime handles tasks such as:
- Pulling container images
- Creating containers
- Starting and stopping containers
- Managing container execution
🔄 How the Components Work Together
A typical Kubernetes workload follows a flow similar to this:
User
 │
 │ kubectl / API request
 ▼
kube-apiserver
 │
 ├──────────────► etcd
 │                  │
 │             Cluster State
 │
 ▼
Controllers / Scheduler
 │
 │ Selects node
 ▼
Worker Node
 │
 ├── kubelet
 │      │
 │      ▼
 │  Container Runtime
 │      │
 │      ▼
 │    Pod
 │
 └── kube-proxy
        │
        ▼
     Networking

The key idea is that Kubernetes continuously works toward the desired state defined by the user.
For example, if a Deployment specifies:
replicas: 3

Kubernetes attempts to maintain three running Pods. If one Pod fails, the control plane detects the difference and takes action to create a replacement.
📌 Summary
Component	Main Responsibility
kube-apiserver	Provides the Kubernetes API
etcd	Stores cluster state and configuration
kube-scheduler	Assigns Pods to suitable nodes
kube-controller-manager	Maintains the desired cluster state
cloud-controller-manager	Integrates Kubernetes with cloud providers
kubelet	Manages Pods and containers on nodes
kube-proxy	Handles Service-related networking
Container Runtime	Runs the actual containers


In short, the control plane makes decisions and manages the cluster, while worker nodes execute the workloads. Together, these components allow Kubernetes to automate deployment, networking, scaling, and recovery of containerized applications.