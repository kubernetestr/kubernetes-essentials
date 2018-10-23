#### Storage Class
```bash
kubectl get storageclass
kubectl get storageclass standard -o yaml
kubectl apply -f 01-gcpd-pv-pvc.yaml 
kubectl get pv
gcloud compute disks  list
```

### SSD Class
```bash
kubectl apply -f storage-sdd.yaml
kubectl get storageclass
kubectl apply -f 02-gcpd-pv-pvc.yaml
kubectl get pvc
kubectl get pv
```

#### what should go wrong
```bash
kubectl delete pvc pvc-data1 pvc-data2
kubectl get pvc
kubectl get pv
kubectl get pv pvc-c0a10dce-d68e-11e8-89dc-42010a9c0015 -o yaml
```

```yaml
spec:
  accessModes:
  - ReadWriteOnce
  capacity:
    storage: 10Gi
  claimRef:
    apiVersion: v1
    kind: PersistentVolumeClaim
    name: pvc-data1
    namespace: default
    resourceVersion: "173319"
    uid: c0a10dce-d68e-11e8-89dc-42010a9c0015
  gcePersistentDisk:
    fsType: ext4
    pdName: gke-meetup-a2eade41-dy-pvc-c0a10dce-d68e-11e8-89dc-42010a9c0015
  persistentVolumeReclaimPolicy: Retain
  storageClassName: ssd
status:
  phase: Bound
```

```bash
kubectl delete pvc pvc-data1  pvc-data2
kubectl get pvc 
kubectl get pv
```
```yaml
# edit ssd storageclass
parameters:
  type: pd-ssd
provisioner: kubernetes.io/gce-pd
reclaimPolicy: Retain
volumeBindingMode: Immediate
```


