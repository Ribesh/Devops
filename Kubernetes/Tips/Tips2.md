# Tips 2

While you would be working mostly the declarative way – using definition files, imperative commands can help in getting one-time tasks done quickly, as well as generate a definition template easily. This would help save a considerable amount of time during your exams.

Before we begin, familiarize yourself with the two options that can come in handy while working with the below commands:

```--dry-run``` By default as soon as the command is run, the resource will be created. If you simply want to test your command, use the ```--dry-run=client``` option. This will not create the resource; instead, it tells you whether the resource can be created and if your command is right.

```-o yaml``` This will output the resource definition in YAML format on the screen.

Use the above two in combination to generate a resource definition file quickly that you can then modify and create resources as required instead of creating the files from scratch.

## POD

### Create an NGINX Pod

```bash
kubectl run nginx --image=nginx
```

### Generate POD Manifest YAML file (-o yaml). Don’t create it(–dry-run)
```bash
kubectl run nginx --image=nginx --dry-run=client -o yaml
```

## Deployment

### Create a deployment
```bash
kubectl create deployment --image=nginx nginx
```

### Generate Deployment YAML file (-o yaml). Don’t create it(–dry-run)
```bash
kubectl create deployment --image=nginx nginx --dry-run=client -o yaml
```
### Generate Deployment with 4 Replicas
```bash
kubectl create deployment nginx --image=nginx --replicas=4
```
### You can also scale a deployment using the
```bash
kubectl scale
```
command.
```bash
kubectl scale deployment nginx--replicas=4
```

**Another way to do this is to save the YAML definition to a file and modify**
```bash
kubectl create deployment nginx --image=nginx --dry-run=client -o yaml > nginx-deployment.yaml
```

You can then update the YAML file with the replicas or any other field before creating the deployment.
## Service

### Create a Service named redis-service of type ClusterIP to expose pod redis on port 6379
```bash
kubectl expose pod redis --port=6379 --name redis-service --dry-run=client -o yaml
```

(This will automatically use the pod’s labels as selectors)

### Or
```bash
kubectl create service clusterip redis --tcp=6379:6379 --dry-run=client -o yaml 
```

(This will not use the pods labels as selectors, instead, it will assume selectors as app=redis.

**You cannot pass in selectors as an option.**

So, it does not work very well if your pod has a different label set. So, generate the file and modify the selectors before creating the service)

### Create a Service named nginx of type NodePort to expose pod nginx’s port 80 on port 30080 on the nodes:
```bash
kubectl expose pod nginx --type=NodePort --port=80 --name=nginx-service --dry-run=client -o yaml
```

(This will automatically use the pod’s labels as selectors, but you cannot specify the node port. You have to generate a definition file and then add the node port manually before creating the service with the pod.)

### Or
```bash
kubectl create service nodeport nginx --tcp=80:80 --node-port=30080 --dry-run=client -o yaml
```

(This will not use the pod labels as selectors.)

Both the above commands have their own challenges. While one of them cannot accept a selector, the other cannot accept a node port. I would recommend going with the

```bash
kubectl expose
```
command. If you need to specify a node port, generate a definition file using the same command and manually input the nodeport before creating the service.
Reference:

https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands

https://kubernetes.io/docs/reference/kubectl/conventions/

## Create Pod with Service (ClusterIP)
```bash
kubectl run httpd --image=httpd:alpine --port=80 --expose

kubectl run httpd --image=httpd:alpine --port=80 --expose --dry-run=client -o yaml > http.yaml
```

``` cat httpd.yaml```
```bash
controlplane ~ ➜  cat http.yaml 
apiVersion: v1
kind: Service
metadata:
  creationTimestamp: null
  name: httpd
spec:
  ports:
  - port: 80
    protocol: TCP
    targetPort: 80
  selector:
    run: httpd
status:
  loadBalancer: {}
---
---
apiVersion: v1
kind: Pod
metadata:
  creationTimestamp: null
  labels:
    run: httpd
  name: httpd
spec:
  containers:
  - image: httpd:alpine
    name: httpd
    ports:
    - containerPort: 80
    resources: {}
  dnsPolicy: ClusterFirst
  restartPolicy: Always
status: {}
```