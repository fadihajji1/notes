# CKAD ex1-Pods

> **for declarative:**
>
> ```
> i : to insert  
> :wq! : to save and exit 
> ```

---

### create pod my-pod with

- nginx image, 
- port 80,
- no restart, 
- sleeps in 1 hour,
- test-namespace namespace,
- generate yaml to pod.yaml
- Environment Variables

---

#### ***IMPERATIVE***

```bash
# need to create namespace of the pod
k create namespace test-namespace
```

```bash
# create pod my-pod
k run my-pod \
  --image=nginx:latest \
  --labels=pod1 \
  --port=80 \
  --restart=Never \
  -- /bin/sh -c "sleep 3600" \
  -n test-namespace \
  --dry-run=client -o yaml > pod.yaml \
  --env="MODE=production" \
```

#### edit pod in multiple methods

```bash
### edit multiple fields
kubectl edit pod <pod-name>
### add label 
kubectl patch pod <pod-name> -p '{"metadata":{"labels":{"env":"prod"}}}'
### For real changes (image, ports…), delete and recreate the pod
kubectl delete pod <pod-name>
```

#### expose cluster

```bash
# create and expose service with a ClusterIP of my-pod
k expose pod my-pod 
  --name=my-service 
  --port=80 
  --target-port=80 
  --type=ClusterIP 
  -n test-namespace
```

---

---

#### ***DECLARATIVE:***

```
# need to create namespace of the pod
apiVersion: v1
kind: Namespace
metadata:
 name: test-namespace
```

```bash
# apply it
k apply -f namespace.yaml
```

---

```
# create pod my-pod
vim my-pod.yaml
-----------------------
apiVersion: v1
kind: Pod
metadata:
  name: my-pod
  namespace: test-namespace
  labels:
    app: pod1
spec:
  restartPolicy: Never
  
  containers:
    - name: my-pod
      image: nginx:latest
      command: ["sleep", "3600"]
      ports:
        - containerPort: 80
      env:
        - name: MODE
          value: "production"
```

```
# apply it
k apply -f my-pod.yaml
```

---

```yaml
# Expose the Pod with a ClusterIP Service (create service)
vim my-service.yaml
--------------------------

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

```bash
#apply
k apply -f my-service.yaml
```

---

```bash
#CHECK EVERYTHING:
kubectl get pods -n test-namespace
kubectl get svc -n test-namespace
kubectl describe svc my-service -n test-namespaceS
```

---

### SECTION 2

2. Create a Deployment

- Create a Deployment named web-deploy with 3 replicas.
- The Deployment should use the image httpd:latest.

3. Namespace Creation

- Create a namespace called dev-team.
- Deploy a Pod named app1 in the dev-team namespace using the image busybox that runs the command sleep 3600.

#### *Imperative*

```bash
#apply
k create configmap app-config --from-literal=DB_HOST=mysql
#Verify
   k get configmap app-config
#Create Secret
   k create secret generic app-secret --from-literal=DB_PASSWORD=Secure
#Verify
   k get secret app-secret
```

```yaml
#Create Pod configered-app.yaml using dry-run:
vim pod.yaml
```

```bash
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

#### *Declarative*

```yaml
vim app-config.yaml
vim app-secret.yaml
vim configured-app.yaml
```

```yaml
apiVersion: v1
kind: ConfigMap
metadata:
  name: app-config
data:
  DB_HOST: mysql
```

```yaml
apiVersion: v1
kind: Secret
metadata:
  name: app-secret
type: Opaque
stringData:
  DB_PASSWORD: Secure
```

```yaml
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

```bash
k apply -f app-config.yaml
k apply -f app-secret.yaml
k apply -f configured-app.yaml
```

```bash
#verify:
k exec -it configured-app -- /bin/bash
cat /etc/config/DB_HOST 
cat /etc/secret/DB_PASSWORD
```

output:

1. mysql
2. Secure

 