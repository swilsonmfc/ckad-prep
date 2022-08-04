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
