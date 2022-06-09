# Update

## DaemonSet update strategy

1. OnDelete  
after you update a DaemonSet template, new DaemonSet pods will only be created when you manually delete old DaemonSet pods.
2. RollingUpdate  
after you update a DaemonSet template, old DaemonSet pods will be killed, and new DaemonSet pods will be created automatically, in a controlled fashion.  

* pdateStrategy.rollingUpdate.maxSurge  
The maximum number of nodes with an existing available DaemonSet pod that can have an updated DaemonSet pod during during an update.
* updateStrategy.rollingUpdate.maxUnavailable  
The maximum number of DaemonSet pods that can be unavailable during the update.


```bash
kubectl set image ds ds-name container-name=image-url
```

