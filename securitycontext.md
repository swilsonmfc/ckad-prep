## Create Pod with SecurityContext
Create a pod running as user 1001 with capability SYS_TIME
<details>
  <summary>View</summary>
  
  ```
apiVersion: v1
kind: Pod
metadata:
  name: example
spec:
  containers:
  - name: worker
    image: nginx
    securityContext:
      runAsUser: 1001
      capabilities:
        add: ['SYS_TIME']
```
</details>

