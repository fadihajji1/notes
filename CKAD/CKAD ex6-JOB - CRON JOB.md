# CKAD ex6-JOB | CRON JOB

---

## JOB

> **Tasks**:
>
> 1. Create a Job named parallel-job with: 
>
> 1. 5 completions (i.e., 5 successful pods).
> 2. Parallelism of 3 (i.e., 3 pods running concurrently).
> 3. A backoff limit of 3 (i.e., retry up to 3 times if a pod fails).
>
> 2. The pod will simply sleep for a few seconds to simulate work.

```
vim parallel-job.yaml
```

```yaml
apiVersion: batch/v1
kind: Job
metadata:
  name: parallel-job
spec:
  completions: 5
  parallelism: 3
  backoffLimit: 3
  template:
    spec:
      containers:
        - name: sleep
          image: busybox
          command: ["sh", "-c", "echo Starting Job; sleep 10"]
      restartPolicy: OnFailure
```

```bash
k apply -f parallel-job.yaml
k get jobs
k describe job parallel-job
```

---

## CRON JOB

> **Tasks**:
>
> 1. Create a CronJob that runs every 1 minute and creates a pod that prints the current time.

```bash
vim cronjob.yaml
```

```yaml
apiVersion: batch/v1
kind: CronJob
metadata:
  name: time-cronjob
spec:
  schedule: "*/1 * * * *"
  jobTemplate:
    spec:
      template:
        spec:
          containers:
            - name: print-time
              image: busybox
              command: ["sh", "-c", "date; echo Current time"]
          restartPolicy: OnFailure
```

```
k apply -f cronjob.yaml
k get cronjob
k get jobs
```

 