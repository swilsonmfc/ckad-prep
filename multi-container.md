# Multi-Containers
* Share same lifecycle
* Share same network and storage

## Create Container
Create two containers in the same pod & retrieve details / logs
```
apiVersion: v1
kind: Pod
metadata: 
  name: multi
spec:
  containers:
  - name: container1
    image: busybox
    command: [ "/bin/sh", "-c", "--" ]
    args: [ "while true; do sleep 60; done;" ]
  - name: container2
    image: busybox
    command: [ "/bin/sh", "-c", "--" ]
    args: [ "while true; do sleep 60; done;" ]
    
  restartPolicy: Never
```
  
Describe
```
kubectl describe po multi
```
  
Log files
```
kubectl logs multi -c container1
kubectl logs multi -c container2
```

## Init Container
```
apiVersion: v1
kind: Pod
metadata:
  name: webapp
spec:
  volumes:
  - name: logs
    emptyDir: {}
  initContainers:
  - name: startup
    image: busybox
    command: ["sleep", "30"]
  containers:
  - name: app
    image: nginx
    ports:
    - containerPort: 80
    volumeMounts:
    - name: logs
      mountPath: /var/logs
```

## Sidecar Pattern
* Helper container that coexists with main functionality
* File sync / watcher
* Handling / standardizing logging format
```
apiVersion: v1
kind: Pod
metadata:
  name: webapp
spec:
  volumes:
  - name: logs
    emptyDir: {}
  containers:
  - name: app
    image: nginx
    ports:
    - containerPort: 80
    volumeMounts:
    - name: logs
      mountPath: /var/logs
  - name: logger
    image: agent
    volumeMounts:
    - name: logs
      mountPath: /var/logs
```

## Adapter Pattern
* Specialization of sidecar
* Present a standard interface
* Adapt logs & metrics for collection by prometheus

## Ambassador Pattern
* Provide a standard interface to outside services consumed by main
* Accessing cached data / database location
