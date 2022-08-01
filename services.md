
## Create Service Imperatively
Create a service named nginx-service exposing nginx pod on port 8080
<details>
  <summary>View</summary>
  
  ```
  kubectl expose pod nginx --port=8080 --name nginx-service
  ```
</details>

## Create Pod & Service Imperatively
Create a service named nginx-service exposing nginx pod on port 8080
<details>
  <summary>View</summary>
  
  ```
  kubectl run nginx --image=nginx --port=8080 --expose 
  ```
</details>
