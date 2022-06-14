# Job

```yaml
apiVersion: batch/v1
kind: Job
metadata:
  creationTimestamp: null
  name: sleepy
spec:
  completions: 5
  parallelism: 2
  template:
    metadata:
      creationTimestamp: null
    spec:
      containers:
      - image: busybox
        name: resting
        command: ["/bin/sleep"]
        args: ["3"]
        resources: {}
      restartPolicy: Never
status: {}
```
