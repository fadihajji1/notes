# **CKAD ex3-DEPLOYMENTS**

***Imperative***

```bash
# Q1: Create deployment web-deploy with nginx:1.18 (imperative)
k create deployment web-deploy \
 --image=nginx:1.18 \
 --replicas=2
 --labels="app=httpd,tier=backend,env=production"
```

**additional functionalities on deployement:**

```bash
# Scale a deployment
kubectl scale deployment nginx-deployment --replicas=2
```

- **rollout** : used for updating

```bash
#Use kubectl rollout to check deployment history
kubectl rollout history deployment/nginx-deployment
#other rollout uses
....
#Rolling Update to change image to nginx:latest
kubectl set image deployment/nginx-deployment nginx=nginx:latest

# check deployment Rollout status | history
kubectl rollout status deployment/nginx-deployment
kubectl rollout history deployment/nginx-deployment

```

**Recreate the Deployment:**

- In Kubernetes, **Recreate** is an update strategy.
- You need to change the deployment strategy from **RollingUpdate** to **Recreate**.

```bash
kubectl edit deployment nginx-deployment
# in yaml file, replace entire strategy section:
# from
strategy:
  type: RollingUpdate
# to:
strategy:
  type: Recreate

```

```bash
# check yaml file
kubectl get deployment nginx-deployment -o yaml

```

---

#### **SUMMARY**:

```
k create deployment nginx-deployment --image=nginx
k scale deployment nginx-deployment --replicas=2
k scale deployment nginx-deployment --replicas=4
k rollout history deployment/nginx-deployment
k set image deployment/nginx-deployment nginx=nginx:latest
k edit deployment nginx-deployment
```

---

***Declarative***

```yaml
# Q2: Create deployment httpd-deploy using YAML

vim httpd-deploy.yaml
-----------------------------
apiVersion: apps/v1
kind: Deployment
metadata:
  name: httpd-deploy
  labels:
    app: httpd
    tier: backend
    env: production
spec:
  replicas: 3
  selector:
    matchLabels:
      app: httpd
  template:
    metadata:
      labels:
        app: httpd
        tier: backend
        env: production
    spec:
      containers:
      - name: httpd
        image: httpd:2.4
        ports:
          - containerPort: 80
```

```bash
# Apply it:
k apply -f httpd-deploy.yaml
```

---

***Edit deployment***

```bash
# Q3: Display all deployments
k get deployments
```

```bash
# Q4: Edit web-deploy and change image to nginx:1.21
k edit deployment web-deploy
## spec.template.spec.containers[].image
```

```bash
# Q5: Update image of httpd-deploy to httpd:2.6
k set image deployment/httpd-deploy httpd=httpd:2.6
# apply it
```

```bash
# Q6: Scale web-deploy to 4 replicas
k scale deployment web-deploy --replicas=4
# apply it
```

```bash
# Q7: Delete only the deployment (keep pods if possible)
k delete deployment httpd-deploy --cascade=orphan
```

```bash
# Q8: Delete all deployments with label tier=frontend
k delete deployments -l tier=frontend
```

 