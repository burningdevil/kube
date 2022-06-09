# kube

## container runtime

crio, docker, containerd

## kubeadm

`sudo kubeadm init`

init control plane

`kubeadm join <ip> --token <token>`

worker node join kube

## kubectl

```kube
kubectl api-resources
kubectl cluster-info
kubectl get nodes/pods/svc(services)/deploy(deplpyments)/rs(replicaset)
kubectl explain resourcetype.subtype
kubectl describe resourcetype/name
kubectl logs <some containers>
# view configs
kubectl config view
# run a single pod
kubectl run nginx --image=nginx:1.20
kubectl exec <command in container> 
kubectl exec -ti $POD_NAME -- curl localhost:8080
kubectl expose <deployment> --type --port 
kubectl label pods $POD_NAME version=v1
kubectl delete service -l app=999
kubectl get services -l app=kubernetes-bootcamp
kubectl scale --replicas=3 rs/foo
kubectl --help
kubectl create -f <file>.yaml
```

### create

`kubectl create deployment <name> --image=<name>`  
`kubectl expose deployment <name> --type=NodePort --port=8080`  
create a deployment and expose it as NodePort in port 8080.

`minikube tunnel`  
Should run on a seperate terminal.  
minikube tunnel runs as a process, creating a network route on the host to the service CIDR of the cluster using the cluster’s IP address as a gateway. The tunnel command exposes the external IP directly to any program running on the host operating system.

### get pods

`kubectl get pods`

### label and selector all all key-values

`-l key=value`

used for combination with label.

### run command in pods(containers)

`kubectl exec <pod name> -- env`  
get environment variables

`kubectl exec -ti <pod name> -- bash`  
start bash in target pod

### service

A Service in Kubernetes is an abstraction which defines a logical set of Pods and a policy by which to access them.
service: one or muliple pods expose together

type:

- cluster
- node-port
- load banlancer
- external name

`kubectl expose pod/rs/deploy <name> --type Cluster/NodePort/LoadBalancer --port <port>`  
expose resource to external

`kubectl get svc/services`  
view all services external ip

### Scaling an application

In the previous modules we created a Deployment, and then exposed it publicly via a Service. The Deployment created only one Pod for running our application. When traffic increases, we will need to scale the application to keep up with user demand.
Scaling is accomplished by changing the number of replicas in a Deployment

```kube
$ kubectl get rs
NAME                            DESIRED   CURRENT   READY   AGE
kubernetes-bootcamp-fb5c67579   1         1         1       96s

$ kubectl scale deployments/kubernetes-bootcamp --replicas=4
deployment.apps/kubernetes-bootcamp scaled
```

```kube
$ kubectl get deployments
NAME                  READY   UP-TO-DATE   AVAILABLE   AGE
kubernetes-bootcamp   4/4     4            4           3m40s
$ kubectl get rs
NAME                            DESIRED   CURRENT   READY   AGE
kubernetes-bootcamp-fb5c67579   4         4         4       3m30s
$ kubectl get pods -o wide
NAME                                  READY   STATUS    RESTARTS   AGE     IP           NODE       NOMINATED NODE   READINESS GATES
kubernetes-bootcamp-fb5c67579-gv9lp   1/1     Running   0          3m51s   172.18.0.5   minikube   <none>           <none>
kubernetes-bootcamp-fb5c67579-lcwxs   1/1     Running   0          45s     172.18.0.7   minikube   <none>           <none>
kubernetes-bootcamp-fb5c67579-mcgm9   1/1     Running   0          45s     172.18.0.8   minikube   <none>           <none>
kubernetes-bootcamp-fb5c67579-tlfgj   1/1     Running   0          45s     172.18.0.9   minikube   <none>           <none>
$ 
```

### update and revert

```kube
kubectl set image deployments/<deploy name> <image name>=jocatalin/kubernetes-bootcamp:v2

# You can also confirm the update by running the rollout status command:
kubectl rollout status deployments/kubernetes-bootcamp

kubectl set image deployments/kubernetes-bootcamp kubernetes-bootcamp=gcr.io/google-samples/kubernetes-bootcamp:v10
kubectl rollout undo deployments/kubernetes-bootcamp
```

## pod network

calico

## example of yaml configuration

pod -> rs -> deployment

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment
spec: 
  selector:
    matchLabels:
      app: nginx
  replicas: 2 # tells deployment to run 2 pods matching the template
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx
        image: nginx:1.19
        ports:
        - containerPort: 80
```

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment
spec: 
  selector:
    matchLabels:
      app: nginx
  replicas: 2 # tells deployment to run 2 pods matching the template
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx
        image: nginx:1.19
        ports:
        - containerPort: 80
```

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: test-pd
spec:
  containers:
  - image: k8s.gcr.io/test-webserver
    name: test-container
    volumeMounts:
    - mountPath: /test-pd
      name: test-volume
  volumes:
  - name: test-volume
    hostPath:
      # directory location on host
      path: /data
      # this field is optional
      type: Directory
```

```yaml
apiVersion: v1
kind: PersistentVolume
metadata:
  name: test-pv
spec:
  capacity:
    storage: 50Gi
  volumeMode: Filesystem
  accessModes:
    - ReadWriteOnce
  csi:
    driver: ebs.csi.aws.com
    volumeHandle: vol-05786ec9ec9526b67
---
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: ebs-claim
spec:
  accessModes:
    - ReadWriteOnce
  resources:
    requests:
      storage: 50Gi
---
apiVersion: v1
kind: Pod
metadata:
  name: app
spec:
  containers:
    - name: app
      image: centos
      command: ["/bin/sh"]
      args:
        ["-c", "while true; do echo $(date -u) >> /data/out.txt; sleep 5; done"]
      volumeMounts:
        - name: persistent-storage
          mountPath: /data
  volumes:
    - name: persistent-storage
      persistentVolumeClaim:
        claimName: ebs-claim
```

```yaml
apiVersion: v1
kind: ConfigMap
metadata:
  name: nginx-conf
data:
  nginx.conf: |
    user nginx;
    worker_processes 3;
    error_log /var/log/nginx/error.log;
...
      server {
          listen     80;
          server_name _;
          location / {
              root   html;
              index  index.html index.htm; } } }
```
