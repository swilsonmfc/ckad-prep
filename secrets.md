## Create Imperative Secrets
Create a Secret with username, password (Note - secrets are not secure -- these are just obscured a bit)
<details>
  <summary>View</summary>
  
  ```
  kubectl create secret generic secrets --from-literal=username=user --from-literal=password=pass
  ```
</details>


## Create Imperative Secrets From File
Create a Secret from a file
<details>
  <summary>View</summary>
  
  ```
  kubectl create secret generic secrets --from-file=secrets.txt
  ```
</details>

## Create Declarative Secrets
Create a Secret from yaml
<details>
  <summary>View</summary>
  
  Base64 encode values
  ```
  echo -n 'user' | base64
  echo -n 'pass' | base64
  ```
  
  ```
apiVersion: v1
kind: Secret
metadata:
  name: secrets
data:
  username: dXNlcg==
  password: cGFzcw==
  ```
</details>


## Consume Secrets in a Pod as Env Variables
Create a Secret from a file
<details>
  <summary>View</summary>
  
  Create pod.yaml
  ```
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
</details>

## Consume Secrets in a Pod as Volume
Create a Secret from a file
<details>
  <summary>View</summary>
  
  Create pod.yaml
  ```
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
</details>
