# kubectl logs vs kubectl events

| Feature | `kubectl logs` | `kubectl events` |
| :--- | :--- | :--- |
| **What it shows** | Output produced by the container/application | Kubernetes events about resources |
| **Main purpose** | Debug application/container behavior | Debug Kubernetes scheduling, startup, probes, images, etc. |
| **Source** | Container's stdout/stderr | Kubernetes control plane/kubelet |
| **Example** | Connection refused to MongoDB | Failed to pull image |
| **Useful for** | App crashes, exceptions, API errors | Pending pods, failed mounts, image problems |
| **Command** | `kubectl logs <pod>` | `kubectl events` |
| **Usually associated with** | Containers | Pods, Nodes, Deployments, etc. |

---

## Example

Suppose you have:

```console
$ kubectl get pods
NAME        READY   STATUS             RESTARTS
my-app      0/1     CrashLoopBackOff   5
```

### 1. `kubectl logs`

```console
$ kubectl logs my-app
Starting application...
Connecting to database...
ERROR: connection refused
Application shutting down
```

This tells you what the application itself is saying.

> **Think:**  
> *"What did my container/application do?"*

---

### 2. `kubectl events`

```console
$ kubectl events
Warning   BackOff   pod/my-app   Back-off restarting failed container
Normal    Pulled    pod/my-app   Successfully pulled image "myapp:v1"
Normal    Created   pod/my-app   Created container app
Normal    Started   pod/my-app   Started container app
```

This tells you what Kubernetes is doing/observing with the Pod.

> **Think:**  
> *"What is Kubernetes doing with my workload?"*

---

## Another Important Example

Suppose the image doesn't exist:

```console
$ kubectl get pods
NAME     READY   STATUS
my-app   0/1     ImagePullBackOff
```

`kubectl logs my-app` may not give you useful application logs because the container never successfully started.

But:

```console
$ kubectl events
Warning   Failed   pod/my-app   Failed to pull image "myapp:v99"
Warning   Failed   pod/my-app   Error: ImagePullBackOff
```

That's why Events are particularly useful when the container hasn't even started.

---

# <span style="font-size: 32px; font-weight: 800; color: #2563eb;">Terminal:</span>

