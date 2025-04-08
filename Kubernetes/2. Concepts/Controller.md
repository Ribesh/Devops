# Controller

- Brain of Kubernetes

## Replication Controller 
```bash
apiVersion: v1
kind: ReplicationController
metadata:
    name: myapp-rc
    labels:
        app: myapp
        type: front-end
spec:
    template:
        metadata:
            name: myapp-pod
            labels:
                app: myapp
                type: frontend
        spec:
            containers:
                -   name: nginx-contaienr
                    image: nginx
    replicas: 3
```

```bash
kubectl create -f rc-definition.yml
```
List Replication Controller
```bash
kubectl get replicationcontrollers
kubectl get rc
```


##  Replication Set
Only slight difference betweeen Replication Controller and Replication Set

```bash
    selector:
        matchLabels:
            type: front-end
```
```

```bash
apiVersion: apps/v1
kind: ReplicaSet
metadata:
    name: myapp-replicaset
    labels:
        app: myapp
        type: front-end
spec:
    template:
        metadata:
            name: myapp-pod
            labels:
                app: myapp
                type: front-end
        spec:
            containers:
                -   name: nginx-container
                    image: nginx
    replicas: 3
    selector:
        matchLabels:
            type: front-end
```

## Scale

```bash
kubectl scale --replicas=6 -f replication-definition.yml
```

```bash
kubectl scale --replicas=6 replicaset myapp-replicaset
```

If changing the ```replicas:6``` in the ```yaml``` file use below command:
```bash
kubectl replace -f replicaset-definition.yml
```

Other Commands:

Create Replica Set
```bash
kubectl create -f <........yml>
```

List the Replica Set
```bash
kubectl get replicaset
kubectl get rs
```

Delete the Replica Set
```bash
kubectl delete replicaset myapp-replicaset      # Also deletes all underlying pods
kubectl delete rs myapp-replicaset
```

Replace/Update
```bash
kubectl replace -f <...yml>
```

Describe
```bash
kubectl describe replicaset myapp-replicaset
kubectl describe rs myapp-replicaset
```

Edit in Runtime
```bash
kubectl edit replicaset myapp-replicaset
kubectl edit rs myapp-replicaset
```
After editing, for the changes to reflect
1. Either Delete all the pods
```bash
kubectl delete pods <pod_1> <pod_2> <pod_3> .....
kubectl delete po <pod_1> <pod_2>
```

2. Or, Update the existing Replicaset
3. Or, Delete and recreate the Replicaset