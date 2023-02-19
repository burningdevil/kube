# Debug

## network

```bash
# run temp pod
kubectl run name --restart=Never --rm -ti --image=alpine -- sh
# test 
wget --spider  $svc_name

wget -O- $svc_name:port
```

```bash
# test repo
curl http://$registry_ip:5000/v2/_catalog
```
