## Create Deployment Imperatively
Create a deployment running nginx, named nginx with 3 replicas
<details>
  <summary>View</summary>
  
  ```
  kubectl create deployment nginx --image=nginx --replicas=3
  ```
</details>

## Create Deployment
Create a deployment with 2 replicas running nginx, name nginx, label worker
<details>
  <summary>View</summary>
  
  ```
apiVersion: apps/v1
kind: Deployment
metadata: 
  name: mydep
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

## Scale Deployment
How can we scale the deployment from 2 to 3
<details>
  <summary>View</summary>
  
  Change the definition file:
  ```
  kubectl replace -f replica.yaml 
  ```
  
  ```
apiVersion: apps/v1
kind: Deployment
metadata: 
  name: mydep
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
  kubectl scale deployment mydep --replicas=3 
  kubectl scale -f replica.yaml --replicas=3 
  ```
</details>
