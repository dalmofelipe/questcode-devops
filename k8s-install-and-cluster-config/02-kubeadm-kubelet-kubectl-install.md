# kubeadm kubelet kubectl install

```bash
sudo su
swapoff -a
curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | apt-key add -
cat <<EOF >/etc/apt/sources.list.d/kubernetes.list
deb https://apt.kubernetes.io/ kubernetes-xenial main
EOF
apt-get update
apt-get install -y kubelet=1.11.3-00 kubeadm=1.11.3-00 kubectl=1.11.3-00
apt-get install -y kubelet kubeadm kubectl
apt-mark hold kubelet kubeadm kubectl
exit
```

apt-mark hold - trava a versao do k8s impedindo atualizações

