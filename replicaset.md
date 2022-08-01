## Create ReplicaSet
Create a replicaset with 2 replicas running nginx, name nginx, label worker
<details>
  <summary>View</summary>
  
  ```
apiVersion: apps/v1
kind: ReplicaSet
metadata: 
  name: myrs
spec:
  template:
    metadata:
      name: myapp
      labels:
        type: worker
    spec:
      containers:
      - name: nginx
        image: nginx
  replicas: 2
  selector:
    matchLabels:
      type: worker
 ```
</details>

## Scale ReplicaSet
How can we scale the replica set from 2 to 3
<details>
  <summary>View</summary>
  
  Change the definition file:
  ```
  kubectl replace -f replica.yaml 
  ```
  
  ```
apiVersion: apps/v1
kind: ReplicaSet
metadata: 
  name: myrs
spec:
  template:
    metadata:
      name: myapp
      labels:
        type: worker
    spec:
      containers:
      - name: nginx
        image: nginx
  replicas: 3
  selector:
    matchLabels:
      type: worker
  ```
  
  Run kubectl scale
  ```
  kubectl scale --replicas=3 replicaset myrs
  kubectl scale --replicas=3 -f replica.yaml
  ```
</details>
