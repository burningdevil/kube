# Service

## Expose

```bash
# kubectl create svc nodeport --port=80

# create a service using existing deploy
kubectl expose deploy dptest --type=NodePort --name=svctest

kubectl expose deploy nginx --port=80 --type=NodePort

kubectl get svc
```

The kubectl expose command created a service for the nginx deployment. This service used port 80 and generated a random port on all the nodes.

## Types

- ClusterIP
- NodePort
- LoadBalancer
- ExternalName

``` bash
# create a local service to access ClusterIP
kubectl proxy

# get resource from API
curl localhost:8001/api/v1/namespaces/default/services/nginx
```

