## Create Imperative ConfigMap
Create a ConfigMap with literals HOST & PORT  
```
kubectl create cm myconfigmap --from-literal=HOST=myhost.com --from-literal=PORT=3306
```



## Create Imperative ConfigMap Pulling Values From File
Create a ConfigMap from a file
```
kubectl create cm myconfigmap --from-file=HOST=config.txt
```

## Create Imperative ConfigMap From File
Create a ConfigMap from a file
```
kubectl create cm myconfigmap --from-env-file=config.txt
```

## Create Imperative ConfigMap From YAML
Create a ConfigMap from a yaml file

```
apiVersion: v1  
kind: ConfigMap
metadata:
  name: myconfig
data:
  HOST: myhost.com 
  PORT: 3306
```

## Create Pod With Environment Variable
Create a pod declaring a HOST & PORT 
```
apiVersion: v1
kind: Pod
metadata:
  name: pod-cm
spec:
  containers:
  - name: container
    image: nginx
    env:
    - name: HOST
      value: myhost.com
    - name: PORT
      value: 3306
  restartPolicy: Never
```

## Create Pod With Environment Variables
Create a pod declaring a HOST & PORT pulling values from config map
```
apiVersion: v1
kind: Pod
metadata:
  name: pod-cm
spec:
  containers:
  - name: container
    image: nginx
    env:
    - name: HOST
      valueFrom:
        configMapKeyRef:
          name: myconfigmap
          key: HOST
    - name: PORT
      valueFrom:
        configMapKeyRef:
          name: myconfigmap
          key: PORT
  restartPolicy: Never
```

## Create Pod Using ConfigMap
Create a ConfigMap from a file
  
```
apiVersion: v1
kind: Pod
metadata:
  name: pod-cm
spec:
  containers:
  - name: container
    image: nginx
    envFrom:
    - configMapRef:
      name: myconfigmap
  restartPolicy: Never
```

## Create Pod Using ConfigMap Volume
Create a ConfigMap volume and mount in a pod
```
apiVersion: v1
kind: Pod
metadata:
  name: pod-cm
spec:
  volumes:
  - name: config-volume
    configMap:
      name: myconfigmap
  containers:
  - name: container
    image: nginx
    volumeMounts:
    - name: config-volume
      mountPath: /etc/config
  restartPolicy: Never
```
