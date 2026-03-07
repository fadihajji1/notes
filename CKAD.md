# CKAD

### SECTION 1

1. Deploy a Pod : **IMPERATIVE**

- create a Pod named my-pod in the test-namespace namespace.
- The Pod should use the nginx:latest image and run on port 80. 
- Expose this Pod using a ClusterIP service named my-service.

```
kubectl run my-pod \
  --image=nginx:latest \
  --port=80 \
  --restart=Never \
  -n test-namespace
```

verify:

```bash
kubectl get pods -n test-namespace
```

Expose the Pod with a ClusterIP Service

```
kubectl expose pod my-pod \
  --name=my-service \
  --port=80 \
  --target-port=80 \
  --type=ClusterIP \
  -n test-namespace
```

verify:

```
kubectl get svc -n test-namespace
```

**CHECK EVERYTHING:**

```
kubectl get pods -n test-namespace
kubectl get svc -n test-namespace
kubectl describe svc my-service -n test-namespace
```

---

**DECLARATIVE:**

- **my-pod:**

```
vim my-pod.yaml
```

`apiVersion: v1
kind: Pod
metadata:
  name: my-pod
  namespace: test-namespace
  labels:
    app: nginx
spec:
  containers:`

  `- name: nginx`  
    `image: nginx:latest`  
  `ports:`

  `- containerPort: 80`

 

- **my-service:**

```
vim my-service.yaml
apiVersion: v1
kind: Service
metadata:
  name: my-service
  namespace: test-namespace
spec:
  selector:
    app: nginx
  ports:
  - protocol: TCP
    port: 80
    targetPort: 80
  type: ClusterIP
```

  
apply

```
kubectl apply -f my-pod.yaml
kubectl apply -f my-service.yaml
```

---

### SECTION 2

2. Create a Deployment

- Create a Deployment named web-deploy with 3 replicas.
- The Deployment should use the image httpd:latest.

3. Namespace Creation

- Create a namespace called dev-team.
- Deploy a Pod named app1 in the dev-team namespace using the image busybox that runs the command sleep 3600.

#### Imperative --------------------------------

**Create ConfigMap**

```
kubectl create configmap app-config --from-literal=DB_HOST=mysql
```

Verify

`kubectl get configmap app-config`

Create Secret

```
kubectl create secret generic app-secret --from-literal=DB_PASSWORD=Secure
```

Verify

`kubectl get secret app-secret`

**Create Pod configered-app.yaml using dry-run:**

```
vim pod.yaml
```

```
apiVersion: v1
kind: Pod
metadata:
  name: configured-app
spec:
  containers:
  - name: configured-app
    image: nginx
    volumeMounts:
    - name: config-volume
      mountPath: /etc/config
    - name: secret-volume
      mountPath: /etc/secret
  volumes:
  - name: config-volume
    configMap:
      name: app-config
  - name: secret-volume 
    secret:
      secretName: app-secret
```

```
kubectl apply -f pod.yaml
```

#### Declarative

`vim app-config.yaml`

`vim app-secret.yaml`

`vim configured-app.yaml`

```
apiVersion: v1
kind: ConfigMap
metadata:
  name: app-config
data:
  DB_HOST: mysql
```

```
apiVersion: v1
kind: Secret
metadata:
  name: app-secret
type: Opaque
stringData:
  DB_PASSWORD: Secure
```

```
apiVersion: v1
kind: Pod
metadata:
  name: configured-app
spec:
  containers:
  - name: nginx
    image: nginx
    volumeMounts:
    - name: config-volume
      mountPath: /etc/config
    - name: secret-volume
      mountPath: /etc/secret
  volumes:
    - name: config-volume
      configMap:
        name: app-config
    - name: secret-volume
      secret:
        secretName: app-secret
```

```
kubectl apply -f config-secret-pod.yaml
```

 