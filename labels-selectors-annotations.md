# Labels, Selectors and Annotations
* Labels & Selectors - Group and Find Objects
* Annotations - Additional details (build version etc)

## Imperatively add Labels
```
kubectl label pod mypod service=backend
```

## Declaratively Label
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: mypod
  labels:
    service: backend
spec:
  containers:
  - image: nginx
    name: backend
```

## Select Pods with Label
```
kubectl get pod -l service=backend
kubectl get pod -l 'service in (backend)'
```

## ReplicaSet - Label Selector
* Note selector.matchLabels & template.metadata.labels agree
```yaml
apiVersion: apps/v1
kind: ReplicaSet
metadata:
  name: webapp
  labels: 
    type: frontend
spec: 
  replicas: 2
  selector:
    matchLabels:
      type: frontend
  template:
    metadata:
      labels:
        type: frontend
    spec:
      containers:
      - name: webserver
        image: nginx
```
