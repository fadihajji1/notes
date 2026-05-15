# CKAD ex7-Resources

> **Tasks**:
>
> Create a pod named nginx-resource with resource memory: "64Mi" cpu: "250m requests and limits.

```bash
vim nginx-resource.yaml
```

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: nginx-resource
spec:
  containers:
    - name: nginx
      image: nginx
      resources:
        requests:
          memory: "64Mi"
          cpu: "250m"
        limits:
          memory: "64Mi"
          cpu: "250m"
```

```bash
k apply -f nginx-resource.yaml
```

 