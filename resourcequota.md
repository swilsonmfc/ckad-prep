## Create ResourceQuota
Create a resource quota for the testing namespace
<details>
  <summary>View</summary>
  
  ```
apiVersion: v1
kind: ResourceQuota
metadata: 
  name: myquota
  namespace: testing
spec:
  hard:
    pods: "3"
    requests.cpu: ".5"
    requests.memory: 100Mi
    limits.cpu: "1"
    limits.memory: 200Mi
 ```
</details>