<pre style="background-color: #1e1e2e; color: #cdd6f4; padding: 16px; border-radius: 8px; font-family: 'Consolas', 'Courier New', monospace; font-size: 13.5px; line-height: 1.45; overflow-x: auto; border: 1px solid #313244;"><code><span style="color: #4ade80; font-weight: bold;">amitabh@LAPTOP-3KF17VR3</span>:<span style="color: #60a5fa;">/mnt/c/Users/USER/Downloads/devops-heros-branch10104-main/devops-heros-branch10104-main/session-14-kubernetes-troubleshooting/01-kubectl-get</span>$ kubectl apply -f sample-workload.yaml
pod/get-demo created
<span style="color: #4ade80; font-weight: bold;">amitabh@LAPTOP-3KF17VR3</span>:<span style="color: #60a5fa;">/mnt/c/Users/USER/Downloads/devops-heros-branch10104-main/devops-heros-branch10104-main/session-14-kubernetes-troubleshooting/01-kubectl-get</span>$ kubectl get pods
NAME                                READY   STATUS    RESTARTS      AGE
get-demo                            1/1     Running   0             13s
notes-dev-deploy-7df4d99689-9rdj5   1/1     Running   1 (56s ago)   6h10m
notes-dev-deploy-7df4d99689-chwpp   1/1     Running   1 (56s ago)   6h10m
notes-dev-deploy-7df4d99689-zlltw   1/1     Running   1 (56s ago)   6h13m
<span style="color: #4ade80; font-weight: bold;">amitabh@LAPTOP-3KF17VR3</span>:<span style="color: #60a5fa;">/mnt/c/Users/USER/Downloads/devops-heros-branch10104-main/devops-heros-branch10104-main/session-14-kubernetes-troubleshooting/01-kubectl-get</span>$ kubectl delete pods -l app=notes-dev
pod &quot;notes-dev-deploy-7df4d99689-9rdj5&quot; deleted from default namespace
pod &quot;notes-dev-deploy-7df4d99689-chwpp&quot; deleted from default namespace
pod &quot;notes-dev-deploy-7df4d99689-zlltw&quot; deleted from default namespace
<span style="color: #4ade80; font-weight: bold;">amitabh@LAPTOP-3KF17VR3</span>:<span style="color: #60a5fa;">/mnt/c/Users/USER/Downloads/devops-heros-branch10104-main/devops-heros-branch10104-main/session-14-kubernetes-troubleshooting/01-kubectl-get</span>$ kubectl get pods -o wide
NAME                                READY   STATUS    RESTARTS   AGE   IP            NODE       NOMINATED NODE   READINESS GATES
get-demo                            1/1     Running   0          72s   10.244.0.10   minikube   &lt;none&gt;           &lt;none&gt;
notes-dev-deploy-7df4d99689-fsrls   1/1     Running   0          18s   10.244.0.11   minikube   &lt;none&gt;           &lt;none&gt;
notes-dev-deploy-7df4d99689-vqx9g   1/1     Running   0          18s   10.244.0.12   minikube   &lt;none&gt;           &lt;none&gt;
notes-dev-deploy-7df4d99689-wqdhr   1/1     Running   0          18s   10.244.0.13   minikube   &lt;none&gt;           &lt;none&gt;
<span style="color: #4ade80; font-weight: bold;">amitabh@LAPTOP-3KF17VR3</span>:<span style="color: #60a5fa;">/mnt/c/Users/USER/Downloads/devops-heros-branch10104-main/devops-heros-branch10104-main/session-14-kubernetes-troubleshooting/01-kubectl-get</span>$ kubectl get pods
NAME                                READY   STATUS    RESTARTS   AGE
get-demo                            1/1     Running   0          103s
notes-dev-deploy-7df4d99689-fsrls   1/1     Running   0          49s
notes-dev-deploy-7df4d99689-vqx9g   1/1     Running   0          49s
notes-dev-deploy-7df4d99689-wqdhr   1/1     Running   0          49s
<span style="color: #4ade80; font-weight: bold;">amitabh@LAPTOP-3KF17VR3</span>:<span style="color: #60a5fa;">/mnt/c/Users/USER/Downloads/devops-heros-branch10104-main/devops-heros-branch10104-main/session-14-kubernetes-troubleshooting/01-kubectl-get</span>$ kubectl delete deployment notes-dev-deploy
deployment.apps &quot;notes-dev-deploy&quot; deleted from default namespace
<span style="color: #4ade80; font-weight: bold;">amitabh@LAPTOP-3KF17VR3</span>:<span style="color: #60a5fa;">/mnt/c/Users/USER/Downloads/devops-heros-branch10104-main/devops-heros-branch10104-main/session-14-kubernetes-troubleshooting/01-kubectl-get</span>$ kubectl get pods
NAME       READY   STATUS    RESTARTS   AGE
get-demo   1/1     Running   0          2m52s
<span style="color: #4ade80; font-weight: bold;">amitabh@LAPTOP-3KF17VR3</span>:<span style="color: #60a5fa;">/mnt/c/Users/USER/Downloads/devops-heros-branch10104-main/devops-heros-branch10104-main/session-14-kubernetes-troubleshooting/01-kubectl-get</span>$ kubectl get services
NAME            TYPE        CLUSTER-IP      EXTERNAL-IP   PORT(S)        AGE
kubernetes      ClusterIP   10.96.0.1       &lt;none&gt;        443/TCP        5d4h
notes-dev-svc   NodePort    10.101.86.145   &lt;none&gt;        80:30090/TCP   6h24m
<span style="color: #4ade80; font-weight: bold;">amitabh@LAPTOP-3KF17VR3</span>:<span style="color: #60a5fa;">/mnt/c/Users/USER/Downloads/devops-heros-branch10104-main/devops-heros-branch10104-main/session-14-kubernetes-troubleshooting/01-kubectl-get</span>$ kubectl delete service notes-dev-svc
service &quot;notes-dev-svc&quot; deleted from default namespace
<span style="color: #4ade80; font-weight: bold;">amitabh@LAPTOP-3KF17VR3</span>:<span style="color: #60a5fa;">/mnt/c/Users/USER/Downloads/devops-heros-branch10104-main/devops-heros-branch10104-main/session-14-kubernetes-troubleshooting/01-kubectl-get</span>$ kubectl get deployments
No resources found in default namespace.
<span style="color: #4ade80; font-weight: bold;">amitabh@LAPTOP-3KF17VR3</span>:<span style="color: #60a5fa;">/mnt/c/Users/USER/Downloads/devops-heros-branch10104-main/devops-heros-branch10104-main/session-14-kubernetes-troubleshooting/01-kubectl-get</span>$ kubectl get nodes
NAME       STATUS   ROLES           AGE    VERSION
minikube   Ready    control-plane   5d4h   v1.37.0
<span style="color: #4ade80; font-weight: bold;">amitabh@LAPTOP-3KF17VR3</span>:<span style="color: #60a5fa;">/mnt/c/Users/USER/Downloads/devops-heros-branch10104-main/devops-heros-branch10104-main/session-14-kubernetes-troubleshooting/01-kubectl-get</span>$ kubectl get all
NAME           READY   STATUS    RESTARTS   AGE
pod/get-demo   1/1     Running   0          4m8s

