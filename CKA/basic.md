# Basical Operations

## Backup etcd DB

``` bash
# find repo of etcd 
sudo grep data-dir /etc/kubernetes/manifests/etcd.yaml

# log into etcd container
kubectl -n kube-system exec -ti podname -- sh

# following command is inside container sh
# show all files in this dir, equal to ls in bash
echo *

```

## upgrade cluster

bmk: https://kubernetes.io/docs/tasks/administer-cluster/kubeadm/kubeadm-upgrade/


```bash
# update package metadata
sudo apt/yum update

# view available packages
```

```bash
# with label filter
k get pods -n project-snake -L app
```

## use jq in vim

`
%!jq .
`

or 

`
%!python3 -m json.tool
`

 k -n project-snake exec backend-0 -- curl -s 10.44.0.25:1111

 sudo kubeadm config print init-defaults