# Deployment

## create

```bash
kubectl create deploy nginx --image=nginx
kubectl get deploy

# output current to yaml
kubectl get deploy nginx -o yaml
# create a template
kubectl create deployment nginx --image=nginx --dry-run=client -o yaml

# expose
kubectl expose deploy nginx --port
```

## update

```bash
kubectl set image deplpyment/name name=url --all

kubectl rollout history deploy name
kubectl rollout history deploy name --revision=1

kubectl rollout undo deploy name
kubectl rollout undo deploy name --to-revision=2
```

## ReplicaSets

### delete

```bash
kubectl delete rs name --cascade=orphan
```
