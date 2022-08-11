# Jobs and CronJobs

## Jobs
Create an imperative simple job
```
kubectl create job myjob --image=busybox -- sleep 10
```

Create a declarative job
```yaml
apiVersion: batch/v1
kind: Job
metadata:
  name: myjob
spec:
  template:
    spec:
      containers:
      - name: myjob
        image: busybox
        command: ["echo", "world"]
```

Create a declarative job with 3 parallel workers
```yaml
apiVersion: batch/v1
kind: Job
metadata:
  name: myjob
spec:
  parallelism: 3
  template:
    spec:
      containers:
      - name: myjob
        image: busybox
        command: ["echo", "world"]
      restartPolicy: Never
```

Create a declarative job with 3 completions
```yaml
apiVersion: batch/v1
kind: Job
metadata:
  name: myjob
spec:
  completions: 3
  template:
    spec:
      containers:
      - name: myjob
        image: busybox
        command: ["echo", "world"]
      restartPolicy: Never
```

## CronJobs
Create a job that runs every minute
```yaml
apiVersion: batch/v1
kind: CronJob
metadata:
  name: myjob
spec:
  schedule: "* * * * *"
  template:
    spec:
      containers:
      - name: myjob
        image: busybox
        command: ["echo", "world"]
      restartPolicy: OnFailure
```

