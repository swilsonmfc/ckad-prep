# Container Images
* Define, build and modify container images

## Create Container
Create an nginx container with memory request and limits

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: nginx
spec:
  containers:
  - name: web
    image: nginx
    resources:
      requests:
        memory: "10Mi"
      limits:
        memory: "50Mi"
```

