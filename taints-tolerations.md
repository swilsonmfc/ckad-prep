## Taint a Node
Taint Node1 with type=frontend as NoSchedule
<details>
  <summary>View</summary>
  
  ```
  kubectl taint nodes node1 type=frontend:NoSchedule
  ```
</details>

## Tolerations for a Pod
Taint Node1 with type=frontend as NoSchedule
<details>
  <summary>View</summary>
  
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
</details>

## Taint a Node
Remove the tain on Node1 with type=frontend and NoSchedule
<details>
  <summary>View</summary>
  
  ```
  kubectl taint nodes node1 type=frontend:NoSchedule-
  ```
</details>
