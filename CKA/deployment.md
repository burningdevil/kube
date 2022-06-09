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

