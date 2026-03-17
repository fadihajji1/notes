# **CKAD ex3-DEPLOYMENTS**

***Imperative***

```bash
# Q1: Create deployment web-deploy with nginx:1.18 (imperative)
k create deployment web-deploy \
 --image=nginx:1.18 \
 --replicas=2
 --labels="app=httpd,tier=backend,env=production"
```

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
```

```bash
# Q6: Scale web-deploy to 4 replicas
k scale deployment web-deploy --replicas=4
```

```bash
# Q7: Delete only the deployment (keep pods if possible)
k delete deployment httpd-deploy --cascade=orphan
```

```bash
# Q8: Delete all deployments with label tier=frontend
k delete deployments -l tier=frontend
```

 