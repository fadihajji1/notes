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
k apply -f my-pvc.yaml 
# verify
k get pvc
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

1. **StorageClass**
  ```bash
  vim storageclassnew.yaml
  ```
  ```
  apiVersion: storage.k8s.io/v1
  kind: StorageClass
  metadata:
    name: storageclassnew
  provisioner: kubernetes.io/no-provisioner
  volumeBindingMode: WaitForFirstConsumer
  ```
  ```
  k apply -f storageclassnew.yaml
  k get storageclass
  ```
2. **PV**
  ```bash
  vim my-pv-4gi.yaml
  ```
  ```
  apiVersion: v1
  kind: PersistentVolume
  metadata:
    name: my-pv-4gi
  spec:
    capacity:
      storage: 4Gi
    accessModes:
      - ReadWriteOnce
    persistentVolumeReclaimPolicy: Retain
    storageClassName: storageclassnew
    hostPath:
      path: /mnt/data4gi
  ```
  ```
  k apply -f my-pv-4gi.yaml
  k get pv
  ```
3. **PVC**
  ```
  vim my-pvc-4gi.yaml
  ```
  ```
  apiVersion: v1
  kind: PersistentVolumeClaim
  metadata:
    name: my-pvc-4gi
  spec:
    accessModes:
      - ReadWriteOnce
    resources:
      requests:
        storage: 4Gi
    storageClassName: storageclassnew
  ```
  ```
  k apply -f my-pvc-4gi.yaml
  k get pvc
  ```
4. Deploy a Pod that mounts the PVC
  ```
  vim my-pod-4gi.yaml
  ```
  ```
  apiVersion: v1
  kind: Pod
  metadata:
    name: my-pod-4gi
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
          claimName: my-pvc-4gi
  ```
  ```
  k apply -f my-pod-4gi.yaml
  k get pods
  ```

 