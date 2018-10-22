#### More PVs
```bash
gcloud compute disks create meetup-disk-2 --size 1g --zone europe-west3-c
kubectl apply -f 01-gcpd-pv-pvc.yaml 
kubectl get pv
kubectl get pvc
kubectl delete -f 01-gcpd-pv-pvc.yaml
kubectl apply -f 02-gcpd-pv-pvc.yaml
kubectl get pv
kubectl get pvc
```
