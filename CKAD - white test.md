# CKAD - white test

white test 1

---

## **Section 1: Multi-Container Pods (Init Containers)**

### **Exercice 1: Pod avec Init Container**

- Créez un pod nommé multi-container-pod avec:
- Un init container init-wait qui dort pendant 10 secondes avant de terminer.
- Un conteneur principal app-container basé sur l'image nginx.

> **Objectifs:**
>
> - Créer un pod avec un init container et un conteneur principal.
> - Vérifier que l'init container s'exécute en premier.
> - Observer l'état du pod après le démarrage.

#### ***Déclaratif***

**create pod**

`vim multi-container-pod.yaml`

```bash
apiVersion: v1
kind: Pod
metadata:
  name: multi-container-pod
spec:
  initContainers:
  - name: init-wait
    image: busybox
    command: ["sh","-c","sleep 10"]
  containers:
  - name: app-container
    image: nginx
```

```bash
# apply
kubectl apply -f pod.yaml
# verify execution ordre
kubectl describe pod multi-container-pod
# verify status
kubectl get pod multi-container-pod -w
```

---

## **Section 2: Readiness Probe et Liveness Probe**

### **Exercice 2: Probes**

- Créez un pod nommé probe-pod avec:
- Un conteneur web-server basé sur nginx.
- Une Readiness Probe qui vérifie /index.html via HTTP.
- Une Liveness Probe qui vérifie le bon fonctionnement du serveur toutes les 10 secondes.

> **Objectifs:**
>
> - Configurer et tester la Readiness Probe.
> - Configurer et tester la Liveness Probe.
> - Observer le comportement en cas d'échec des probes.

#### ***Déclaratif***

- **create pod**
- **vim** probe-pod.yaml

```

apiVersion: v1
kind: Pod
metadata:
  name: probe-pod
spec:
  containers:
  - name: web-server
    image: nginx
    ports:
    - containerPort: 80
    readinessProbe:
      httpGet:
        path: /index.html
        port: 80
      initialDelaySeconds: 5
      periodSeconds: 5
    livenessProbe:
      httpGet:
        path: /
        port: 80
      initialDelaySeconds: 10
      periodSeconds: 10
```

```
# apply
kubectl apply -f pod.yaml
# verify
kubectl describe pod probe-pod
kubectl get pod probe-pod -w
```

---

## **Section 3: Container Logging**

### **Exercice 3: Logs des Conteneurs**

- Déployez un pod logging-pod avec un conteneur basé sur busybox, qui génère un message toutes les 5 secondes.

> **Objectifs:**
>
> - Déployer un pod qui écrit des logs.
> - Observer et analyser les logs avec kubectl logs.
> - Rediriger les logs dans un fichier et les récupérer.

#### ***Déclaratif***

- **create pod**

`vim logging-pod.yaml`

```
apiVersion: v1
kind: Pod
metadata:
  name: logging-pod
spec:
  containers:
  - name: logger
    image: busybox
    command: ["sh","-c","while true; do echo log message $(date); sleep 5; done"]
```

```
# apply
kubectl apply -f pod.yaml
# observe logs
kubectl logs logging-pod
# rediger logs dans fichier
kubectl logs logging-pod > logs.txt
# recuperer logs
kubectl logs -f logging-pod > logs.txt
```

---

## **Section 4: Labels et Sélecteurs**

### **Exercice 5: Sélectionner des Pods**

- Créez trois pods avec les labels app=web, app=api, et app=db.
- Sélectionnez uniquement les pods web avec kubectl get pods -l app=web.

> **Objectifs:**
>
> - Comprendre l'utilisation des labels.
> - Apprendre à filtrer des pods avec kubectl.

 

#### ***Impératif :***

```
kubectl run web-pod --image=nginx --restart=Never --labels=app=web
kubectl run api-pod --image=nginx --restart=Never --labels=app=api
kubectl run db-pod --image=nginx --restart=Never --labels=app=db
```

#### ***Déclaratif***

- **create pods**

```bash
vim web-pod.yaml
--------------------
apiVersion: v1
kind: Pod
metadata:
  name: web-pod
  labels:
    app: web
spec:
  containers:
  - name: nginx
    image: nginx
```

```bash
vim api-pod.yaml
--------------------
apiVersion: v1
kind: Pod
metadata:
  name: api-pod
  labels:
    app: api
spec:
  containers:name: nginx
image: nginx
```

```bash
vim db-pod.yaml
--------------------
apiVersion: v1
kind: Pod
metadata:
  name: db-pod
  labels:
    app: db
spec:
  containers:
  - name: nginx
    image: nginx
```

```bash
kubectl apply -f web.yaml
kubectl apply -f api.yaml
kubectl apply -f db.yaml
```

```bash
# filter pod
kubectl get pods -l app=web
kubectl get pods -l app!=db
```

---

## **Section 6: Rolling Update et Rollback**

### **Exercice 6: Recreate Strategy**

- Créez un déploiement web-recreate avec l'image nginx:1.19, puis mettez à jour vers nginx:1.20 en utilisant la stratégie **Recreate**.

> **Objectifs:**
>
> - Créer un déploiement avec 3 réplicas.
> - Définir la stratégie Recreate.
> - Observer l'impact du déploiement.

Impératif :

```bash
# create deployment
kubectl create deployment web-recreate --image=nginx:1.19 --replicas=3
# add reacreate strategy
kubectl patch deployment web-recreate -p '{"spec":{"strategy":{"type":"Recreate"}}}'
# update nginx version
kubectl set image deployment/web-recreate nginx=nginx:1.20
```

#### *Déclaratif :*

`vim deploy.yaml`

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: web-recreate
spec:
  replicas: 3
  strategy:
    type: Recreate
  selector:
    matchLabels:
      app: web-recreate
  template:
    metadata:
      labels:
        app: web-recreate
    spec:
      containers:
      - name: nginx
        image: nginx:1.19

```

```bash
kubectl apply -f deploy.yaml
```

```bash
# Mise à jour vers 1.20 :
kubectl set image deployment/web-recreate nginx=nginx:1.20

# observe
kubectl get pods -w
```

 