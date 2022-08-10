## Create Deployment Imperatively
Create a deployment running nginx, named nginx with 3 replicas
```
kubectl create deployment nginx --image=nginx --replicas=3
```

## Create Deployment
Create a deployment with 2 replicas running nginx, name nginx, label worker
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

## Scale Deployment
How can we scale the deployment from 2 to 3
  
### Change the definition file:
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
  
### Run kubectl scale
```
kubectl scale deployment mydep --replicas=3 
kubectl scale -f replica.yaml --replicas=3 
```

## Upgrade Strategies
* Recreate - delete all pods and recreate (not default)
* Rolling
  * New ReplicaSet created
  * Destroys pods in prior version of ReplicaSet   
  * Brings up upgraded pods in new ReplicaSet

## Upgrades
Create a Deployment
```
kubectl create deployment mydeploy --image=nginx
kubectl rollout status deployment/mydeploy
```

Upgrade
```
kubectl set image deployment/mydeploy nginx=nginx:1.19.1
kubectl rollout status deployent/mydeploy
```

View History
```
kubectl rollout history deployment/mydeploy
```

Perform a Rollback
```
kubectl rollback deployment/mydeploy
kubectl rollout undo deployment/mydeploy
kubectl rollout undo deployment/mydeploy --to-revision=1
```

History - Recording
```
kubectl apply -f deploy.yaml --record
```