NAME                 TYPE        CLUSTER-IP   EXTERNAL-IP   PORT(S)   AGE
service/kubernetes   ClusterIP   10.96.0.1    &lt;none&gt;        443/TCP   5d4h
<span style="color: #4ade80; font-weight: bold;">amitabh@LAPTOP-3KF17VR3</span>:<span style="color: #60a5fa;">/mnt/c/Users/USER/Downloads/devops-heros-branch10104-main/devops-heros-branch10104-main/session-14-kubernetes-troubleshooting/01-kubectl-get</span>$ kubectl get pods -w
NAME       READY   STATUS    RESTARTS   AGE
get-demo   1/1     Running   0          4m28s
^C<span style="color: #4ade80; font-weight: bold;">amitabh@LAPTOP-3KF17VR3</span>:<span style="color: #60a5fa;">/mnt/c/Users/USER/Downloads/devops-heros-branch10104-main/devops-heros-branch10104-main/session-14-kubernetes-troubleshooting/01-kubectl-get</span>$ kubectl delete pod get-demo
pod &quot;get-demo&quot; deleted from default namespace
<span style="color: #4ade80; font-weight: bold;">amitabh@LAPTOP-3KF17VR3</span>:<span style="color: #60a5fa;">/mnt/c/Users/USER/Downloads/devops-heros-branch10104-main/devops-heros-branch10104-main/session-14-kubernetes-troubleshooting/01-kubectl-get</span>$ kubectl get pods
No resources found in default namespace.
<span style="color: #4ade80; font-weight: bold;">amitabh@LAPTOP-3KF17VR3</span>:<span style="color: #60a5fa;">/mnt/c/Users/USER/Downloads/devops-heros-branch10104-main/devops-heros-branch10104-main/session-14-kubernetes-troubleshooting/01-kubectl-get</span>$ kubectl describe
error: You must specify the type of resource to describe. Use &quot;kubectl api-resources&quot; for a complete list of supported resources.
<span style="color: #4ade80; font-weight: bold;">amitabh@LAPTOP-3KF17VR3</span>:<span style="color: #60a5fa;">/mnt/c/Users/USER/Downloads/devops-heros-branch10104-main/devops-heros-branch10104-main/session-14-kubernetes-troubleshooting/01-kubectl-get</span>$ kubectl logs
error: expected &#x27;logs [-f] [-p] (POD | TYPE/NAME) [-c CONTAINER]&#x27;.
POD or TYPE/NAME is a required argument for the logs command
See &#x27;kubectl logs -h&#x27; for help and examples
<span style="color: #4ade80; font-weight: bold;">amitabh@LAPTOP-3KF17VR3</span>:<span style="color: #60a5fa;">/mnt/c/Users/USER/Downloads/devops-heros-branch10104-main/devops-heros-branch10104-main/session-14-kubernetes-troubleshooting/01-kubectl-get</span>$ kubectl get pods
kubectl get pods -o wide
kubectl get all
kubectl get nodes
kubectl get services
kubectl get deployments
kubectl get pods -w
No resources found in default namespace.
No resources found in default namespace.
NAME                 TYPE        CLUSTER-IP   EXTERNAL-IP   PORT(S)   AGE
service/kubernetes   ClusterIP   10.96.0.1    &lt;none&gt;        443/TCP   5d4h
NAME       STATUS   ROLES           AGE    VERSION
minikube   Ready    control-plane   5d4h   v1.37.0
NAME         TYPE        CLUSTER-IP   EXTERNAL-IP   PORT(S)   AGE
kubernetes   ClusterIP   10.96.0.1    &lt;none&gt;        443/TCP   5d4h
No resources found in default namespace.
^C<span style="color: #4ade80; font-weight: bold;">amitabh@LAPTOP-3KF17VR3</span>:<span style="color: #60a5fa;">/mnt/c/Users/USER/Downloads/devops-heros-branch10104-main/devops-heros-branch10104-main/session-14-kubernetes-troubleshooting/01-kubectl-get</span>$ cd ..
<span style="color: #4ade80; font-weight: bold;">amitabh@LAPTOP-3KF17VR3</span>:<span style="color: #60a5fa;">/mnt/c/Users/USER/Downloads/devops-heros-branch10104-main/devops-heros-branch10104-main/session-14-kubernetes-troubleshooting</span>$ cd mini-project
<span style="color: #4ade80; font-weight: bold;">amitabh@LAPTOP-3KF17VR3</span>:<span style="color: #60a5fa;">/mnt/c/Users/USER/Downloads/devops-heros-branch10104-main/devops-heros-branch10104-main/session-14-kubernetes-troubleshooting/mini-project</span>$ kubectl apply -f deployment.yaml
kubectl apply -f service.yaml
deployment.apps/troubleshooting-app created
service/troubleshooting-service created
<span style="color: #4ade80; font-weight: bold;">amitabh@LAPTOP-3KF17VR3</span>:<span style="color: #60a5fa;">/mnt/c/Users/USER/Downloads/devops-heros-branch10104-main/devops-heros-branch10104-main/session-14-kubernetes-troubleshooting/mini-project</span>$ kubectl get pods
kubectl get service
NAME                                   READY   STATUS    RESTARTS   AGE
troubleshooting-app-59d4957864-jrhph   1/1     Running   0          37s
troubleshooting-app-59d4957864-s76dk   1/1     Running   0          37s
NAME                      TYPE        CLUSTER-IP       EXTERNAL-IP   PORT(S)   AGE
kubernetes                ClusterIP   10.96.0.1        &lt;none&gt;        443/TCP   5d4h
troubleshooting-service   ClusterIP   10.103.205.128   &lt;none&gt;        80/TCP    38s
<span style="color: #4ade80; font-weight: bold;">amitabh@LAPTOP-3KF17VR3</span>:<span style="color: #60a5fa;">/mnt/c/Users/USER/Downloads/devops-heros-branch10104-main/devops-heros-branch10104-main/session-14-kubernetes-troubleshooting/mini-project</span>$ kubectl get pods -o wide
NAME                                   READY   STATUS    RESTARTS   AGE   IP            NODE       NOMINATED NODE   READINESS GATES
troubleshooting-app-59d4957864-jrhph   1/1     Running   0          51s   10.244.0.14   minikube   &lt;none&gt;           &lt;none&gt;
troubleshooting-app-59d4957864-s76dk   1/1     Running   0          51s   10.244.0.15   minikube   &lt;none&gt;           &lt;none&gt;
<span style="color: #4ade80; font-weight: bold;">amitabh@LAPTOP-3KF17VR3</span>:<span style="color: #60a5fa;">/mnt/c/Users/USER/Downloads/devops-heros-branch10104-main/devops-heros-branch10104-main/session-14-kubernetes-troubleshooting/mini-project</span>$ kubectl get pods
NAME                                   READY   STATUS    RESTARTS   AGE
troubleshooting-app-59d4957864-jrhph   1/1     Running   0          70s
troubleshooting-app-59d4957864-s76dk   1/1     Running   0          70s
<span style="color: #4ade80; font-weight: bold;">amitabh@LAPTOP-3KF17VR3</span>:<span style="color: #60a5fa;">/mnt/c/Users/USER/Downloads/devops-heros-branch10104-main/devops-heros-branch10104-main/session-14-kubernetes-troubleshooting/mini-project</span>$ kubectl describe pod troubleshooting-app-59d4957864-jrhph
Name:             troubleshooting-app-59d4957864-jrhph
Namespace:        default
Priority:         0
Service Account:  default
Node:             minikube/192.168.49.2
Start Time:       Tue, 22 Sep 2026 13:50:05 +0000
Labels:           app=troubleshooting-app
                  pod-template-hash=59d4957864
