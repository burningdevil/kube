# command

## Environment

VRA: centos 7

```bash

# change passwd
passwd

# make admin's home folder if not exist
cd /home/
sudo mkdir admin
sudo chown $(id -u):$(id -g) admin
cd admin/

# install docker
sudo yum install -y yum-utils
sudo yum-config-manager --add-repo  https://download.docker.com/linux/centos/docker-ce.repo
sudo yum install docker-ce docker-ce-cli containerd.io docker-compose-plugin
sudo systemctl enable docker --now
# test docker installed
sudo docker run hello-world

# disable firewall
sudo vi /etc/selinux/config
# change to 'SELINUX=disabled'
systemctl stop firewalld.service

# disable swap
sudo swapoff -a
sudo sed -i '/swap/d' /etc/fstab

# change bridge
sudo vi /etc/sysctl.d/k8s.conf
# input below content:
net.bridge.bridge-nf-call-ip6tables = 1
net.bridge.bridge-nf-call-iptables = 1
net.ipv4.ip_forward = 1
# reboot
sudo reboot

# install kube*
cat <<EOF | sudo tee /etc/yum.repos.d/kubernetes.repo
[kubernetes]
name=Kubernetes
baseurl=https://packages.cloud.google.com/yum/repos/kubernetes-el7-\$basearch
enabled=1
gpgkey=https://packages.cloud.google.com/yum/doc/yum-key.gpg https://packages.cloud.google.com/yum/doc/rpm-package-key.gpg
exclude=kubelet kubeadm kubectl
EOF

sudo setenforce 0
sudo sed -i 's/^SELINUX=enforcing$/SELINUX=permissive/' /etc/selinux/config
sudo yum install -y kubelet kubeadm kubectl --disableexcludes=kubernetes

# start kubelet
sudo systemctl enable --now kubelet


# reconfig docker
sudo rm /etc/containerd/config.toml
sudo systemctl restart docker
sudo systemctl restart containerd



# for master

# init kubeadm
sudo kubeadm reset
sudo kubeadm init --pod-network-cidr=192.168.0.0/16

# copy config
mkdir -p $HOME/.kube
sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
sudo chown $(id -u):$(id -g) $HOME/.kube/config

# install calico, from: https://projectcalico.docs.tigera.io/getting-started/kubernetes/quickstart
kubectl create -f https://projectcalico.docs.tigera.io/manifests/tigera-operator.yaml
kubectl create -f https://projectcalico.docs.tigera.io/manifests/custom-resources.yaml

kubectl taint nodes --all node-role.kubernetes.io/master-
kubectl get nodes -o wide

## ready to connect
sudo kubeadm token create --print-join-command
# result
# kubeadm join 10.23.39.152:6443 --token g3jo4i.6qldbixdmcjr8h58 --discovery-token-ca-cert-hash sha256:423684b67d5824df452bb4f1c43e384d78a941e3c023e1174b11f34c077e7776

# for slave
# join cluster
kubeadm join 10.23.39.152:6443 --token g3jo4i.6qldbixdmcjr8h58 --discovery-token-ca-cert-hash sha256:423684b67d5824df452bb4f1c43e384d78a941e3c023e1174b11f34c077e7776
# copy to slave and execute
mkdir -p $HOME/.kube
sudo scp admin@$(master_node_ip):/home/admin/.kube/config $HOME/.kube/config
sudo chown -R $(id -u):$(id -g) $HOME/.kube
# now you can use
kubectl get nodes
```

# command to join

``` bash
sudo kubeadm token create --print-join-command
```

sudo kubeadm join 10.23.39.152:6443 --token 6t4ene.z43l5brqkpqbnt1i --discovery-token-ca-cert-hash sha256:423684b67d5824df452bb4f1c43e384d78a941e3c023e1174b11f34c077e7776

# commnad to delete 

on master node:

``` bash
kubectl cordon $node_name
kubectl drain $node_name --ignore-daemonsets
kubectl delete node $node_name
```

# command to connect another master

rm -rf $HOME/.kube
sudo rm -rf /etc/kubernetes/pki/
sudo kubeadm reset

# Other tools

## Bash auto completion tool

https://kubernetes.io/docs/tasks/tools/included/optional-kubectl-configs-bash-linux/
