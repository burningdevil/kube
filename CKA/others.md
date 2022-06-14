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