Annotations:      &lt;none&gt;
Status:           Running
IP:               10.244.0.14
IPs:
  IP:           10.244.0.14
Controlled By:  ReplicaSet/troubleshooting-app-59d4957864
Containers:
  app:
    Container ID:   containerd://f53d47203c70c3e84b7017fb62231d41693c167e6c8b9e3400a5e8f7cd3106bf     
    Image:          nginx:1.27
    Image ID:       docker.io/library/nginx@sha256:6784fb0834aa7dbbe12e3d7471e69c290df3e6ba810dc38b34ae33d3c1c05f7d
    Port:           80/TCP
    Host Port:      0/TCP
    State:          Running
      Started:      Tue, 22 Sep 2026 13:50:06 +0000
    Ready:          True
    Restart Count:  0
    Environment:    &lt;none&gt;
    Mounts:
      /var/run/secrets/kubernetes.io/serviceaccount from kube-api-access-8wwwq (ro)
Conditions:
  Type                        Status
  PodReadyToStartContainers   True
  Initialized                 True
  Ready                       True
  ContainersReady             True
  PodScheduled                True
Volumes:
  kube-api-access-8wwwq:
    Type:                    Projected (a volume that contains injected data from multiple sources)   
    TokenExpirationSeconds:  3607
    ConfigMapName:           kube-root-ca.crt
    Optional:                false
    DownwardAPI:             true
QoS Class:                   BestEffort
Node-Selectors:              &lt;none&gt;
Tolerations:                 node.kubernetes.io/not-ready:NoExecute op=Exists for 300s
                             node.kubernetes.io/unreachable:NoExecute op=Exists for 300s
Events:
  Type    Reason     Age   From               Message
  ----    ------     ----  ----               -------
  Normal  Scheduled  98s   default-scheduler  Successfully assigned default/troubleshooting-app-59d4957864-jrhph to minikube
  Normal  Pulled     98s   kubelet            spec.containers{app}: Container image &quot;nginx:1.27&quot; already present on machine and can be accessed by the pod
  Normal  Created    97s   kubelet            spec.containers{app}: Container created
  Normal  Started    97s   kubelet            spec.containers{app}: Container started
