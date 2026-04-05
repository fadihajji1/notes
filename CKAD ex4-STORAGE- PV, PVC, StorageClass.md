# CKAD ex4-STORAGE: PV, PVC, StorageClass

 

> ### **Task 1:**
>
> 1. Create a PV named my-pv with 1Gi of storage.
> 2. Create a PVC named my-pvc requesting 1Gi of storage.
> 3. Create a pod named nginx-pod-with-pv and mount the PVC.

 

***Declarative*** 

1. ***create PV***
  ```yaml
  vim my-pv.yaml
  ```
  ```yaml
  apiVersion: v1
  kind: PersistentVolume
  metadata:
    name: my-pv
  spec:
    capacity:
      storage: 1Gi
    accessModes:
      - ReadWriteOnce
    hostPath:
      path: /mnt/data
  ```
  ```
  #apply it
  k apply -f my-pv.yaml 
  # verify
  k get pv
  ```
2. **create PVC**

```yaml
vim my-pvc.yaml
```

```yaml
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: my-pvc
spec:
  accessModes:
    - ReadWriteOnce
  resources:
    requests:
      storage: 1Gi
```

```
# apply it
k apply -f my-pv.yaml 
# verify
k get pv
```

1. **create a Pod and mount the PVC**

```
apiVersion: v1
kind: Pod
metadata:
  name: nginx-pod-with-pv
spec:
  containers:
    - name: nginx
      image: nginx
      volumeMounts:
        - name: my-storage
          mountPath: /usr/share/nginx/html
  volumes:
    - name: my-storage
      persistentVolumeClaim:
        claimName: my-pvc
```

```
k apply -f nginx-pod-with-pv.yaml
k get pods
k describe pod nginx-pod-with-pv
```

---

> TASK 2:
>
> ### **Using a StorageClass, PV, PVC, and PodSteps:**
>
> 1. Create a **StorageClass** called  storageclassnew  with:
>   - provisioner: kubernetes.io/no-provisioner
>   - volumeBindingMode: WaitForFirstConsumer
> 2. Create a **PersistentVolume (PV)** of 4Gi **accessMode**: RWo , **policy**:  Retain  .
> 3. Create a **PersistentVolumeClaim (PVC)** that binds to the PV.
>
> Deploy a **Pod** that mounts the PVC

 

 

 