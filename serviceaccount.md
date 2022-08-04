## Create Imperative ServiceAccount
Create a ServiceAccount for the metrics-server
  <summary>View</summary>
  
  ```
  kubectl create serviceaccount metrics-server
  ```
  
  ```
  kubectl get serviceaccount 
  ```
</details>

## View ServiceAccount Token
Create a ServiceAccount for the metrics-server
<details>
  <summary>View</summary>
  
  ```
  kubectl create serviceaccount metrics-server
  ```
  
  ```
  kubectl get serviceaccount 
  ```
  
  ```
  kubectl describe secret metrics-server-token-<hash>
  ```
  
  Token can be included in "Authorization: Bearer ..." headers
</details>
  
## Mount ServiceAccount Token
Obtain the token for the metrics-server
<details>
  <summary>View</summary>
  
  ```
  kubectl create serviceaccount metrics-server
  ```
  
  ```
  kubectl get serviceaccount 
  ```
  
  ```
  kubectl describe secret metrics-server-token-<hash>
  ```
  
  Token can be included in "Authorization: Bearer ..." headers
  Can be volume mounted into pods
</details>
