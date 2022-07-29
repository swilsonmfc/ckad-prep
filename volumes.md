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

## Create Persistent Volume, Claim & Pod
Create an nginx container using a persistent volume
<details>
  <summary>View</summary>
  
  ```
  kind: PersistentVolume
  apiVersion: v1
  metadata:
    name: mypvol
  spec:
    storageClassName: standard
    capacity:
      storage: 10Mi
    accessModes:
      - ReadWriteOnce
      - ReadWriteMany
    hostPath:
      path: /etc/pvol
  ```
  
  ```
  apiVersion: v1
  kind: PersistentVolumeClaim
  metadata:
    name: mypvc
  spec:
    storageClassName: standard
    accessModes:
      - ReadWriteOnce
    resources:
      requests:
        storage: 1Mi
  ```
  
  ```
  apiVersion: v1
  kind: Pod
  metadata:
    name: nginx
  spec:
    volumes:
    - name: myvol
      persistentVolumeClaim:
        claimName: mypvc
    containers:
    - name: nginx
      image: nginx
      volumeMounts:
      - name: myvol
        mountPath: /etc/data
    restartPolicy: Never
  ```
</details>
