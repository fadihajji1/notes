# CKAD ex5-Taint&Tolerations

> **Tasks**:
>
> 1. Taint a node with key=value:NoSchedule.
> 2. Create a pod that tolerates the taint.

1. **Taint a Node:**
  ```bash
  # Taint node (replace NODE_NAME with your node)
  kubectl taint nodes worker-1 env=prod:NoSchedule
  ```
2. **Tolerate a pod with the taint**

create a pod:

`vim pod.yaml`

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: tolerant-pod
spec:
  containers:
    - name: nginx
      image: nginx
  tolerations:
    - key: "env"
      operator: "Equal"
      value: "prod"
      effect: "NoSchedule"
```

```bash
kubectl apply -f pod.yaml
```

```bash
# validation
kubectl describe node <node-name> | grep Taints
kubectl describe pod tolerant-pod
```

 