<span style="color: #4ade80; font-weight: bold;">amitabh@LAPTOP-3KF17VR3</span>:<span style="color: #60a5fa;">/mnt/c/Users/USER/Downloads/devops-heros-branch10104-main/devops-heros-branch10104-main/session-14-kubernetes-troubleshooting/mini-project</span>$ kubectl logs troubleshooting-app-59d4957
864-jrhph
/docker-entrypoint.sh: /docker-entrypoint.d/ is not empty, will attempt to perform configuration
/docker-entrypoint.sh: Looking for shell scripts in /docker-entrypoint.d/
/docker-entrypoint.sh: Launching /docker-entrypoint.d/10-listen-on-ipv6-by-default.sh
10-listen-on-ipv6-by-default.sh: info: Getting the checksum of /etc/nginx/conf.d/default.conf
10-listen-on-ipv6-by-default.sh: info: Enabled listen on IPv6 in /etc/nginx/conf.d/default.conf       
/docker-entrypoint.sh: Sourcing /docker-entrypoint.d/15-local-resolvers.envsh
/docker-entrypoint.sh: Launching /docker-entrypoint.d/20-envsubst-on-templates.sh
/docker-entrypoint.sh: Launching /docker-entrypoint.d/30-tune-worker-processes.sh
/docker-entrypoint.sh: Configuration complete; ready for start up
2026/09/22 13:50:06 [notice] 1#1: using the &quot;epoll&quot; event method
2026/09/22 13:50:06 [notice] 1#1: nginx/1.27.5
2026/09/22 13:50:06 [notice] 1#1: built by gcc 12.2.0 (Debian 12.2.0-14)
2026/09/22 13:50:06 [notice] 1#1: OS: Linux 6.18.33.2-microsoft-standard-WSL2
2026/09/22 13:50:06 [notice] 1#1: getrlimit(RLIMIT_NOFILE): 1048576:1048576
2026/09/22 13:50:06 [notice] 1#1: start worker processes
2026/09/22 13:50:06 [notice] 1#1: start worker process 29
2026/09/22 13:50:06 [notice] 1#1: start worker process 30
2026/09/22 13:50:06 [notice] 1#1: start worker process 31
2026/09/22 13:50:06 [notice] 1#1: start worker process 32
2026/09/22 13:50:06 [notice] 1#1: start worker process 33
2026/09/22 13:50:06 [notice] 1#1: start worker process 34
2026/09/22 13:50:06 [notice] 1#1: start worker process 35
2026/09/22 13:50:06 [notice] 1#1: start worker process 36
2026/09/22 13:50:06 [notice] 1#1: start worker process 37
2026/09/22 13:50:06 [notice] 1#1: start worker process 38
2026/09/22 13:50:06 [notice] 1#1: start worker process 39
2026/09/22 13:50:06 [notice] 1#1: start worker process 40
<span style="color: #4ade80; font-weight: bold;">amitabh@LAPTOP-3KF17VR3</span>:<span style="color: #60a5fa;">/mnt/c/Users/USER/Downloads/devops-heros-branch10104-main/devops-heros-branch10104-main/session-14-kubernetes-troubleshooting/mini-project</span>$ kubectl exec -it troubleshooting-app-59d4957
864-jrhph -- bash
error: you must specify at least one command for the container
864-jrhph: command not found
<span style="color: #4ade80; font-weight: bold;">amitabh@LAPTOP-3KF17VR3</span>:<span style="color: #60a5fa;">/mnt/c/Users/USER/Downloads/devops-heros-branch10104-main/devops-heros-branch10104-main/session-14-kubernetes-troubleshooting/mini-project</span>$ kubectl exec -it troubleshooting-app-59d4957864-jrhph -- bash
<span style="color: #f87171; font-weight: bold;">root@troubleshooting-app-59d4957864-jrhph</span>:<span style="color: #60a5fa;">/</span># curl localhost
&lt;!DOCTYPE html&gt;
&lt;html&gt;
&lt;head&gt;
&lt;title&gt;Welcome to nginx!&lt;/title&gt;
&lt;style&gt;
html { color-scheme: light dark; }
body { width: 35em; margin: 0 auto;
font-family: Tahoma, Verdana, Arial, sans-serif; }
&lt;/style&gt;
&lt;/head&gt;
&lt;body&gt;
&lt;h1&gt;Welcome to nginx!&lt;/h1&gt;
&lt;p&gt;If you see this page, the nginx web server is successfully installed and
working. Further configuration is required.&lt;/p&gt;

&lt;p&gt;For online documentation and support please refer to
&lt;a href=&quot;http://nginx.org/&quot;&gt;nginx.org&lt;/a&gt;.&lt;br/&gt;
Commercial support is available at
&lt;a href=&quot;http://nginx.com/&quot;&gt;nginx.com&lt;/a&gt;.&lt;/p&gt;

