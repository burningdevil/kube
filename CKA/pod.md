# Pod

## create pod

```bash
# dry run
kubectl run pod_name --image=nginx  --image-pull-policy=IfNotPresent --dry-run=client -o yaml
```

## init Containers

```yaml
initContainers:
	- image: 
	  name:
	  imagePullPolicy: Always
	  command:
	  SecurityContext:
	  	privileged: true
```

## static pods

Static Pods are managed directly by the kubelet daemon on a specific node, without the API server observing them. Unlike Pods that are managed by the control plane (for example, a Deployment); instead, the kubelet watches each static Pod (and restarts it if it fails).

Static Pods are always bound to one Kubelet on a specific node.

The kubelet automatically tries to create a mirror Pod on the Kubernetes API server for each static Pod. This means that the Pods running on a node are visible on the API server, but cannot be controlled from there. The Pod names will be suffixed with the node hostname with a leading hyphen.

```bash
# get config file
ps aux | grep kubelet

# 
sudo vi /var/lib/kubelet/config.yaml
# edit
staticPodPath: path

# restart
systemctl restart kubelet
```

## Cordon and drain node

``` bash
# make node unscheduleable
kubectl cordon node_name

# make it scheduleable
kubectl uncordon node_name

# delete a node
kubectl drain node_name --ignore-daemonsets --delte-emptydir-data
```

## Properties

`
--image-pull-policy
`

```bash
kubectl label node nodename key=value
kubectl label node nodename key-
kubectl label node --all key=value
```
