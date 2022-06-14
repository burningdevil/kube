# Ingress

An Ingress Controller is a daemon running in a Pod which watches the /ingresses endpoint on the API server, which is found under the networking.k8s.io/v1beta1 group for new objects. When a new endpoint is created, the daemon uses the configured set of rules to allow inbound connection to a service, most often HTTP traffic. This allows easy access to a service through an edge router to Pods, regardless of where the Pod is deployed.

Multiple Ingress Controllers can be deployed. Traffic should use **annotations** to select the proper controller. The lack of a matching annotation will cause every controller to attempt to satisfy the ingress traffic.

## yaml

```yaml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  annotations:
    kubernetes.io/ingress.class: nginx
  generation: 1
  name: ingress-test
  namespace: default
  resourceVersion: "1188752"
spec:
  rules:
  - host: www.external.com
    http:
      paths:
      - backend:
          service:
            name: web-one
            port:
              number: 80
        path: /
        pathType: ImplementationSpecific
```

## commands

```bash
kubectl get ingress
kubectl delete ingress name
kubectl edit ingress name
```

```bash
kubectl run ghost --image=ghost
```
