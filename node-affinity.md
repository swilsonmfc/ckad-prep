# Node Affinity
* Types
  * requiredDuringSchedulingIgnoredDuringExecution
  * preferredDuringSchedulingIgnoredDuringExecution
* DuringScheduling
  * Required - Mandates that it fit the rules
  * Preferred - Will try, unless it can't place the pod, then it will go anywhere
* DuringExecution
  * Ignored - Does not force eviction - continue running
  * Required - Not yet available - Will evict if not matching   

## Declarative Affinity
Assign affinity to Big and Medium node types
```
apiVersion: v1
kind: Pod
metadata:
  name: mypod
spec:
  containers:
  - name: worker
    image: nginx
  affinity:
    nodeAffinity:
      requiredDuringScheduledIgnoredDuringExecution:
        nodeSelectorTerms:
        - matchExpression:
          - key: type
            operator: In
            values:
            - Big
            - Medium
```

## Declarative Affinity
Assign affinity to exclude Small Nodes
```
apiVersion: v1
kind: Pod
metadata:
  name: mypod
spec:
  containers:
  - name: worker
    image: nginx
  affinity:
    nodeAffinity:
      requiredDuringScheduledIgnoredDuringExecution:
        nodeSelectorTerms:
        - matchExpression:
          - key: type
            operator: NotIn
            values:
            - Small
```
