# Container Images
* Define, build and modify container images

## Create Container
Create an nginx container using the run command
<details>
  <summary>View</summary>
  
  ```
  kubectl run <name> --image=<image> --restart=<restartPolicy> 
  kubectl run nginx --image=nginx --restart=Never
  ```
</details>
  
## Create Container Yaml
Generate a yaml file for an nginx container 
<details>
  <summary>View</summary>
  
  ```
  kubectl run <name> --image=<image> --restart=<restartPolicy> --dry-run=client -o yaml > nginx.yaml
  kubectl run nginx --image=nginx --restart=Never --dry-run=client -o yaml > nginx.yaml
  ```
</details>
  
## Create Container File
Generate a yaml file for an nginx container 
<details>
  <summary>View</summary>
  
  ```yaml
  apiVersion: v1
  kind: Pod
  metadata:
    name: nginx
  spec:
    containers:
    - name: nginx
      image: nginx
    restartPolicy: Never
  ```
</details>
  
## Create Container
Create a container from yaml file
<details>
  <summary>View</summary>
  
  ```
  kubectl create -f <filename> 
  kubectl create -f nginx.yaml
  ```
</details>
  
## View running pods
Get a list of running pods 
<details>
  <summary>View</summary>
  
  ```
  kubectl get po 
  kubectl get pod 
  kubectl get pods
  ```
</details>
  
## View details of a running pod
Get a list of running pods using the describe command
<details>
  <summary>View</summary>
  
  ```
  kubectl describe <type> <name>
  kubectl describe pod nginx
  ```
</details>
