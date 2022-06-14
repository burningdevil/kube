# Schedule

## Pod Specification

- Node name and nodeSelector  
The nodeName and nodeSelector options allow a Pod to be assigned to a single node or a group of nodes with particular labels.
- affinity and anti-affinity  
Affinity and anti-affinity can be used to require or prefer which node is used by the scheduler. If using a preference instead, a matching node is chosen first, but other nodes would be used if no match is present.
- taints and tolerations  
The use of taints allows a node to be labeled such that Pods would not be scheduled for some reason, such as the cp node after initialization. A toleration allows a Pod to ignore the taint and be scheduled assuming other requirements are met.
- schedulerName  
Should none of the options above meet the needs of the cluster, there is also the ability to deploy a custom scheduler. Each Pod could then include a schedulerName to choose which schedule to use.

## Label Selector

```yaml
spec:
  containers:
  - name: redis
    image: redis
  nodeSelector:
    net: fast
```

## Pod Affinity Rules

Pods which may communicate a lot or share data may operate best if co-located, which would be a form of affinity. For greater fault tolerance, you may want Pods to be as separate as possible, which would be anti-affinity. These settings are used by the scheduler based on the labels of Pods that are already running. As a result, the scheduler must interrogate each node and track the labels of running Pods. Clusters larger than several hundred nodes may see significant performance loss. Pod affinity rules use In, NotIn, Exists, and DoesNotExist operators.

- requiredDuringSchedulingIgnoredDuringExecution  
The use of requiredDuringSchedulingIgnoredDuringExecution means that the Pod will not be scheduled on a node unless the following operator is true. If the operator changes to become false in the future, the Pod will continue to run. This could be seen as a hard rule.
- preferredDuringSchedulingIgnoredDuringExecution  
Similarly, preferredDuringSchedulingIgnoredDuringExecution will choose a node with the desired setting before those without. If no properly-labeled nodes are available, the Pod will execute anyway. This is more of a soft setting, which declares a preference instead of a requirement.
- podAffinity  
With the use of podAffinity, the scheduler will try to schedule Pods together.
- podAntiAffinity  
The use of podAntiAffinity would cause the scheduler to keep Pods on different nodes.

## Taints

A node with a particular taint will repel Pods without tolerations for that taint. A taint is expressed as **key=value:effect**. The key and the value are created by the administrator.

The key and value used can be any legal string, and this allows flexibility to prevent Pods from running on nodes based off of any need. If a Pod does not have an existing toleration, the scheduler will not consider the tainted node.

- NoSchedule  
The scheduler will not schedule a Pod on this node, unless the Pod has this toleration. Existing Pods continue to run, regardless of toleration.
- PreferNoSchedule  
The scheduler will avoid using this node, unless there are no untainted nodes for the Pods toleration. Existing Pods are unaffected.
- NoExecute  
This taint will cause existing Pods to be evacuated and no future Pods scheduled. Should an existing Pod have a toleration, it will continue to run. If the Pod tolerationSeconds is set, they will remain for that many seconds, then be evicted. Certain node issues will cause the kubelet to add 300 second tolerations to avoid unnecessary evictions.

## Tolerations

Setting tolerations on a node are used to schedule Pods on tainted nodes. This provides an easy way to avoid Pods using the node. Only those with a particular toleration would be scheduled.

An operator can be included in a Pod specification, defaulting to Equal if not declared. The use of the operator Equal requires a value to match. The Exists operator should not be specified. If an empty key uses the Exists operator, it will tolerate every taint. If there is no effect, but a key and operator are declared, all effects are matched with the declared key.

```yaml
tolerations:
- key: "server"
  operator: "Equal"
  value: "ap-east"
  effect: "NoExecute"
  tolerationSeconds: 3600
```

```bash
# taint
kubectl taint node node_name key=value:NoSchedule

# untaint
kubectl taint node node_name key-
```

You can view the scheduler and other information with this command:

`
kubectl get events
`