&lt;p&gt;&lt;em&gt;Thank you for using nginx.&lt;/em&gt;&lt;/p&gt;
&lt;/body&gt;
&lt;/html&gt;
<span style="color: #f87171; font-weight: bold;">root@troubleshooting-app-59d4957864-jrhph</span>:<span style="color: #60a5fa;">/</span># exit
exit
<span style="color: #4ade80; font-weight: bold;">amitabh@LAPTOP-3KF17VR3</span>:<span style="color: #60a5fa;">/mnt/c/Users/USER/Downloads/devops-heros-branch10104-main/devops-heros-branch10104-main/session-14-kubernetes-troubleshooting/mini-project</span>$ kubectl get service
NAME                      TYPE        CLUSTER-IP       EXTERNAL-IP   PORT(S)   AGE
kubernetes                ClusterIP   10.96.0.1        &lt;none&gt;        443/TCP   5d4h
troubleshooting-service   ClusterIP   10.103.205.128   &lt;none&gt;        80/TCP    4m26s
<span style="color: #4ade80; font-weight: bold;">amitabh@LAPTOP-3KF17VR3</span>:<span style="color: #60a5fa;">/mnt/c/Users/USER/Downloads/devops-heros-branch10104-main/devops-heros-branch10104-main/session-14-kubernetes-troubleshooting/mini-project</span>$ kubectl describe service troubleshooting-service
Name:                     troubleshooting-service
Namespace:                default
Labels:                   &lt;none&gt;
Annotations:              &lt;none&gt;
Selector:                 app=troubleshooting-app
Type:                     ClusterIP
IP Family Policy:         SingleStack
IP Families:              IPv4
IP:                       10.103.205.128
IPs:                      10.103.205.128
Port:                     &lt;unset&gt;  80/TCP
TargetPort:               80/TCP
Endpoints:                10.244.0.15:80,10.244.0.14:80
Session Affinity:         None
Internal Traffic Policy:  Cluster
Events:                   &lt;none&gt;
<span style="color: #4ade80; font-weight: bold;">amitabh@LAPTOP-3KF17VR3</span>:<span style="color: #60a5fa;">/mnt/c/Users/USER/Downloads/devops-heros-branch10104-main/devops-heros-branch10104-main/session-14-kubernetes-troubleshooting/mini-project</span>$ kubectl get endpoints troubleshooting-service
Warning: v1 Endpoints is deprecated in v1.33+; use discovery.k8s.io/v1 EndpointSlice
NAME                      ENDPOINTS                       AGE
troubleshooting-service   10.244.0.14:80,10.244.0.15:80   4m51s
<span style="color: #4ade80; font-weight: bold;">amitabh@LAPTOP-3KF17VR3</span>:<span style="color: #60a5fa;">/mnt/c/Users/USER/Downloads/devops-heros-branch10104-main/devops-heros-branch10104-main/session-14-kubernetes-troubleshooting/mini-project</span>$ kubectl apply -f broken-pod.yaml
pod/project-broken-pod created
<span style="color: #4ade80; font-weight: bold;">amitabh@LAPTOP-3KF17VR3</span>:<span style="color: #60a5fa;">/mnt/c/Users/USER/Downloads/devops-heros-branch10104-main/devops-heros-branch10104-main/session-14-kubernetes-troubleshooting/mini-project</span>$ kubectl get pod project-broken-pod      
NAME                 READY   STATUS              RESTARTS   AGE
project-broken-pod   0/1     ContainerCreating   0          8s
<span style="color: #4ade80; font-weight: bold;">amitabh@LAPTOP-3KF17VR3</span>:<span style="color: #60a5fa;">/mnt/c/Users/USER/Downloads/devops-heros-branch10104-main/devops-heros-branch10104-main/session-14-kubernetes-troubleshooting/mini-project</span>$ kubectl get pod project-broken-pod      
NAME                 READY   STATUS             RESTARTS   AGE
project-broken-pod   0/1     ImagePullBackOff   0          25s
<span style="color: #4ade80; font-weight: bold;">amitabh@LAPTOP-3KF17VR3</span>:<span style="color: #60a5fa;">/mnt/c/Users/USER/Downloads/devops-heros-branch10104-main/devops-heros-branch10104-main/session-14-kubernetes-troubleshooting/mini-project</span>$ kubectl describe pod project-broken-pod
Name:             project-broken-pod
Namespace:        default
Priority:         0
Service Account:  default
Node:             minikube/192.168.49.2
Start Time:       Tue, 22 Sep 2026 13:55:09 +0000
Labels:           &lt;none&gt;
Annotations:      &lt;none&gt;
Status:           Pending
IP:               10.244.0.16
IPs:
  IP:  10.244.0.16
Containers:
  app:
    Container ID:
    Image:          nginx:this-tag-does-not-exist
    Image ID:
    Port:           &lt;none&gt;
    Host Port:      &lt;none&gt;
    State:          Waiting
      Reason:       ErrImagePull
    Ready:          False
    Restart Count:  0
    Environment:    &lt;none&gt;
    Mounts:
      /var/run/secrets/kubernetes.io/serviceaccount from kube-api-access-rnq8x (ro)
Conditions:
  Type                        Status
  PodReadyToStartContainers   True
  Initialized                 True
  Ready                       False
  ContainersReady             False
  PodScheduled                True
Volumes:
  kube-api-access-rnq8x:
    Type:                    Projected (a volume that contains injected data from multiple sources)   
    TokenExpirationSeconds:  3607
    ConfigMapName:           kube-root-ca.crt
    Optional:                false
    DownwardAPI:             true
QoS Class:                   BestEffort
Node-Selectors:              &lt;none&gt;
Tolerations:                 node.kubernetes.io/not-ready:NoExecute op=Exists for 300s
                             node.kubernetes.io/unreachable:NoExecute op=Exists for 300s
