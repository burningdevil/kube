# label

## label command

```bash
# show label
kubectl get nodes --show-labels
# show resources with label
kubectl get resoutce_type -l key=value
# set label
kubectl label nodes <your-node-name> disktype=ssd
```

## node selector

```bash
apiVersion: v1
kind: Pod
metadata:
  name: nginx
  labels:
    env: test
spec:
  containers:
  - name: nginx
    image: nginx
    imagePullPolicy: IfNotPresent
  nodeSelector:
    disktype: ssd
```
