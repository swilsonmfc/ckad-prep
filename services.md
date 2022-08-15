
## Create Service Imperatively
Create a service named nginx-service exposing nginx pod on port 8080  
```
kubectl expose pod nginx --port=8080 --name nginx-service
```

## Create Service Imperatively
Create a service named nginx-service exposing nginx pod on port 8080 targeting port 80
```
kubectl expose pod nginx --port=8080 --target-port=80 --name nginx-service
```

## Create Pod & Service Imperatively
Create a service named nginx-service exposing nginx pod on port 8080
```
kubectl run nginx --image=nginx --port=8080 --expose 
```

## Create a Declarative ClusterIP Service
* Ports
  * nodePort - Port listening on the node that will forward to the service
    * Default = auto-assigned
    * Must be in range 30000 and 32767
  * port - Port in the service handling incoming requests from nodePort
    * Required
  * targetPort - Target to send traffic to on selected pods
    * Default = port
* Selector
  * List of labels to find routed pods
```yaml
apiVersion: v1
kind: Service
metadata:
  name: mysvc
spec:
  type: ClusterIP
  ports:
  - port: 80
    targetPort: 8080
  selector:
    app: frontend
```

## Create a Declarative NodePort
* Ports
  * nodePort - Port listening on the node that will forward to the service
    * Default = auto-assigned
    * Must be in range 30000 and 32767
  * port - Port in the service handling incoming requests from nodePort
    * Required
  * targetPort - Target to send traffic to on selected pods
    * Default = port
* Selector
  * List of labels to find routed pods
```yaml
apiVersion: v1
kind: Service
metadata:
  name: mysvc
spec:
  type: NodePort
  ports:
  - targetPort: 30001
    port: 80
    targetPort: 8080
  selector:
    app: frontend
```
