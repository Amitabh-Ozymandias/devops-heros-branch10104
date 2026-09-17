ConfigMap-01:

amitabh@LAPTOP-3KF17VR3:/mnt/c/Users/USER/Downloads/devops-heros-branch10104-main/devops-heros-branch10104-main/session-11-kubernetes-services$ cd ..
amitabh@LAPTOP-3KF17VR3:/mnt/c/Users/USER/Downloads/devops-heros-branch10104-main/devops-heros-branch10104-main$ cd session-12-ingress-configmaps-secrets
amitabh@LAPTOP-3KF17VR3:/mnt/c/Users/USER/Downloads/devops-heros-branch10104-main/devops-heros-branch10104-main/session-12-ingress-configmaps-secrets$ ls
01-configmap  02-secret  03-ingress  04-full-demo  lab.md  troubleshooting
amitabh@LAPTOP-3KF17VR3:/mnt/c/Users/USER/Downloads/devops-heros-branch10104-main/devops-heros-branch10104-main/session-12-ingress-configmaps-secrets$ cd 01-configmap
amitabh@LAPTOP-3KF17VR3:/mnt/c/Users/USER/Downloads/devops-heros-branch10104-main/devops-heros-branch10104-main/session-12-ingress-configmaps-secrets/01-configmap$ kubectl apply -f configmap/app-config.yaml
error: the path "configmap/app-config.yaml" does not exist
amitabh@LAPTOP-3KF17VR3:/mnt/c/Users/USER/Downloads/devops-heros-branch10104-main/devops-heros-branch10104-main/session-12-ingress-configmaps-secrets/01-configmap$ kubectl apply -f app-config.yaml
configmap/yatri-app-config created
amitabh@LAPTOP-3KF17VR3:/mnt/c/Users/USER/Downloads/devops-heros-branch10104-main/devops-heros-branch10104-main/session-12-ingress-configmaps-secrets/01-configmap$ kubectl get yatri-app-config
error: the server doesn't have a resource type "yatri-app-config"
amitabh@LAPTOP-3KF17VR3:/mnt/c/Users/USER/Downloads/devops-heros-branch10104-main/devops-heros-branch10104-main/session-12-ingress-configmaps-secrets/01-configmap$ kubectl get configmap yatri-app-config
NAME               DATA   AGE
yatri-app-config   5      24s
amitabh@LAPTOP-3KF17VR3:/mnt/c/Users/USER/Downloads/devops-heros-branch10104-main/devops-heros-branch10104-main/session-12-ingress-configmaps-secrets/01-configmap$ kubectl describe configmap yatri-app-config
Name:         yatri-app-config
Namespace:    default
Labels:       app=yatri-backend
Annotations:  <none>

Data
====
DEFAULT_CURRENCY:
----
INR

ENVIRONMENT:
----
production

LOG_LEVEL:
----
INFO

MAX_BOOKING_DAYS:
----
30

PORT:
----
5000


BinaryData
====

Events:  <none>


Secret-02:

amitabh@LAPTOP-3KF17VR3:/mnt/c/Users/USER/Downloads/devops-heros-branch10104-main/devops-heros-branch10104-main/session-12-ingress-configmaps-secrets/01-configmap$ kubectl apply -f db-secret.yaml
amitabh@LAPTOP-3KF17VR3:/mnt/c/Users/USER/Downloads/devops-heros-branch10104-main/devops-heros-branch10104-main/session-12-ingress-configmaps-secrets/01-configmap$ cd ..
amitabh@LAPTOP-3KF17VR3:/mnt/c/Users/USER/Downloads/devops-heros-branch10104-main/devops-heros-branch10104-main/session-12-ingress-configmaps-secrets$ ls
01-configmap  02-secret  03-ingress  04-full-demo  lab.md  troubleshooting
amitabh@LAPTOP-3KF17VR3:/mnt/c/Users/USER/Downloads/devops-heros-branch10104-main/devops-heros-branch10104-main/session-12-ingress-configmaps-secrets$ cd 02-secret
amitabh@LAPTOP-3KF17VR3:/mnt/c/Users/USER/Downloads/devops-heros-branch10104-main/devops-heros-branch10104-main/session-12-ingress-configmaps-secrets/02-secret$ kubectl apply -f secret/db-secret.yaml
error: the path "secret/db-secret.yaml" does not exist
amitabh@LAPTOP-3KF17VR3:/mnt/c/Users/USER/Downloads/devops-heros-branch10104-main/devops-heros-branch10104-main/session-12-ingress-configmaps-secrets/02-secret$ kubectl apply -f db-secret.yaml
secret/yatri-db-secret created
amitabh@LAPTOP-3KF17VR3:/mnt/c/Users/USER/Downloads/devops-heros-branch10104-main/devops-heros-branch10104-main/session-12-ingress-configmaps-secrets/02-secret$ kubectl get secret yatri-db-secret
NAME              TYPE     DATA   AGE
yatri-db-secret   Opaque   3      8s
amitabh@LAPTOP-3KF17VR3:/mnt/c/Users/USER/Downloads/devops-heros-branch10104-main/devops-heros-branch10104-main/session-12-ingress-configmaps-secrets/02-secret$ ^C
amitabh@LAPTOP-3KF17VR3:/mnt/c/Users/USER/Downloads/devops-heros-branch10104-main/devops-heros-branch10104-main/session-12-ingress-configmaps-secrets/02-secret$ kubectl get secret yatri-db-secret -o jsonpath='{.data.POSTGRES_PASSWORD}' | base64 --decode
secretpasswordamitabh@LAPTOP-3KF17VR3:/mnt/c/Users/USER/Downloads/devops-heros-branch10104-main/devops-heros-branch10104-main/session-12-ingress-configmaps-secreecho -n "yatri_admin" | base64dmin" | base64
eWF0cmlfYWRtaW4=
amitabh@LAPTOP-3KF17VR3:/mnt/c/Users/USER/Downloads/devops-heros-branch10104-main/devops-heros-branch10104-main/session-12-ingress-configmaps-secrets/02-secret$ echo -n "secretpassword" | base64
c2VjcmV0cGFzc3dvcmQ=
amitabh@LAPTOP-3KF17VR3:/mnt/c/Users/USER/Downloads/devops-heros-branch10104-main/devops-heros-branch10104-main/session-12-ingress-configmaps-secrets/02-secret$ echo -n "yatri_production_db" | base64
eWF0cmlfcHJvZHVjdGlvbl9kYg==

FullDemo_04:
amitabh@LAPTOP-3KF17VR3:/mnt/c/Users/USER/Downloads/devops-heros-branch10104-main/devops-heros-branch10104-main$ cd session-12-ingress-configmaps-secrets
amitabh@LAPTOP-3KF17VR3:/mnt/c/Users/USER/Downloads/devops-heros-branch10104-main/devops-heros-branch10104-main/session-12-ingress-configmaps-secrets$ cd 04-full-demo
amitabh@LAPTOP-3KF17VR3:/mnt/c/Users/USER/Downloads/devops-heros-branch10104-main/devops-heros-branch10104-main/session-12-ingress-configmaps-secrets/04-full-demo$ minikube start docker-desktop
😄  minikube v1.39.0 on Ubuntu 26.04 (kvm/amd64)
✨  Using the docker driver based on existing profile
👍  Starting "minikube" primary control-plane node in "minikube" cluster
🚜  Pulling base image v0.0.51 ...
🔄  Restarting existing docker container for "minikube" ...
📦  Preparing Kubernetes v1.37.0 on containerd 2.3.4 ...
🔎  Verifying Kubernetes components...
    ▪ Using image gcr.io/k8s-minikube/storage-provisioner:v5
    ▪ Using image registry.k8s.io/ingress-nginx/kube-webhook-certgen:v1.6.9
    ▪ Using image registry.k8s.io/ingress-nginx/controller:v1.15.1
    ▪ Using image registry.k8s.io/ingress-nginx/kube-webhook-certgen:v1.6.9
