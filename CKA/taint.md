# Taint and Affinity

## node selector

nodeSelector is the simplest way to constrain Pods to nodes with specific labels.

## Affinity

Affinity and anti-affinity expands the types of constraints you can define.

The affinity feature consists of two types of affinity:

1. Node affinity functions like the nodeSelector field but is more expressive and allows you to specify soft rules.
2. Inter-pod affinity/anti-affinity allows you to constrain Pods against labels on other Pods.  

Inter-pod affinity and anti-affinity rules take the form "this Pod should (or, in the case of anti-affinity, should not) run in an X if that X is already running one or more Pods that meet rule Y", where X is a topology domain like node, rack, cloud provider zone or region, or similar and Y is the rule Kubernetes tries to satisfy.

## Taint

Node affinity is a property of Pods that attracts them to a set of nodes (either as a preference or a hard requirement).  
**Taints** are the opposite -- they allow a node to repel a set of pods.  
**Tolerations** are applied to pods, and allow (but do not require) the pods to schedule onto nodes with matching taints.  

### command

node.spec.taints

``` bash
# format
kubectl taint nodes node_name key=value:effect
# effect is one of NoSchedule, PreferNoSchedule, NoExecute
# Can only apply to nodes

# add taint
kubectl taint nodes node1 key1=value:NoSchedule
kunectl taint nodes --all key=value:NoSchedule

# remote taint
kubectl taint nodes node1 key1=value:NoSchedule-
```

### yaml

spec.tolerations

```yaml
tolerations:
- key: "key1"
  operator: "Equal"
  value: "value1"
  effect: "NoSchedule"
```

or

```yaml
tolerations:
- key: "key1"
  operator: "Exists"
  effect: "NoSchedule"
```
