# Pods

- Containers are encapsulated in kubernetes object called Pod
- It is the smalled object you can create in k8s


## Commands

Run an image
```bash
kubectl run <pod_name> --image=<image_location>
```
```bash
kubectl run nginx --image=nginx
```

List pods
```bash
kubectl get pods
kubectl get po
kubectl get pods -o wide    # Get more info
```

Get more details of pod
```bash
kubectl describe pod nginx
```

Delete Pod
```bash
kubectl delete pod nginx
```

