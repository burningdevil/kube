# Softwares

## CNCF projects

- Containerd  
container runtime
- CoreDNS, etcd  
Coordination & Service Discovery
- envoy  
Service Proxy
- fluentd  
logging
- HARBOR  
container registry
- HELM  
Application Definition & Image build
- JAEGER  
Tracing
- Kubernetes  
Scheduling & Orchestration
- LINKERD  
Service Mesh
- Open Policy Agent， TUF
Security & Compliance
- Promethus  
Monitoring
- Rook  
Clould Native Storage
- TIKV, Vitess  
Database

## Containers

### building images

buildah or kaniko

### full alternatives to docker

podman, docker

## docker Registry

Docker Hub(docker) and Quay(podman)

## Service discovery

### Key-Value-Store

Using datastore to store information about services. It's a service registry indeed.  

- etcd
- Consul
- Apache Zookeeper

## Service Mesh

### proxy

second container in application. The software that you use to manage network traffic is called a proxy. Sit between client and server and can modify or filter network traffic.

- nginx
- haproxy
- envoy

### service mesh

a service mesh adds a proxy server to every container that you have in your architecture. When a service mesh is used, applications don’t talk to each other directly, but the traffic is routed through the proxies instead.

- istio
- linkered

## Kube clusters

### setting up test cluster

- minikube
- kind
- microk8s

### production-grade cluster

- kubeadm
- kops
- kubespray

### venders packing kube into distribution

- rancher
- k3s
- openshift(red hat)
- vmware tanzu

### Cloud provier

- Amazon(EKS)
- Google(GKE)
- Microsoft(AKS)
- DigitalOcean(DOKS)

## KubeAPI Aceess Control

### Authentication

Service Accounts

### Authorization

Role Based Access Control

### Admission Control

Open Policy Agent

## ContainerD (container runtime)

replacement of ContainerD/CRI-O

- gvisor  
google, runsc, security

- kata containers  
secure, virtual machine, behaves as container

## Network

To implement networking, you can choose from a variety of network vendors like:

- Project Calico
- Weave
- Cilium

## Working with Kubernetes

Other tools for interacting with Kubernetes:

- Kubernetes/dashboard
- derailed/k9s
- Lens
- VMware Tanzu Octant

creation of templates and the packaging of Kubernetes objects. Helm is a package manager for Kubernetes, which allows easier updates and interaction with objects.

- Helm

## Storage

### cloud block storage

- Amazon EBS
- Google Persistent Disks
- Azure Disk Storage

### consume from storage systems

- Ceph
- GlusterFS
- traditional system NFS

### Operate storgae in kube

- Rook

## Autoscaling

### horizontal scale

Based on metrics addon

- metrics server

Events Driven

- KEDA

## CI/CD Tools

- Spinnaker
- GitLab
- Jenkins
- Jenkins X
- Token CD
- Argo

## GitOPs

GitOps takes the idea of Git as the single source of truth a step further and integrates the provisioning and change process of infrastructure with version control operations.

GitOps framework use pull-based approach.

- Flux(built with GitOPs toolkit)
- ArgoCD(kubernetes controller)

## Logs

### ship and store Logs

fluentd and filebeat

### store logs

OpenSearch or Granfana Loki

## Metrics

- Granfana: most used companion for Prometheus, build dashboards from collected metrics.
- Alertmanager: alertmanager can send a notification to email, chat tool when a alert from Prometheus fires.

## Tracing

### store and analyzed

Jaeger

## gPRC

gRPC is a modern open source high performance Remote Procedure Call (RPC) framework that can run in any environment.
