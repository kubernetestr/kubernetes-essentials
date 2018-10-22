### Persistent Volume and Persistent Volume Claim
```bash
kubectl apply -f 01-nfs-pv-pvc.yaml
kubectl get pv
kubectl get pvc
kubectl apply -f 01-nfs-dp.yaml 
kubectl scale deployment test-pd --replicas=2
kubectl delete -f 01-nfs-dp.yaml
```

#### Little change move to gcp
```bash
kubectl apply -f 02-gcpd-pv-pvc.yaml
kubectl apply -f 01-nfs-dp.yaml
kubectl get pods
kubectl delete -f 01-nfs-dp.yaml
```