Events:
  Type     Reason     Age                From               Message
  ----     ------     ----               ----               -------
  Normal   Scheduled  45s                default-scheduler  Successfully assigned default/project-broken-pod to minikube
  Normal   Pulling    22s (x2 over 44s)  kubelet            spec.containers{app}: Pulling image &quot;nginx:this-tag-does-not-exist&quot;
  Warning  Failed     20s (x2 over 34s)  kubelet            spec.containers{app}: Failed to pull image &quot;nginx:this-tag-does-not-exist&quot;: rpc error: code = NotFound desc = failed to pull and unpack image &quot;docker.io/library/nginx:this-tag-does-not-exist&quot;: failed to resolve reference &quot;docker.io/library/nginx:this-tag-does-not-exist&quot;: docker.io/library/nginx:this-tag-does-not-exist: not found
  Warning  Failed     20s (x2 over 34s)  kubelet            spec.containers{app}: Error: ErrImagePull 
  Normal   BackOff    9s (x2 over 33s)   kubelet            spec.containers{app}: Back-off pulling image &quot;nginx:this-tag-does-not-exist&quot;
  Warning  Failed     9s (x2 over 33s)   kubelet            spec.containers{app}: Error: ImagePullBackOff
<span style="color: #4ade80; font-weight: bold;">amitabh@LAPTOP-3KF17VR3</span>:<span style="color: #60a5fa;">/mnt/c/Users/USER/Downloads/devops-heros-branch10104-main/devops-heros-branch10104-main/session-14-kubernetes-troubleshooting/mini-project</span>$ kubectl get service
NAME                      TYPE        CLUSTER-IP       EXTERNAL-IP   PORT(S)   AGE
kubernetes                ClusterIP   10.96.0.1        &lt;none&gt;        443/TCP   5d4h
troubleshooting-service   ClusterIP   10.103.205.128   &lt;none&gt;        80/TCP    9m34s
<span style="color: #4ade80; font-weight: bold;">amitabh@LAPTOP-3KF17VR3</span>:<span style="color: #60a5fa;">/mnt/c/Users/USER/Downloads/devops-heros-branch10104-main/devops-heros-branch10104-main/session-14-kubernetes-troubleshooting/mini-project</span>$ kubectl get endpoints troubleshooting-service
Warning: v1 Endpoints is deprecated in v1.33+; use discovery.k8s.io/v1 EndpointSlice
NAME                      ENDPOINTS                       AGE
troubleshooting-service   10.244.0.14:80,10.244.0.15:80   9m52s
<span style="color: #4ade80; font-weight: bold;">amitabh@LAPTOP-3KF17VR3</span>:<span style="color: #60a5fa;">/mnt/c/Users/USER/Downloads/devops-heros-branch10104-main/devops-heros-branch10104-main/session-14-kubernetes-troubleshooting/mini-project</span>$ kubectl get pods --show-labels
NAME                                   READY   STATUS             RESTARTS   AGE     LABELS
project-broken-pod                     0/1     ImagePullBackOff   0          5m14s   &lt;none&gt;
troubleshooting-app-59d4957864-jrhph   1/1     Running            0          10m     app=troubleshooting-app,pod-template-hash=59d4957864
troubleshooting-app-59d4957864-s76dk   1/1     Running            0          10m     app=troubleshooting-app,pod-template-hash=59d4957864
<span style="color: #4ade80; font-weight: bold;">amitabh@LAPTOP-3KF17VR3</span>:<span style="color: #60a5fa;">/mnt/c/Users/USER/Downloads/devops-heros-branch10104-main/devops-heros-branch10104-main/session-14-kubernetes-troubleshooting/mini-project</span>$ kubectl describe service troubleshooting-service
Name:                     troubleshooting-service
Namespace:                default
Labels:                   &lt;none&gt;
Annotations:              &lt;none&gt;
Selector:                 app=troubleshooting-app
Type:                     ClusterIP
IP Family Policy:         SingleStack
IP Families:              IPv4
IP:                       10.103.205.128
IPs:                      10.103.205.128
Port:                     &lt;unset&gt;  80/TCP
TargetPort:               80/TCP
Endpoints:                10.244.0.15:80,10.244.0.14:80
Session Affinity:         None
Internal Traffic Policy:  Cluster
Events:                   &lt;none&gt;
<span style="color: #4ade80; font-weight: bold;">amitabh@LAPTOP-3KF17VR3</span>:<span style="color: #60a5fa;">/mnt/c/Users/USER/Downloads/devops-heros-branch10104-main/devops-heros-branch10104-main/session-14-kubernetes-troubleshooting/mini-project</span>$ kubectl describe service troubleshooting-service
Name:                     troubleshooting-service
Namespace:                default
Labels:                   &lt;none&gt;
Annotations:              &lt;none&gt;
Selector:                 app=troubleshooting-app
Type:                     ClusterIP
IP Family Policy:         SingleStack
IP Families:              IPv4
IP:                       10.103.205.128
IPs:                      10.103.205.128
Port:                     &lt;unset&gt;  80/TCP
TargetPort:               80/TCP
Endpoints:                10.244.0.15:80,10.244.0.14:80
Session Affinity:         None
Internal Traffic Policy:  Cluster
Events:                   &lt;none&gt;
<span style="color: #4ade80; font-weight: bold;">amitabh@LAPTOP-3KF17VR3</span>:<span style="color: #60a5fa;">/mnt/c/Users/USER/Downloads/devops-heros-branch10104-main/devops-heros-branch10104-main/session-14-kubernetes-troubleshooting/mini-project</span>$ kubectl get endpoints troubleshooting-service
Warning: v1 Endpoints is deprecated in v1.33+; use discovery.k8s.io/v1 EndpointSlice
NAME                      ENDPOINTS                       AGE
troubleshooting-service   10.244.0.14:80,10.244.0.15:80   13m
<span style="color: #4ade80; font-weight: bold;">amitabh@LAPTOP-3KF17VR3</span>:<span style="color: #60a5fa;">/mnt/c/Users/USER/Downloads/devops-heros-branch10104-main/devops-heros-branch10104-main/session-14-kubernetes-troubleshooting/mini-project</span>$ kubectl get deployment
NAME                  READY   UP-TO-DATE   AVAILABLE   AGE
troubleshooting-app   2/2     2            2           31m
<span style="color: #4ade80; font-weight: bold;">amitabh@LAPTOP-3KF17VR3</span>:<span style="color: #60a5fa;">/mnt/c/Users/USER/Downloads/devops-heros-branch10104-main/devops-heros-branch10104-main/session-14-kubernetes-troubleshooting/mini-project</span>$ kubectl get deployment troubleshooting-app -o yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  annotations:
    deployment.kubernetes.io/revision: &quot;1&quot;
    kubectl.kubernetes.io/last-applied-configuration: |
      {&quot;apiVersion&quot;:&quot;apps/v1&quot;,&quot;kind&quot;:&quot;Deployment&quot;,&quot;metadata&quot;:{&quot;annotations&quot;:{},&quot;name&quot;:&quot;troubleshooting-app&quot;,&quot;namespace&quot;:&quot;default&quot;},&quot;spec&quot;:{&quot;replicas&quot;:2,&quot;selector&quot;:{&quot;matchLabels&quot;:{&quot;app&quot;:&quot;troubleshooting-app&quot;}},&quot;template&quot;:{&quot;metadata&quot;:{&quot;labels&quot;:{&quot;app&quot;:&quot;troubleshooting-app&quot;}},&quot;spec&quot;:{&quot;containers&quot;:[{&quot;image&quot;:&quot;nginx:1.27&quot;,&quot;name&quot;:&quot;app&quot;,&quot;ports&quot;:[{&quot;containerPort&quot;:80}]}]}}}}
  creationTimestamp: &quot;2026-09-22T13:50:05Z&quot;
  generation: 1
  name: troubleshooting-app
  namespace: default
  resourceVersion: &quot;310837&quot;
  uid: 4eefd2b2-f840-4af4-adaa-2ae48ada4400
