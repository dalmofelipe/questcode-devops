# CONFIGURANDO CLUSTER


## Init Cluster

```bash
sudo kubeadm init --pod-network-cidr=10.244.0.0/16
```


## Configurando Client (kubectl)

```bash
mkdir -p $HOME/.kube
sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
sudo chown $(id -u):$(id -g) $HOME/.kube/config
```


## Instalando Pod Network Addon (Flanel) e Master Isolation

```bash
# POD para gerenciamentos de rede interna do k8s
kubectl apply -f https://raw.githubusercontent.com/coreos/flannel/v0.10.0/Documentation/kube-flannel.yml
kubectl apply -f https://raw.githubusercontent.com/flannel-io/flannel/master/Documentation/kube-flannel.yml
```


```bash
# libera o master para agir como worker
kubectl taint nodes --all node-role.kubernetes.io/master-
```

```bash
# Note: The node-role.kubernetes.io/master taint is deprecated and kubeadm will stop using it in version 1.25. 
# https://kubernetes.io/docs/setup/production-environment/tools/kubeadm/create-cluster-kubeadm/
kubectl taint nodes --all node-role.kubernetes.io/control-plane- node-role.kubernetes.io/master-
```
