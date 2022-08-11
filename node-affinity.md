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
```yaml
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
```yaml
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

## Declarative Affinity - Deployments
Affinity for deployment on frontend nodes
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: mydeploy
spec:
  replicas: 5
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx
        image: nginx
      affinity:
        nodeAffinity:
          requiredDuringSchedulingIgnoredDuringExecution:
            nodeSelectorTerms:
            - matchExpressions:
              - key: type
                operator: In
                values:
                - frontend
```
