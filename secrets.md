## Notes:
* https://kubernetes.io/docs/concepts/configuration/secret/#risks

## Create Imperative Secrets
Create a Secret with username, password (Note - secrets are not secure -- these are just obscured a bit)
```
kubectl create secret generic secrets --from-literal=username=user --from-literal=password=pass
```

## Create Imperative Secrets From File
Create a Secret from a file
```
kubectl create secret generic secrets --from-file=secrets.txt
```

## Create Declarative Secrets
Create a Secret from yaml (Base64 encode values)
```
echo -n 'user' | base64
echo -n 'pass' | base64
```
  
```yaml
apiVersion: v1
kind: Secret
metadata:
  name: secrets
data:
  username: dXNlcg==
  password: cGFzcw==
```

## Consume Secrets in a Pod as Env Variables
Create a Secret from a file
  
Create pod.yaml
```yaml
apiVersion: v1
kind: Pod
metadata: 
  name: app
spec:
  containers:
  - name: app
    image: nginx
    envFrom:
    - secretRef:
        name: secrets
```
  
Create pod  
```
kubectl create -f pod.yaml
```

## Consume Secrets in a Pod as Volume
Create a Secret from a file

Create pod.yaml
```yaml
apiVersion: v1
kind: Pod
metadata: 
  name: app
spec:
  volumes:
  - name: app-volume
    secret:
      secretName: secrets
  containers:
  - name: app
    image: nginx
    volumeMounts:
    - name: app-volume
      mountPath: /opt/secrets
```
  
Create pod
```
kubectl create -f pod.yaml
```
