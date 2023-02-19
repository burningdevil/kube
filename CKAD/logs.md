# logs

## log locations

/var/log/containers

list of files

```bash
kube-controller-manager-tec-l-1073877_kube-system_kube-controller-manager-db1f744473263445c84aee2a83819b2888c0789473336f2d5e0b642f136b1c5a.log
kube-proxy-8ctnp_kube-system_kube-proxy-97ab577f3aedf84d5c3bfd7edf52f084922d1aa0b3386af06ed3cc00e5c542c4.log
kube-scheduler-tec-l-1073877_kube-system_kube-scheduler-98843568fbc2a82bcbaa0edfaa502267c0fe4a31fef1250fe5d059ab87737c08.log
kube-scheduler-tec-l-1073877_kube-system_kube-scheduler-a25a726777903f10f75693f09e104093e1f531af70363caa9f93af140d7c421a.log
```

/var/log/pods

```bash
alico-apiserver_calico-apiserver-67f5fc4bf5-dzjqh_0f67654f-1962-4f04-af52-717d54dfd151
calico-apiserver_calico-apiserver-67f5fc4bf5-kx6rx_f6b7b05d-2659-4f75-99b6-9f240add559a
kube-system_coredns-6d4b75cb6d-h5xwf_fee1feef-dc82-4216-a128-45859aed2eea
kube-system_coredns-6d4b75cb6d-rz8h7_d644c8e6-aa9c-469d-bf36-5016706dabb3
kube-system_etcd-tec-l-1073877_b2e125d16c67e392dad2bc183a104ec0
kube-system_kube-apiserver-tec-l-1073877_f8850031dd1dee57ec456b12bb20a48a
kube-system_kube-controller-manager-tec-l-1073877_8f36255a76704c2b47378bb04c832742
kube-system_kube-proxy-8ctnp_159d43f0-7930-47ed-8294-9723836d7e79
kube-system_kube-scheduler-tec-l-1073877_7a7a6db2fb03f20b5e24de8fbcfa689c
kube-system_metrics-server-df6668697-k885x_8ac1a123-6898-4de5-a474-c22b0142ad69
```

iptables-save | grep hostnames