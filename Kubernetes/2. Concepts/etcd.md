# Etcd 

- It is a distributed reliable key-value store that is Simple, Secure & Fast

## ETCD in K8s
 - Stores information about
    -   Nodes
    -   PODs
    -   Configs
    -   Secrets
    -   Accounts
    -   Roles
    -   Bindings
    -   Others

- Every info you see, when you run ```kubectl get``` commad is from etcd server

- Any changes you make to the cluster — whether adding nodes, deploying pods, or configuring ReplicaSets — are first recorded in etcd

- Only after etcd is updated are these changes considered to be complete.


Setup - kubeadm

```bash
kubectl get pods -n kube-system
```

```bash
kubectl exec etcd-master -n kybe-system etcdctl get / --prefix -keys-only
```