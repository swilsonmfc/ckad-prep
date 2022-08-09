# Probes
* Lifecycle - Pod Status (kubectl get pods in Status column)
  * Pending
  * ContainerCreating
  * Running   
* Pod Conditions (kubectl describe pod in Conditions section)
  * PodScheduled
  * Initialized
  * ContainerReady
  * Ready   

## Readiness Probe
* Waits to set the Ready Condition until the condition is met
* Examples
  * HTTP response code
  * TCP Port test
  * Execute command  
* Options
  * initialDelaySeconds - Wait in seconds
  * periodSeconds - Time between checks   
  * failureThreshold - Default 3, times to check

### Web Readiness
```yaml
apiVersion: v1
kind: Pod
metadata: 
  name: app
spec:
  containers:
  - name: web
    image: nginx
    ports:
    - containerPort: 8080
    readinessProbe:
      httpGet:
        path: /ready
        port: 8080
```

### Exec Command
```yaml
apiVersion: v1
kind: Pod
metadata: 
  name: app
spec:
  containers:
  - name: web
    image: nginx
    ports:
    - containerPort: 8080
    readinessProbe:
      exec:
        command:
        - cat
        - /app/ready
```

### TCP Test
```yaml
apiVersion: v1
kind: Pod
metadata: 
  name: app
spec:
  containers:
  - name: web
    image: nginx
    ports:
    - containerPort: 8080
    readinessProbe:
      tcpSocket:
        port: 5432
```

## Liveness Probe
* Similar to readinessProbe

```yaml
apiVersion: v1
kind: Pod
metadata: 
  name: app
spec:
  containers:
  - name: web
    image: nginx
    ports:
    - containerPort: 8080
    livenessProbe:
      httpGet:
        path: /healthy
        port: 8080
```
