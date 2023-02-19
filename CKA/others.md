jq
tmux

`
kubectl exec nginx-1423793266-13p69 -- printenv
`

# copy

`
kubectl cp file_in_node target_node:/path/path
`

`
kubectl exec -ti pod_name -c container_name -- commands
`

`
kubectl top pod -A --sort-by=cpu
`

```bash
# get cidr, grep controller-manager process 
ps -aux  | grep -i cidr
```

systemd location: (service/process has it)
/etc/systemd/system

By default the kubelet looks into /etc/cni/net.d to discover the CNI plugins. This will be the same on every master and worker nodes.

systemctl restart kubelet
systemctl status kubelet
journalctl -u kubelet
vim /etc/systemd/system/kubelet.service.d/10-kubeadm.conf
