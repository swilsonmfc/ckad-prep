# Volumes

## Create Volume
Create an nginx container with an empy directory volume

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


## Create Persistent Volume, Claim & Pod
Create an nginx container using a persistent volume
  
```
apiVersion: v1
kind: PersistentVolume
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
