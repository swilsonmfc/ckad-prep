# Container Images
* Define, build and modify container images

## Create Container
Create an nginx container using the run command
```
kubectl run <name> --image=<image> --restart=<restartPolicy> 
kubectl run nginx --image=nginx --restart=Never
```

## Create Container Yaml
Generate a yaml file for an nginx container 
```
kubectl run <name> --image=<image> --restart=<restartPolicy> --dry-run=client -o yaml > nginx.yaml
kubectl run nginx --image=nginx --restart=Never --dry-run=client -o yaml > nginx.yaml
```
  
## Create Container File
Generate a yaml file for an nginx container 
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: nginx
spec:
  containers:
  - name: nginx
    image: nginx
restartPolicy: Never
```

  
## Create Container
Create a container from yaml file
```
kubectl create -f <filename> 
kubectl create -f nginx.yaml
```

## View running pods
Get a list of running pods 
```
kubectl get po 
kubectl get pod 
kubectl get pods
```
  
## View details of a running pod
Get a list of running pods using the describe command
```
kubectl describe <type> <name>
kubectl describe pod nginx
```

## View the image of a running pod
```
kubectl describe <type> <name> | grep -i image
kubectl describe pod nginx | grep -i image
```
