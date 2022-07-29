# Volumes

## Create Volume
Create an nginx container with an empy directory volume
<details>
  <summary>View</summary>
  
  ```
  apiVersion: v1
  kind: Pod
  metadata:
    name: nginx
  spec:
    volumes:
    - name: myvol
      emptyDir: {}
    containers:
    - name: nginx
      image: nginx
      volumeMounts:
      - name: myvol
        mountPath: /etc/data
    restartPolicy: Never
  ```
</details>

## Create Persistent Volume
Create an nginx container using the run command
<details>
  <summary>View</summary>
  
  ```
  Persistent Volume
  ```
  
  ```
  Persistent Volume Claim
  ```
  
  ```
  Pod
  ```
</details>
