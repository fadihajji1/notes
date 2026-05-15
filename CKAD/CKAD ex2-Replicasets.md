# CKAD ex2-Replicasets

#### ***Impreative***

```bash
# Q2: Create rs-apache using dry-run → yaml → edit → apply
k create rs rs-apache --image=httpd:2.4 
 --replicas=2 
 --dry-run=client 
 -o yaml > rs-apache.yaml 
```

**Delete a ReplicaSet**

```
kubectl delete rs <replicaset-name>
```

---

#### *Declarative*

```bash
# Q1: Create ReplicaSet rs-nginx (declarative)

vim rs-nginx.yaml
--------------------
apiVersion: apps/v1
kind: ReplicaSet
metadata:
  name: rs-nginx
spec:
  replicas: 3
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx
        image: nginx:1.19
```

```bash
# Apply the ReplicaSet:
k apply -f rs-nginx.yaml
```

---

***edit replicasetes (IMPERATIVE)***

```bash
# imperative
# Q3: Scale rs-nginx to 5 replicas
k scale rs rs-nginx --replicas=5
```

```bash
#Q4: Scale rs-apache to 1 replica
k scale rs rs-apache --replicas=1
```

```bash
# Q5: Change image of rs-nginx to nginx:1.25
k set image rs/rs-nginx nginx=nginx:1.25
```

```bash
# Q6: Delete rs-apache
k delete rs rs-apache
```

```bash
# Q7: Delete all ReplicaSets with label tier=frontend
k delete rs -l tier=frontend
```

```bash
# Q8: Get names of pods labels=nginx
k get pods -l app=nginx 
```

 