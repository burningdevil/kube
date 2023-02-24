# Common knowledge

- API server config file is `/etc/kubernetes/manifests/kube-apiserver.yaml` .
- System log in `/var/log/syslog`. Helpful when apiserver log is missing.
- API server log is in `/var/log/pods/kube-system_kube-apiserver-tec-l-1073877_6acae61dad06654958b855d5e6985854/kube-apiserver/0.log`.
- use `crictl ps -a; crictl logs` to check logs.
- `crictl ps` if not found, **ssh** to another node.
- check profile:  
    - ps -elf | grep name
    - systemctl status name
    - /etc/*.d/
- container share a same pid `docker run --name app2 --pid=container:app1 -d nginx:alpine sleep infinity`
- disable mounting of serviceAccount token: `automountServiceAccountToken: false` on both serviceaccount or pod spec.