## Taint a Node
Taint Node1 with type=frontend as NoSchedule
```
kubectl taint nodes node1 type=frontend:NoSchedule
```

## Tolerations for a Pod
Add Toleration for type=frontend as NoSchedule
```
apiVersion: v1
kind: Pod
metadata:
  name: web
spec:
  containers:
  - name: nginx
    image: nginx
  tolerations:
  - key: "type"
    value: "frontend"
    operator: "Equal"
    effect: "NoSchedule"
```

## Taint a Node
Remove the taint on Node1 with type=frontend and NoSchedule
```
kubectl taint nodes node1 type=frontend:NoSchedule-
```