🔎  Verifying ingress addon...
🌟  Enabled addons: default-storageclass, storage-provisioner, ingress

❗  /usr/local/bin/kubectl is version 1.34.1, which may have incompatibilities with Kubernetes 1.37.0.
    ▪ Want kubectl v1.37.0? Try 'minikube kubectl -- get pods -A'
🏄  Done! kubectl is now configured to use "minikube" cluster and "default" namespace by default
amitabh@LAPTOP-3KF17VR3:/mnt/c/Users/USER/Downloads/devops-heros-branch10104-main/devops-heros-branch10104-main/session-12-ingress-configmaps-secrets/04-full-demo$ minikube status
minikube
type: Control Plane
host: Running
kubelet: Running
apiserver: Running
kubeconfig: Configured

amitabh@LAPTOP-3KF17VR3:/mnt/c/Users/USER/Downloads/devops-heros-branch10104-main/devops-heros-branch10104-main/session-12-ingress-configmaps-secrets/04-full-demo$ kubectl config current-context
minikube
amitabh@LAPTOP-3KF17VR3:/mnt/c/Users/USER/Downloads/devops-heros-branch10104-main/devops-heros-branch10104-main/session-12-ingress-configmaps-secrets/04-full-demo$ kubectl apply -f 04-full-demo/configmap.yaml
kubectl describe configmap yatri-app-config
error: the path "04-full-demo/configmap.yaml" does not exist
Name:         yatri-app-config
Namespace:    default
Labels:       app=yatri-backend
Annotations:  <none>

Data
====
DEFAULT_CURRENCY:
----
INR

ENVIRONMENT:
----
production

LOG_LEVEL:
----
INFO

MAX_BOOKING_DAYS:
----
30

PORT:
----
5000


BinaryData
====

Events:  <none>
amitabh@LAPTOP-3KF17VR3:/mnt/c/Users/USER/Downloads/devops-heros-branch10104-main/devops-heros-branch10104-main/session-12-ingress-configmaps-secrets/04-full-demo$ kubectl apply -f configmap.yaml
kubectl describe configmap yatri-app-config
configmap/yatri-app-config configured
Name:         yatri-app-config
Namespace:    default
Labels:       app=yatri-app
Annotations:  <none>

Data
====
APP_PORT:
----
5000

DEFAULT_CURRENCY:
----
INR

ENVIRONMENT:
----
production

LOG_LEVEL:
----
INFO

MAX_BOOKING_DAYS:
----
30


BinaryData
====

Events:  <none>
amitabh@LAPTOP-3KF17VR3:/mnt/c/Users/USER/Downloads/devops-heros-branch10104-main/devops-heros-branch10104-main/session-12-ingress-configmaps-secrets/04-full-demo$ kubectl apply -f secret.yaml
kubectl describe secret yatri-db-secret
secret/yatri-db-secret configured
Name:         yatri-db-secret
Namespace:    default
Labels:       app=yatri-app
Annotations:  <none>

Type:  Opaque

Data
====
POSTGRES_DB:        19 bytes
POSTGRES_PASSWORD:  14 bytes
POSTGRES_USER:      11 bytes
amitabh@LAPTOP-3KF17VR3:/mnt/c/Users/USER/Downloads/devops-heros-branch10104-main/devops-heros-branch10104-main/session-12-ingress-configmaps-secrets/04-full-demo$ kubectl apply -f frontend.yaml
deployment.apps/yatri-frontend created
service/yatri-frontend-service created
amitabh@LAPTOP-3KF17VR3:/mnt/c/Users/USER/Downloads/devops-heros-branch10104-main/devops-heros-branch10104-main/session-12-ingress-configmaps-secrets/04-full-demo$ kubectl get pods -l app=yatri-frontend
kubectl get svc yatri-frontend-service
NAME                             READY   STATUS    RESTARTS   AGE
yatri-frontend-ddcfc4b5f-j7czj   1/1     Running   0          14s
yatri-frontend-ddcfc4b5f-p4v4d   1/1     Running   0          14s
NAME                     TYPE        CLUSTER-IP      EXTERNAL-IP   PORT(S)   AGE
yatri-frontend-service   ClusterIP   10.107.93.193   <none>        80/TCP    14s
amitabh@LAPTOP-3KF17VR3:/mnt/c/Users/USER/Downloads/devops-heros-branch10104-main/devops-heros-branch10104-main/session-12-ingress-configmaps-secrets/04-full-demo$ kubectl apply -f backend.yaml
deployment.apps/yatri-backend created
service/yatri-backend-service created
amitabh@LAPTOP-3KF17VR3:/mnt/c/Users/USER/Downloads/devops-heros-branch10104-main/devops-heros-branch10104-main/session-12-ingress-configmaps-secrets/04-full-demo$ kubectl rollout status deployment/yatri-backend --timeout=90s
deployment "yatri-backend" successfully rolled out
amitabh@LAPTOP-3KF17VR3:/mnt/c/Users/USER/Downloads/devops-heros-branch10104-main/devops-heros-branch10104-main/session-12-ingress-configmaps-secrets/04-full-demo$ kubectl get pods -l app=yatri-backend
kubectl get svc yatri-backend-service
NAME                             READY   STATUS    RESTARTS   AGE
yatri-backend-6c58cb99c7-db4hk   1/1     Running   0          32s
yatri-backend-6c58cb99c7-fbfzt   1/1     Running   0          32s
NAME                    TYPE        CLUSTER-IP    EXTERNAL-IP   PORT(S)   AGE
yatri-backend-service   ClusterIP   10.97.215.2   <none>        80/TCP    33s
amitabh@LAPTOP-3KF17VR3:/mnt/c/Users/USER/Downloads/devops-heros-branch10104-main/devops-heros-branch10104-main/session-12-ingress-configmaps-secrets/04-full-demo$ kubectl apply -f ingress.yaml
ingress.networking.k8s.io/yatri-ingress configured
amitabh@LAPTOP-3KF17VR3:/mnt/c/Users/USER/Downloads/devops-heros-branch10104-main/devops-heros-branch10104-main/session-12-ingress-configmaps-secrets/04-full-demo$ kubectl get ingress yatri-ingress
kubectl describe ingress yatri-ingress
NAME            CLASS   HOSTS         ADDRESS        PORTS   AGE
yatri-ingress   nginx   yatri.local   192.168.49.2   80      90m
Name:             yatri-ingress
Labels:           app=yatri-app
Namespace:        default
Address:          192.168.49.2
Ingress Class:    nginx
Default backend:  <default>
Rules:
  Host         Path  Backends
  ----         ----  --------
  yatri.local  
               /api(/|$)(.*)   yatri-backend-service:80 (10.244.0.6:5000,10.244.0.7:5000)
               /               yatri-frontend-service:80 (10.244.0.5:80,10.244.0.4:80)
Annotations:   nginx.ingress.kubernetes.io/rewrite-target: /$2
               nginx.ingress.kubernetes.io/ssl-redirect: false
               nginx.ingress.kubernetes.io/use-regex: true
Events:
  Type    Reason  Age                  From                      Message
  ----    ------  ----                 ----                      -------
  Normal  Sync    83m (x2 over 84m)    nginx-ingress-controller  Scheduled for sync
  Normal  Sync    59m (x3 over 60m)    nginx-ingress-controller  Scheduled for sync
  Normal  Sync    10s (x4 over 9m58s)  nginx-ingress-controller  Scheduled for sync
