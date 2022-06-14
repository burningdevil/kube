# Log and Metrics

## Review log file

```bash
# view the node level logs forkubelet
jouranlctl -u kubelet | less

# get api server log location
sudo find / -name '*apiserver*log'
# result: /var/log/containers/*
```

## Monitoring and Metrics

```bash
kubectl -n kube-system logs pod_name
kubectl top nodes
```
