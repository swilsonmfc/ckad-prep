# Multi-Containers

## Create Container
Create two containers in the same pod & retrieve details / logs
<details>
  <summary>View</summary>
  
  ```
apiVersion: v1
kind: Pod
metadata: 
  name: multi
spec:
  containers:
  - name: container1
    image: busybox
    command: [ "/bin/sh", "-c", "--" ]
    args: [ "while true; do sleep 60; done;" ]
  - name: container2
    image: busybox
    command: [ "/bin/sh", "-c", "--" ]
    args: [ "while true; do sleep 60; done;" ]
  restartPolicy: Never
  ```
  
  Describe
  ```
  kubectl describe po multi
  ```
  
  Log files
  ```
  kubectl logs multi -c container1
  kubectl logs multi -c container2
  ```
</details>

## Init Container

## Sidecar

## Adapter / Proxy