amitabh@LAPTOP-3KF17VR3:/mnt/c/Users/USER/Downloads/devops-heros-branch10104-main/devops-heros-branch10104-main/session-12-ingress-configmaps-secrets/04-full-demo$ echo "$(minikube ip) yatri.local" | sudo tee -a /etc/hosts
[sudo: authenticate] Password:          
sudo: Authentication failed, try again.
[sudo: authenticate] Password:        
sudo: Authentication failed, try again.
[sudo: authenticate] Password: 

amitabh@LAPTOP-3KF17VR3:/mnt/c/Users/USER/Downloads/devops-heros-branch10104-main/devops-heros-branch10104-main/session-12-ingress-configmaps-secrets/04-full-demo$ echo "$(minikube ip) yatri.local" | sudo tee -a /etc/hosts
[sudo: authenticate] Password:        
192.168.49.2 yatri.local
amitabh@LAPTOP-3KF17VR3:/mnt/c/Users/USER/Downloads/devops-heros-branch10104-main/devops-heros-branch10104-main/session-12-ingress-configmaps-secrets/04-full-demo$ cat /etc/hosts | grep yatri.local
192.168.49.2 yatri.local
amitabh@LAPTOP-3KF17VR3:/mnt/c/Users/USER/Downloads/devops-heros-branch10104-main/devops-heros-branch10104-main/session-12-ingress-configmaps-secrets/04-full-demo$ curl http://yatri.local
^C
amitabh@LAPTOP-3KF17VR3:/mnt/c/Users/USER/Downloads/devops-heros-branch10104-main/devops-heros-branch10104-main/session-12-ingress-configmaps-secrets/04-full-demo$ getent hosts yatri.local
192.168.49.2    yatri.local
amitabh@LAPTOP-3KF17VR3:/mnt/c/Users/USER/Downloads/devops-heros-branch10104-main/devops-heros-branch10104-main/session-12-ingress-configmaps-secrets/04-full-demo$ curl -v --max-time 10 http://yatri.local
* Host yatri.local:80 was resolved.
* IPv6: (none)
* IPv4: 192.168.49.2
*   Trying 192.168.49.2:80...
* Connection timed out after 10002 milliseconds
* closing connection #0
curl: (28) Connection timed out after 10002 milliseconds
amitabh@LAPTOP-3KF17VR3:/mnt/c/Users/USER/Downloads/devops-heros-branch10104-main/devops-heros-branch10104-main/session-12-ingress-configmaps-secrets/04-full-demo$ kubectl get pods -n ingress-nginx -o wide
NAME                                       READY   STATUS      RESTARTS      AGE   IP           NODE       NOMINATED NODE   READINESS GATES
ingress-nginx-admission-create-fs676       0/1     Completed   0             95m   <none>       minikube   <none>           <none>
ingress-nginx-admission-patch-fxld2        0/1     Completed   0             95m   <none>       minikube   <none>           <none>
ingress-nginx-controller-d7cd8c989-hm9x7   1/1     Running     2 (19m ago)   95m   10.244.0.3   minikube   <none>           <none>
amitabh@LAPTOP-3KF17VR3:/mnt/c/Users/USER/Downloads/devops-heros-branch10104-main/devops-heros-branch10104-main/session-12-ingress-configmaps-secrets/04-full-demo$ kubectl get svc -n ingress-nginx
NAME                                 TYPE        CLUSTER-IP       EXTERNAL-IP   PORT(S)                      AGE
ingress-nginx-controller             NodePort    10.107.181.154   <none>        80:32461/TCP,443:31953/TCP   96m
ingress-nginx-controller-admission   ClusterIP   10.106.230.169   <none>        443/TCP                      96m
amitabh@LAPTOP-3KF17VR3:/mnt/c/Users/USER/Downloads/devops-heros-branch10104-main/devops-heros-branch10104-main/session-12-ingress-configmaps-secrets/04-full-demo$ minikube ip
192.168.49.2
amitabh@LAPTOP-3KF17VR3:/mnt/c/Users/USER/Downloads/devops-heros-branch10104-main/devops-heros-branch10104-main/session-12-ingress-configmaps-secrets/04-full-demo$ minikube ssh -- curl -v --max-time 5 -H "Host: yatri.local" http://192.168.49.2
* Could not resolve host: yatri.local
* Closing connection 0
curl: (6) Could not resolve host: yatri.local
*   Trying 192.168.49.2:80...
* Connected to 192.168.49.2 (192.168.49.2) port 80 (#1)
> GET / HTTP/1.1
> User-Agent: curl/7.88.1
> Accept: */*
> 
< HTTP/1.1 400 Bad Request
< Date: Thu, 17 Sep 2026 12:01:16 GMT
< Content-Type: text/html
< Content-Length: 150
< Connection: close
< 
<html>
<head><title>400 Bad Request</title></head>
<body>
<center><h1>400 Bad Request</h1></center>
<hr><center>nginx</center>
</body>
</html>
* Closing connection 1
amitabh@LAPTOP-3KF17VR3:/mnt/c/Users/USER/Downloads/devops-heros-branch10104-main/devops-heros-branch10104-main/session-12-ingress-configmaps-secrets/04-full-demo$ minikube ssh -- curl -v --max-time 5 -H 'Host: yatri.local' http://192.168.49.2/
* Could not resolve host: yatri.local
* Closing connection 0
curl: (6) Could not resolve host: yatri.local
*   Trying 192.168.49.2:80...
* Connected to 192.168.49.2 (192.168.49.2) port 80 (#1)
> GET / HTTP/1.1
> User-Agent: curl/7.88.1
> Accept: */*
> 
< HTTP/1.1 400 Bad Request
< Date: Thu, 17 Sep 2026 12:02:17 GMT
< Content-Type: text/html
< Content-Length: 150
< Connection: close
< 
<html>
<head><title>400 Bad Request</title></head>
<body>
<center><h1>400 Bad Request</h1></center>
<hr><center>nginx</center>
</body>
</html>
* Closing connection 1
amitabh@LAPTOP-3KF17VR3:/mnt/c/Users/USER/Downloads/devops-heros-branch10104-main/devops-heros-branch10104-main/session-12-ingress-configmaps-secrets/04-full-demo$ minikube ssh -- curl -v --max-time 5 -H 'Host: yatri.local' http://192.168.49.2/api/
* Could not resolve host: yatri.local
* Closing connection 0
curl: (6) Could not resolve host: yatri.local
*   Trying 192.168.49.2:80...
* Connected to 192.168.49.2 (192.168.49.2) port 80 (#1)
> GET /api/ HTTP/1.1
> User-Agent: curl/7.88.1
> Accept: */*
> 
< HTTP/1.1 400 Bad Request
< Date: Thu, 17 Sep 2026 12:02:40 GMT
< Content-Type: text/html
< Content-Length: 150
< Connection: close
< 
<html>
<head><title>400 Bad Request</title></head>
<body>
<center><h1>400 Bad Request</h1></center>
<hr><center>nginx</center>
</body>
</html>
* Closing connection 1
amitabh@LAPTOP-3KF17VR3:/mnt/c/Users/USER/Downloads/devops-heros-branch10104-main/devops-heros-branch10104-main/session-12-ingress-configmaps-secrets/04-full-demo$ kubectl get ingress yatri-ingress -o yaml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  annotations:
    kubectl.kubernetes.io/last-applied-configuration: |
      {"apiVersion":"networking.k8s.io/v1","kind":"Ingress","metadata":{"annotations":{"nginx.ingress.kubernetes.io/rewrite-target":"/$2","nginx.ingress.kubernetes.io/ssl-redirect":"false","nginx.ingress.kubernetes.io/use-regex":"true"},"labels":{"app":"yatri-app"},"name":"yatri-ingress","namespace":"default"},"spec":{"ingressClassName":"nginx","rules":[{"host":"yatri.local","http":{"paths":[{"backend":{"service":{"name":"yatri-backend-service","port":{"number":80}}},"path":"/api(/|$)(.*)","pathType":"ImplementationSpecific"},{"backend":{"service":{"name":"yatri-frontend-service","port":{"number":80}}},"path":"/","pathType":"Prefix"}]}}]}}
    nginx.ingress.kubernetes.io/rewrite-target: /$2
    nginx.ingress.kubernetes.io/ssl-redirect: "false"
    nginx.ingress.kubernetes.io/use-regex: "true"
  creationTimestamp: "2026-09-17T10:21:16Z"
  generation: 1
  labels:
    app: yatri-app
  name: yatri-ingress
  namespace: default
  resourceVersion: "7185"
  uid: d96fb78b-bd20-4fe5-86b1-636872d96e39
spec:
  ingressClassName: nginx
  rules:
  - host: yatri.local
    http:
      paths:
      - backend:
          service:
            name: yatri-backend-service
            port:
              number: 80
        path: /api(/|$)(.*)
        pathType: ImplementationSpecific
      - backend:
          service:
            name: yatri-frontend-service
            port:
              number: 80
        path: /
        pathType: Prefix
status:
  loadBalancer:
    ingress:
    - ip: 192.168.49.2
amitabh@LAPTOP-3KF17VR3:/mnt/c/Users/USER/Downloads/devops-heros-branch10104-main/devops-heros-branch10104-main/session-12-ingress-configmaps-secrets/04-full-demo$ kubectl logs -n ingress-nginx deployment/ingress-nginx-controller --tail=50
I0917 11:41:19.180659       7 nginx.go:273] "Starting NGINX Ingress controller"
I0917 11:41:19.184077       7 event.go:377] Event(v1.ObjectReference{Kind:"ConfigMap", Namespace:"ingress-nginx", Name:"udp-services", UID:"abc42e4c-45ee-4716-9ad5-58c1210bfced", APIVersion:"v1", ResourceVersion:"5123", FieldPath:""}): type: 'Normal' reason: 'CREATE' ConfigMap ingress-nginx/udp-services
I0917 11:41:19.184165       7 event.go:377] Event(v1.ObjectReference{Kind:"ConfigMap", Namespace:"ingress-nginx", Name:"ingress-nginx-controller", UID:"ce6226df-1cb3-4110-9ee2-3751b92e3844", APIVersion:"v1", ResourceVersion:"5121", FieldPath:""}): type: 'Normal' reason: 'CREATE' ConfigMap ingress-nginx/ingress-nginx-controller
I0917 11:41:19.186114       7 event.go:377] Event(v1.ObjectReference{Kind:"ConfigMap", Namespace:"ingress-nginx", Name:"tcp-services", UID:"c6f3da99-f8a5-4245-9e3c-a0ad6b8e9898", APIVersion:"v1", ResourceVersion:"5122", FieldPath:""}): type: 'Normal' reason: 'CREATE' ConfigMap ingress-nginx/tcp-services
I0917 11:41:20.284304       7 store.go:443] "Found valid IngressClass" ingress="default/yatri-ingress" ingressclass="nginx"
I0917 11:41:20.284489       7 event.go:377] Event(v1.ObjectReference{Kind:"Ingress", Namespace:"default", Name:"yatri-ingress", UID:"d96fb78b-bd20-4fe5-86b1-636872d96e39", APIVersion:"networking.k8s.io/v1", ResourceVersion:"6159", FieldPath:""}): type: 'Normal' reason: 'Sync' Scheduled for sync
I0917 11:41:20.382328       7 nginx.go:319] "Starting NGINX process"
I0917 11:41:20.382400       7 leaderelection.go:258] "Attempting to acquire leader lease..." lock="ingress-nginx/ingress-nginx-leader"
I0917 11:41:20.383078       7 nginx.go:339] "Starting validation webhook" address=":8443" certPath="/usr/local/certificates/cert" keyPath="/usr/local/certificates/key"
W0917 11:41:20.383198       7 controller.go:1135] Error obtaining Endpoints for Service "default/yatri-backend-service": no object matching key "default/yatri-backend-service" in local store
W0917 11:41:20.383208       7 controller.go:1135] Error obtaining Endpoints for Service "default/yatri-frontend-service": no object matching key "default/yatri-frontend-service" in local store
I0917 11:41:20.383770       7 controller.go:217] "Configuration changes detected, backend reload required"
I0917 11:41:20.390053       7 leaderelection.go:272] "Successfully acquired lease" lock="ingress-nginx/ingress-nginx-leader"
I0917 11:41:20.390159       7 status.go:85] "New leader elected" identity="ingress-nginx-controller-d7cd8c989-hm9x7"
I0917 11:41:20.392911       7 status.go:224] "POD is not ready" pod="ingress-nginx/ingress-nginx-controller-d7cd8c989-hm9x7" node="minikube"
I0917 11:41:20.394716       7 status.go:311] "updating Ingress status" namespace="default" ingress="yatri-ingress" currentValue=[{"ip":"192.168.49.2"}] newValue=[]
I0917 11:41:20.400582       7 event.go:377] Event(v1.ObjectReference{Kind:"Ingress", Namespace:"default", Name:"yatri-ingress", UID:"d96fb78b-bd20-4fe5-86b1-636872d96e39", APIVersion:"networking.k8s.io/v1", ResourceVersion:"6478", FieldPath:""}): type: 'Normal' reason: 'Sync' Scheduled for sync
I0917 11:41:20.416306       7 controller.go:231] "Backend successfully reloaded"
I0917 11:41:20.416380       7 controller.go:243] "Initial sync, sleeping for 1 second"
I0917 11:41:20.416421       7 event.go:377] Event(v1.ObjectReference{Kind:"Pod", Namespace:"ingress-nginx", Name:"ingress-nginx-controller-d7cd8c989-hm9x7", UID:"1492902e-9e38-4e0d-9ea2-849a0bf19642", APIVersion:"v1", ResourceVersion:"6363", FieldPath:""}): type: 'Normal' reason: 'RELOAD' NGINX reload triggered due to a change in configuration
I0917 11:41:20.493076       7 status.go:224] "POD is not ready" pod="ingress-nginx/ingress-nginx-controller-d7cd8c989-hm9x7" node="minikube"
W0917 11:41:23.718048       7 controller.go:1135] Error obtaining Endpoints for Service "default/yatri-backend-service": no object matching key "default/yatri-backend-service" in local store
W0917 11:41:23.718098       7 controller.go:1135] Error obtaining Endpoints for Service "default/yatri-frontend-service": no object matching key "default/yatri-frontend-service" in local store
W0917 11:41:27.052608       7 controller.go:1135] Error obtaining Endpoints for Service "default/yatri-backend-service": no object matching key "default/yatri-backend-service" in local store
W0917 11:41:27.052666       7 controller.go:1135] Error obtaining Endpoints for Service "default/yatri-frontend-service": no object matching key "default/yatri-frontend-service" in local store
W0917 11:41:30.383524       7 controller.go:1135] Error obtaining Endpoints for Service "default/yatri-backend-service": no object matching key "default/yatri-backend-service" in local store
W0917 11:41:30.383576       7 controller.go:1135] Error obtaining Endpoints for Service "default/yatri-frontend-service": no object matching key "default/yatri-frontend-service" in local store
I0917 11:42:20.394016       7 status.go:311] "updating Ingress status" namespace="default" ingress="yatri-ingress" currentValue=null newValue=[{"ip":"192.168.49.2"}]
W0917 11:42:20.398806       7 controller.go:1135] Error obtaining Endpoints for Service "default/yatri-backend-service": no object matching key "default/yatri-backend-service" in local store
W0917 11:42:20.398831       7 controller.go:1135] Error obtaining Endpoints for Service "default/yatri-frontend-service": no object matching key "default/yatri-frontend-service" in local store
I0917 11:42:20.398914       7 event.go:377] Event(v1.ObjectReference{Kind:"Ingress", Namespace:"default", Name:"yatri-ingress", UID:"d96fb78b-bd20-4fe5-86b1-636872d96e39", APIVersion:"networking.k8s.io/v1", ResourceVersion:"6551", FieldPath:""}): type: 'Normal' reason: 'Sync' Scheduled for sync
W0917 11:49:43.027561       7 controller.go:1135] Error obtaining Endpoints for Service "default/yatri-backend-service": no object matching key "default/yatri-backend-service" in local store
W0917 11:49:43.029497       7 controller.go:1241] Service "default/yatri-frontend-service" does not have any active Endpoint.
I0917 11:49:43.030761       7 controller.go:217] "Configuration changes detected, backend reload required"
I0917 11:49:43.095736       7 controller.go:231] "Backend successfully reloaded"
I0917 11:49:43.096174       7 event.go:377] Event(v1.ObjectReference{Kind:"Pod", Namespace:"ingress-nginx", Name:"ingress-nginx-controller-d7cd8c989-hm9x7", UID:"1492902e-9e38-4e0d-9ea2-849a0bf19642", APIVersion:"v1", ResourceVersion:"6363", FieldPath:""}): type: 'Normal' reason: 'RELOAD' NGINX reload triggered due to a change in configuration
W0917 11:49:46.362432       7 controller.go:1135] Error obtaining Endpoints for Service "default/yatri-backend-service": no object matching key "default/yatri-backend-service" in local store
W0917 11:49:49.694302       7 controller.go:1135] Error obtaining Endpoints for Service "default/yatri-backend-service": no object matching key "default/yatri-backend-service" in local store
W0917 11:50:16.052710       7 controller.go:1241] Service "default/yatri-backend-service" does not have any active Endpoint.
I0917 11:50:16.054020       7 controller.go:217] "Configuration changes detected, backend reload required"
I0917 11:50:16.108387       7 controller.go:231] "Backend successfully reloaded"
I0917 11:50:16.108692       7 event.go:377] Event(v1.ObjectReference{Kind:"Pod", Namespace:"ingress-nginx", Name:"ingress-nginx-controller-d7cd8c989-hm9x7", UID:"1492902e-9e38-4e0d-9ea2-849a0bf19642", APIVersion:"v1", ResourceVersion:"6363", FieldPath:""}): type: 'Normal' reason: 'RELOAD' NGINX reload triggered due to a change in configuration
I0917 11:51:08.113651       7 main.go:107] "successfully validated configuration, accepting" ingress="default/yatri-ingress"
I0917 11:51:08.117716       7 event.go:377] Event(v1.ObjectReference{Kind:"Ingress", Namespace:"default", Name:"yatri-ingress", UID:"d96fb78b-bd20-4fe5-86b1-636872d96e39", APIVersion:"networking.k8s.io/v1", ResourceVersion:"7185", FieldPath:""}): type: 'Normal' reason: 'Sync' Scheduled for sync
I0917 11:51:08.118417       7 controller.go:217] "Configuration changes detected, backend reload required"
I0917 11:51:08.146184       7 controller.go:231] "Backend successfully reloaded"
I0917 11:51:08.146553       7 event.go:377] Event(v1.ObjectReference{Kind:"Pod", Namespace:"ingress-nginx", Name:"ingress-nginx-controller-d7cd8c989-hm9x7", UID:"1492902e-9e38-4e0d-9ea2-849a0bf19642", APIVersion:"v1", ResourceVersion:"6363", FieldPath:""}): type: 'Normal' reason: 'RELOAD' NGINX reload triggered due to a change in configuration
192.168.49.2 - - [17/Sep/2026:12:01:16 +0000] "GET / HTTP/1.1" 400 150 "-" "curl/7.88.1" 56 0.000 [] [] - - - - d80e3ff5d5315c04615eff891aa5c6f1
192.168.49.2 - - [17/Sep/2026:12:02:17 +0000] "GET / HTTP/1.1" 400 150 "-" "curl/7.88.1" 56 0.000 [] [] - - - - 584bbc4022e7032059ed114b045d3881
192.168.49.2 - - [17/Sep/2026:12:02:40 +0000] "GET /api/ HTTP/1.1" 400 150 "-" "curl/7.88.1" 60 0.000 [] [] - - - - 80c64cc16430a154742b90a0c5f20cd9
amitabh@LAPTOP-3KF17VR3:/mnt/c/Users/USER/Downloads/devops-heros-branch10104-main/devops-heros-branch10104-main/session-12-ingress-configmaps-secrets/04-full-demo$ kubectl get ingressclass
NAME              CONTROLLER             PARAMETERS   AGE
nginx (default)   k8s.io/ingress-nginx   <none>       99m
amitabh@LAPTOP-3KF17VR3:/mnt/c/Users/USER/Downloads/devops-heros-branch10104-main/devops-heros-branch10104-main/session-12-ingress-configmaps-secrets/04-full-demo$ kubectl get svc yatri-frontend-service yatri-backend-service
NAME                     TYPE        CLUSTER-IP      EXTERNAL-IP   PORT(S)   AGE
yatri-frontend-service   ClusterIP   10.107.93.193   <none>        80/TCP    14m
yatri-backend-service    ClusterIP   10.97.215.2     <none>        80/TCP    14m
amitabh@LAPTOP-3KF17VR3:/mnt/c/Users/USER/Downloads/devops-heros-branch10104-main/devops-heros-branch10104-main/session-12-ingress-configmaps-secrets/04-full-demo$ curl -v --max-time 10 -H "Host: yatri.local" http://192.168.49.2/
*   Trying 192.168.49.2:80...
* Connection timed out after 10002 milliseconds
* closing connection #0
curl: (28) Connection timed out after 10002 milliseconds
amitabh@LAPTOP-3KF17VR3:/mnt/c/Users/USER/Downloads/devops-heros-branch10104-main/devops-heros-branch10104-main/session-12-ingress-configmaps-secrets/04-full-demo$ kubectl get pods -o wide
NAME                             READY   STATUS    RESTARTS   AGE   IP           NODE       NOMINATED NODE   READINESS GATES
yatri-backend-6c58cb99c7-db4hk   1/1     Running   0          15m   10.244.0.6   minikube   <none>           <none>
yatri-backend-6c58cb99c7-fbfzt   1/1     Running   0          15m   10.244.0.7   minikube   <none>           <none>
yatri-frontend-ddcfc4b5f-j7czj   1/1     Running   0          15m   10.244.0.5   minikube   <none>           <none>
yatri-frontend-ddcfc4b5f-p4v4d   1/1     Running   0          15m   10.244.0.4   minikube   <none>           <none>
amitabh@LAPTOP-3KF17VR3:/mnt/c/Users/USER/Downloads/devops-heros-branch10104-main/devops-heros-branch10104-main/session-12-ingress-configmaps-secrets/04-full-demo$ kubectl get endpoints yatri-frontend-service yatri-backend-service
Warning: v1 Endpoints is deprecated in v1.33+; use discovery.k8s.io/v1 EndpointSlice
NAME                     ENDPOINTS                         AGE
yatri-frontend-service   10.244.0.4:80,10.244.0.5:80       15m
yatri-backend-service    10.244.0.6:5000,10.244.0.7:5000   15m
amitabh@LAPTOP-3KF17VR3:/mnt/c/Users/USER/Downloads/devops-heros-branch10104-main/devops-heros-branch10104-main/session-12-ingress-configmaps-secrets/04-full-demo$ kubectl run test-curl --rm -it --image=curlimages/curl -- sh
All commands and output from this session will be recorded in container logs, including credentials and sensitive information passed through the command prompt.
If you don't see a command prompt, try pressing enter.
~ $ curl -v http://yatri-frontend-service
* Host yatri-frontend-service:80 was resolved.
* IPv6: (none)
* IPv4: 10.107.93.193
*   Trying 10.107.93.193:80...
* Established connection to yatri-frontend-service (10.107.93.193 port 80) from 10.244.0.8 port 51738 
* using HTTP/1.x
> GET / HTTP/1.1
> Host: yatri-frontend-service
> User-Agent: curl/8.22.0
> Accept: */*
> 
* Request completely sent off
< HTTP/1.1 200 OK
< Server: nginx/1.25.5
< Date: Thu, 17 Sep 2026 12:06:22 GMT
< Content-Type: text/html
< Content-Length: 615
< Last-Modified: Tue, 16 Apr 2024 15:47:06 GMT
< Connection: keep-alive
< ETag: "661e9d7a-267"
< Accept-Ranges: bytes
< 
<!DOCTYPE html>
<html>
<head>
<title>Welcome to nginx!</title>
<style>
html { color-scheme: light dark; }
body { width: 35em; margin: 0 auto;
font-family: Tahoma, Verdana, Arial, sans-serif; }
</style>
</head>
<body>
<h1>Welcome to nginx!</h1>
<p>If you see this page, the nginx web server is successfully installed and
working. Further configuration is required.</p>

<p>For online documentation and support please refer to
<a href="http://nginx.org/">nginx.org</a>.<br/>
Commercial support is available at
<a href="http://nginx.com/">nginx.com</a>.</p>

<p><em>Thank you for using nginx.</em></p>
</body>
</html>
* Connection #0 to host yatri-frontend-service:80 left intact
~ $ curl -v http://yatri-backend-service
* Host yatri-backend-service:80 was resolved.
* IPv6: (none)
* IPv4: 10.97.215.2
*   Trying 10.97.215.2:80...
* Established connection to yatri-backend-service (10.97.215.2 port 80) from 10.244.0.8 port 51924 
* using HTTP/1.x
> GET / HTTP/1.1
> Host: yatri-backend-service
> User-Agent: curl/8.22.0
> Accept: */*
> 
* Request completely sent off
* HTTP 1.0, assume close after body
< HTTP/1.0 200 OK
< Server: BaseHTTP/0.6 Python/3.11.11
< Date: Thu, 17 Sep 2026 12:06:33 GMT
< Content-Type: text/plain
< Content-Length: 178
< 
Yatri Backend API
=================
ENVIRONMENT     : production
LOG_LEVEL       : INFO
DEFAULT_CURRENCY: INR
POSTGRES_USER   : yatri_admin
POSTGRES_DB     : yatri_production_db
* shutting down connection #0
~ $ exit
Session ended, resume using 'kubectl attach test-curl -c test-curl -i -t' command when the pod is running
pod "test-curl" deleted from default namespace
amitabh@LAPTOP-3KF17VR3:/mnt/c/Users/USER/Downloads/devops-heros-branch10104-main/devops-heros-branch10104-main/session-12-ingress-configmaps-secrets/04-full-demo$ curl -v --max-time 10 -H "Host: yatri.local" http://192.168.49.2/
*   Trying 192.168.49.2:80...
* Connection timed out after 10002 milliseconds
* closing connection #0
curl: (28) Connection timed out after 10002 milliseconds
amitabh@LAPTOP-3KF17VR3:/mnt/c/Users/USER/Downloads/devops-heros-branch10104-main/devops-heros-branch10104-main/session-12-ingress-configmaps-secrets/04-full-demo$ bash cleanup.sh
: invalid option nameet: pipefail
amitabh@LAPTOP-3KF17VR3:/mnt/c/Users/USER/Downloads/devops-heros-branch10104-main/devops-heros-branch10104-main/session-12-ingress-configmaps-secrets/04-full-demo$ kubectl get pods
kubectl get svc
kubectl get ingress
kubectl get configmap
kubectl get secret
NAME                             READY   STATUS    RESTARTS   AGE
yatri-backend-6c58cb99c7-db4hk   1/1     Running   0          20m
yatri-backend-6c58cb99c7-fbfzt   1/1     Running   0          20m
yatri-frontend-ddcfc4b5f-j7czj   1/1     Running   0          20m
yatri-frontend-ddcfc4b5f-p4v4d   1/1     Running   0          20m
NAME                     TYPE        CLUSTER-IP      EXTERNAL-IP   PORT(S)   AGE
kubernetes               ClusterIP   10.96.0.1       <none>        443/TCP   3h5m
yatri-backend-service    ClusterIP   10.97.215.2     <none>        80/TCP    20m
yatri-frontend-service   ClusterIP   10.107.93.193   <none>        80/TCP    20m
NAME            CLASS   HOSTS         ADDRESS        PORTS   AGE
yatri-ingress   nginx   yatri.local   192.168.49.2   80      109m
NAME               DATA   AGE
kube-root-ca.crt   1      3h5m
yatri-app-config   5      123m
NAME              TYPE     DATA   AGE
yatri-db-secret   Opaque   3      121m
amitabh@LAPTOP-3KF17VR3:/mnt/c/Users/USER/Downloads/devops-heros-branch10104-main/devops-heros-branch10104-main/session-12-ingress-configmaps-secrets/04-full-demo$ kubectl get pods | grep yatri
kubectl get svc | grep yatri
kubectl get ingress | grep yatri
yatri-backend-6c58cb99c7-db4hk   1/1     Running   0          20m
yatri-backend-6c58cb99c7-fbfzt   1/1     Running   0          20m
yatri-frontend-ddcfc4b5f-j7czj   1/1     Running   0          21m
yatri-frontend-ddcfc4b5f-p4v4d   1/1     Running   0          21m
yatri-backend-service    ClusterIP   10.97.215.2     <none>        80/TCP    20m
yatri-frontend-service   ClusterIP   10.107.93.193   <none>        80/TCP    21m
yatri-ingress   nginx   yatri.local   192.168.49.2   80      109m
amitabh@LAPTOP-3KF17VR3:/mnt/c/Users/USER/Downloads/devops-heros-branch10104-main/devops-heros-branch10104-main/session-12-ingress-configmaps-secrets/04-full-demo$ sed -i 's/\r$//' cleanup.sh
sed -i 's/\r$//' run-demo.sh
amitabh@LAPTOP-3KF17VR3:/mnt/c/Users/USER/Downloads/devops-heros-branch10104-main/devops-heros-branch10104-main/session-12-ingress-configmaps-secrets/04-full-demo$ head -5 cleanup.sh
#!/usr/bin/env bash
# cleanup.sh — Tear down all demo resources for Session 12
set -euo pipefail

DEMO_DIR="$(cd "$(dirname "${BASH_SOURCE[0]}")" && pwd)"
amitabh@LAPTOP-3KF17VR3:/mnt/c/Users/USER/Downloads/devops-heros-branch10104-main/devops-heros-branch10104-main/session-12-ingress-configmaps-secrets/04-full-demo$ bash cleanup.sh
[INFO] Deleting Ingress...
ingress.networking.k8s.io "yatri-ingress" deleted from default namespace
[INFO] Deleting Backend Deployment and Service...
deployment.apps "yatri-backend" deleted from default namespace
service "yatri-backend-service" deleted from default namespace
[INFO] Deleting Frontend Deployment and Service...
deployment.apps "yatri-frontend" deleted from default namespace
service "yatri-frontend-service" deleted from default namespace
[INFO] Deleting Secret...
secret "yatri-db-secret" deleted from default namespace
[INFO] Deleting ConfigMap...
configmap "yatri-app-config" deleted from default namespace
[INFO] All demo resources removed.
amitabh@LAPTOP-3KF17VR3:/mnt/c/Users/USER/Downloads/devops-heros-branch10104-main/devops-heros-branch10104-main/session-12-ingress-configmaps-secrets/04-full-demo$ kubectl get pods | grep yatri
kubectl get svc | grep yatri
kubectl get ingress | grep yatri
kubectl get configmap | grep yatri
kubectl get secret | grep yatri
yatri-backend-6c58cb99c7-db4hk   1/1     Terminating   0          25m
yatri-backend-6c58cb99c7-fbfzt   1/1     Terminating   0          25m
No resources found in default namespace.
No resources found in default namespace.
amitabh@LAPTOP-3KF17VR3:/mnt/c/Users/USER/Downloads/devops-heros-branch10104-main/devops-heros-branch10104-main/session-12-ingress-configmaps-secrets/04-full-demo$ bash run-demo.sh
[INFO] Step 1: Enabling NGINX Ingress Controller on Minikube...
💡  ingress is an addon maintained by Kubernetes. For any concerns contact minikube on GitHub.
You can view the list of minikube maintainers at: https://github.com/kubernetes/minikube/blob/master/OWNERS
    ▪ Using image registry.k8s.io/ingress-nginx/controller:v1.15.1
    ▪ Using image registry.k8s.io/ingress-nginx/kube-webhook-certgen:v1.6.9
    ▪ Using image registry.k8s.io/ingress-nginx/kube-webhook-certgen:v1.6.9
🔎  Verifying ingress addon...
🌟  The 'ingress' addon is enabled
[INFO] Waiting 30 seconds for Ingress Controller pods to become Ready...
pod/ingress-nginx-controller-d7cd8c989-hm9x7 condition met
[INFO] Ingress Controller is Ready.

[INFO] Step 2: Applying ConfigMap (plain-text configuration)...
configmap/yatri-app-config created
NAME               DATA   AGE
yatri-app-config   5      0s

[INFO] Step 3: Applying Secret (sensitive database credentials)...
secret/yatri-db-secret created
NAME              TYPE     DATA   AGE
yatri-db-secret   Opaque   3      0s

[INFO] Step 4: Deploying Frontend (Nginx) + ClusterIP Service...
deployment.apps/yatri-frontend created
service/yatri-frontend-service created

[INFO] Step 5: Deploying Backend (Python HTTP server) + ClusterIP Service...
deployment.apps/yatri-backend created
service/yatri-backend-service created

[INFO] Step 6: Waiting for all pods to reach Running state...
Waiting for deployment "yatri-frontend" rollout to finish: 0 of 2 updated replicas are available...
Waiting for deployment "yatri-frontend" rollout to finish: 1 of 2 updated replicas are available...
deployment "yatri-frontend" successfully rolled out
deployment "yatri-backend" successfully rolled out

[INFO] Step 7: Applying Ingress routing rules...
ingress.networking.k8s.io/yatri-ingress created

[INFO] Step 8: Summary of deployed resources...
NAME               DATA   AGE
yatri-app-config   5      1s
NAME              TYPE     DATA   AGE
yatri-db-secret   Opaque   3      1s
NAME                             READY   STATUS    RESTARTS   AGE
yatri-frontend-ddcfc4b5f-p6cwz   1/1     Running   0          1s
yatri-frontend-ddcfc4b5f-vmvwr   1/1     Running   0          1s
NAME                             READY   STATUS    RESTARTS   AGE
yatri-backend-6c58cb99c7-6dldg   1/1     Running   0          2s
yatri-backend-6c58cb99c7-gjlv9   1/1     Running   0          2s
NAME                     TYPE        CLUSTER-IP       EXTERNAL-IP   PORT(S)   AGE
yatri-frontend-service   ClusterIP   10.108.167.179   <none>        80/TCP    2s
yatri-backend-service    ClusterIP   10.98.12.236     <none>        80/TCP    2s
NAME            CLASS   HOSTS         ADDRESS   PORTS   AGE
yatri-ingress   nginx   yatri.local             80      1s

[INFO] Step 9: Adding yatri.local to /etc/hosts (requires sudo)...
[INFO] Minikube IP detected: 192.168.49.2
[INFO] yatri.local already exists in /etc/hosts. Skipping.

[INFO] ============================================================
[INFO] Demo is READY. Test with the following commands:

  Test FRONTEND (path: /):
    curl http://yatri.local
    OR open http://yatri.local in your browser

  Test BACKEND API (path: /api/) -- shows ConfigMap + Secret values:
    curl http://yatri.local/api/

  Verify environment variable injection inside backend pod:
    kubectl exec -it deploy/yatri-backend -- env | grep -E 'ENVIRONMENT|LOG_LEVEL|POSTGRES'

  Decode Secret password:
    kubectl get secret yatri-db-secret -o jsonpath='{.data.POSTGRES_PASSWORD}' | base64 --decode
[INFO] ============================================================
amitabh@LAPTOP-3KF17VR3:/mnt/c/Users/USER/Downloads/devops-heros-branch10104-main/devops-heros-branch10104-main/session-12-ingress-configmaps-secrets/04-full-demo$ kubectl get ingress yatri-ingress
NAME            CLASS   HOSTS         ADDRESS        PORTS   AGE
yatri-ingress   nginx   yatri.local   192.168.49.2   80      96s
amitabh@LAPTOP-3KF17VR3:/mnt/c/Users/USER/Downloads/devops-heros-branch10104-main/devops-heros-branch10104-main/session-12-ingress-configmaps-secrets/04-full-demo$ kubectl get ingress yatri-ingress -w
NAME            CLASS   HOSTS         ADDRESS        PORTS   AGE
yatri-ingress   nginx   yatri.local   192.168.49.2   80      109s
^Camitabh@LAPTOP-3KF17VR3:/mnt/c/Users/USER/Downloads/devops-heros-branch10104-main/devops-heros-branch10104-main/session-12-ingress-configmaps-secrets/04-full-demokubectl run ingress-test --rm -it --image=curlimages/curl -- shsh
All commands and output from this session will be recorded in container logs, including credentials and sensitive information passed through the command prompt.
If you don't see a command prompt, try pressing enter.
~ $ curl -v -H 'Host: yatri.local' http://192.168.49.2/
*   Trying 192.168.49.2:80...
* Established connection to 192.168.49.2 (192.168.49.2 port 80) from 10.244.0.13 port 55298 
* using HTTP/1.x
> GET / HTTP/1.1
> Host: yatri.local
> User-Agent: curl/8.22.0
> Accept: */*
> 
* Request completely sent off
< HTTP/1.1 200 OK
< Date: Thu, 17 Sep 2026 12:20:04 GMT
< Content-Type: text/html
< Content-Length: 615
< Connection: keep-alive
< Last-Modified: Tue, 16 Apr 2024 15:47:06 GMT
< ETag: "661e9d7a-267"
< Accept-Ranges: bytes
< 
<!DOCTYPE html>
<html>
<head>
<title>Welcome to nginx!</title>
<style>
html { color-scheme: light dark; }
body { width: 35em; margin: 0 auto;
font-family: Tahoma, Verdana, Arial, sans-serif; }
</style>
</head>
<body>
<h1>Welcome to nginx!</h1>
<p>If you see this page, the nginx web server is successfully installed and
working. Further configuration is required.</p>

<p>For online documentation and support please refer to
<a href="http://nginx.org/">nginx.org</a>.<br/>
Commercial support is available at
<a href="http://nginx.com/">nginx.com</a>.</p>

<p><em>Thank you for using nginx.</em></p>
</body>
</html>
* Connection #0 to host 192.168.49.2:80 left intact
~ $ curl -v -H 'Host: yatri.local' http://192.168.49.2/api/
*   Trying 192.168.49.2:80...
* Established connection to 192.168.49.2 (192.168.49.2 port 80) from 10.244.0.13 port 44550 
* using HTTP/1.x
> GET /api/ HTTP/1.1
> Host: yatri.local
> User-Agent: curl/8.22.0
> Accept: */*
> 
* Request completely sent off
< HTTP/1.1 200 OK
< Date: Thu, 17 Sep 2026 12:20:21 GMT
< Content-Type: text/plain
< Content-Length: 178
< Connection: keep-alive
< 
Yatri Backend API
=================
ENVIRONMENT     : production
LOG_LEVEL       : INFO
DEFAULT_CURRENCY: INR
POSTGRES_USER   : yatri_admin
POSTGRES_DB     : yatri_production_db
* Connection #0 to host 192.168.49.2:80 left intact
~ $ exit
Session ended, resume using 'kubectl attach ingress-test -c ingress-test -i -t' command when the pod is running
pod "ingress-test" deleted from default namespace
amitabh@LAPTOP-3KF17VR3:/mnt/c/Users/USER/Downloads/devops-heros-branch10104-main/devops-heros-branch10104-main/session-12-ingress-configmaps-secrets/04-full-demo$ curl -H "Host: yatri.local" http://127.0.0.1:8080/
<!DOCTYPE html>
<html>
<head>
<title>Welcome to nginx!</title>
<style>
html { color-scheme: light dark; }
body { width: 35em; margin: 0 auto;
font-family: Tahoma, Verdana, Arial, sans-serif; }
</style>
</head>
<body>
<h1>Welcome to nginx!</h1>
<p>If you see this page, the nginx web server is successfully installed and
working. Further configuration is required.</p>

<p>For online documentation and support please refer to
<a href="http://nginx.org/">nginx.org</a>.<br/>
Commercial support is available at
<a href="http://nginx.com/">nginx.com</a>.</p>

<p><em>Thank you for using nginx.</em></p>
</body>
</html>
amitabh@LAPTOP-3KF17VR3:/mnt/c/Users/USER/Downloads/devops-heros-branch10104-main/devops-heros-branch10104-main/session-12-ingress-configmaps-secrets/04-full-demo$ curl -H "Host: yatri.local" http://127.0.0.1:8080/api/
Yatri Backend API
=================
ENVIRONMENT     : production
LOG_LEVEL       : INFO
DEFAULT_CURRENCY: INR
POSTGRES_USER   : yatri_admin
POSTGRES_DB     : yatri_production_db
amitabh@LAPTOP-3KF17VR3:/mnt/c/Users/USER/Downloads/devops-heros-branch10104-main/devops-heros-branch10104-main/session-12-ingress-configmaps-secrets/04-full-demo$ kubectl get pods
NAME                             READY   STATUS    RESTARTS   AGE
yatri-backend-6c58cb99c7-6dldg   1/1     Running   0          6m30s
yatri-backend-6c58cb99c7-gjlv9   1/1     Running   0          6m30s
yatri-frontend-ddcfc4b5f-p6cwz   1/1     Running   0          6m30s
yatri-frontend-ddcfc4b5f-vmvwr   1/1     Running   0          6m30s
amitabh@LAPTOP-3KF17VR3:/mnt/c/Users/USER/Downloads/devops-heros-branch10104-main/devops-heros-branch10104-main/session-12-ingress-configmaps-secrets/04-full-demo$ kubectl get svc
NAME                     TYPE        CLUSTER-IP       EXTERNAL-IP   PORT(S)   AGE
kubernetes               ClusterIP   10.96.0.1        <none>        443/TCP   3h19m
yatri-backend-service    ClusterIP   10.98.12.236     <none>        80/TCP    6m39s
yatri-frontend-service   ClusterIP   10.108.167.179   <none>        80/TCP    6m39s
amitabh@LAPTOP-3KF17VR3:/mnt/c/Users/USER/Downloads/devops-heros-branch10104-main/devops-heros-branch10104-main/session-12-ingress-configmaps-secrets/04-full-demo$ kubectl get ingress
NAME            CLASS   HOSTS         ADDRESS        PORTS   AGE
yatri-ingress   nginx   yatri.local   192.168.49.2   80      6m46s
amitabh@LAPTOP-3KF17VR3:/mnt/c/Users/USER/Downloads/devops-heros-branch10104-main/devops-heros-branch10104-main/session-12-ingress-configmaps-secrets/04-full-demo$ kubectl get ingress yatri-ingress -o wide
NAME            CLASS   HOSTS         ADDRESS        PORTS   AGE
yatri-ingress   nginx   yatri.local   192.168.49.2   80      6m53s
amitabh@LAPTOP-3KF17VR3:/mnt/c/Users/USER/Downloads/devops-heros-branch10104-main/devops-heros-branch10104-main/session-12-ingress-configmaps-secrets/04-full-demo$ kubectl exec -it deploy/yatri-backend -- env | grep -E 'ENVIRONMENT|LOG_LEVEL|POSTGRES'
POSTGRES_USER=yatri_admin
POSTGRES_PASSWORD=secretpassword
POSTGRES_DB=yatri_production_db
ENVIRONMENT=production
LOG_LEVEL=INFO
amitabh@LAPTOP-3KF17VR3:/mnt/c/Users/USER/Downloads/devops-heros-branch10104-main/devops-heros-branch10104-main/session-12-ingress-configmaps-secrets/04-full-demo$ kubectl get secret yatri-db-secret -o jsonpath='{.data.POSTGRES_PASSWORD}' | base64 --decode
secretpasswordamitabh@LAPTOP-3KF17VR3:/mnt/c/Users/USER/Downloads/devops-heros-branch10104-main/devops-heros-branch10104-main/session-12-ingress-configmaps-secrets/kubectl describe ingress yatri-ingress yatri-ingress
Name:             yatri-ingress
Labels:           app=yatri-app
Namespace:        default
Address:          192.168.49.2
Ingress Class:    nginx
Default backend:  <default>
Rules:
  Host         Path  Backends
  ----         ----  --------
  yatri.local  
               /api(/|$)(.*)   yatri-backend-service:80 (10.244.0.12:5000,10.244.0.11:5000)
               /               yatri-frontend-service:80 (10.244.0.10:80,10.244.0.9:80)
Annotations:   nginx.ingress.kubernetes.io/rewrite-target: /$2
               nginx.ingress.kubernetes.io/ssl-redirect: false
               nginx.ingress.kubernetes.io/use-regex: true
Events:
  Type    Reason  Age                   From                      Message
  ----    ------  ----                  ----                      -------
  Normal  Sync    7m2s (x2 over 7m54s)  nginx-ingress-controller  Scheduled for sync