spec:
  progressDeadlineSeconds: 600
  replicas: 2
  revisionHistoryLimit: 10
  selector:
    matchLabels:
      app: troubleshooting-app
  strategy:
    rollingUpdate:
      maxSurge: 25%
      maxUnavailable: 25%
    type: RollingUpdate
  template:
    metadata:
      labels:
        app: troubleshooting-app
    spec:
      containers:
      - image: nginx:1.27
        imagePullPolicy: IfNotPresent
        name: app
        ports:
        - containerPort: 80
          protocol: TCP
        resources: {}
        terminationMessagePath: /dev/termination-log
        terminationMessagePolicy: File
      dnsPolicy: ClusterFirst
      restartPolicy: Always
      schedulerName: default-scheduler
      securityContext: {}
      terminationGracePeriodSeconds: 30
status:
  availableReplicas: 2
  conditions:
  - lastTransitionTime: &quot;2026-09-22T13:50:06Z&quot;
    lastUpdateTime: &quot;2026-09-22T13:50:06Z&quot;
    message: Deployment has minimum availability.
    reason: MinimumReplicasAvailable
    status: &quot;True&quot;
    type: Available
  - lastTransitionTime: &quot;2026-09-22T13:50:05Z&quot;
    lastUpdateTime: &quot;2026-09-22T13:50:06Z&quot;
    message: ReplicaSet &quot;troubleshooting-app-59d4957864&quot; has successfully progressed.
    reason: NewReplicaSetAvailable
    status: &quot;True&quot;
    type: Progressing
  observedGeneration: 1
  readyReplicas: 2
  replicas: 2
  terminatingReplicas: 0
  updatedReplicas: 2
<span style="color: #4ade80; font-weight: bold;">amitabh@LAPTOP-3KF17VR3</span>:<span style="color: #60a5fa;">/mnt/c/Users/USER/Downloads/devops-heros-branch10104-main/devops-heros-branch10104-main/session-14-kubernetes-troubleshooting/mini-project</span>$ kubectl apply -f service.yaml
service/troubleshooting-service configured
<span style="color: #4ade80; font-weight: bold;">amitabh@LAPTOP-3KF17VR3</span>:<span style="color: #60a5fa;">/mnt/c/Users/USER/Downloads/devops-heros-branch10104-main/devops-heros-branch10104-main/session-14-kubernetes-troubleshooting/mini-project</span>$ kubectl get endpoints troubleshooting-service
Warning: v1 Endpoints is deprecated in v1.33+; use discovery.k8s.io/v1 EndpointSlice
NAME                      ENDPOINTS   AGE
troubleshooting-service   &lt;none&gt;      36m
</code></pre>
