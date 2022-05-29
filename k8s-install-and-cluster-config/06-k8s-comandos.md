### LISTA DE COMANDOS K8S

```bash

# Aplica um arquivo de configuração ao server
kubectl apply -f <filename> 

# Lista todos recursos em todos namespaces
kubectl get all --all-namespaces 

# para editar enquanto esta em execução
kubectl edit svc <service_name> -n <namespace>


kubectl logs pod/backend-scm-78c94d4d76-r87h6 -n staging

kubectl describe pod/backend-scm-78c94d4d76-r87h6 -n staging

```


### VSCODE DISABLE LINT K8S

then edit VS Code setting.json to look like this:

```json
{
    "vs-kubernetes": {
        "disable-linters": ["resource-limits"]
    }
}
```


### Desligando K8S [WIP]

```bash

kubectl scale deploy <deploy-name> -n <namespace> --replicas=0

kubectl scale deploy -n <namespace> --replicas=0 --all 

kubectl get deploy -n <namespace> -o name | xargs -I % kubectl scale % --replicas=0 -n <namespace>

kubectl scale statefulset,deployment -n mynamespace --all --replicas=0

k scale deploy -n staging --all --replicas=0

sudo systemctl stop docker.service docker.socket kubelet.service

ps aux | grep kube  

sudo kill -9 <PID-PROCESSO> 

kube-apiserver
kube-proxy
etcd
flanneld

```



> We have had hard DC crashes and when bringing things back up, we just made sure the control plane was up before our nodes and things have come back fine.

> We have also powered off our cluster(s) before and for the most part did this:

> 1. Scale all applications down to 0 excluding cluster services e.g. CNI DaemonSets, DNS etc.
> 2. Drain all nodes excluding the control plane.
> 3. Shut down nodes.
> 4. Shut down all components but kube-apiserver and etcd. – If using kubelet to manage components (kubeadm), just move the manifests out of the /etc/kubernetes/manifests dir and kubelet will stop the containers gracefully.
> 5. shut down kube-apiserver
> 6. Stop kubelet on control plane, just ensure the etcd leader is the last one to be stopped.
> 7. Backup dirs/etcd if needed.
> 8. Bringing it backup is essentially the opposite order.
