### gce pd
#### Bad practice
```bash
gcloud compute disks create meetup-disk --size 1g --zone europe-west3-c
kubectl apply -f  01-gce-pd.yaml
kubectl describe pod test-pd
kubectl exec -it test-pd  -- /bin/sh
echo k8s > /cache/data.txt
kubectl delete pod test-pd
kubectl apply -f 01-gce-pd.yaml 
kubectl exec -it test-pd  -- /bin/sh
cat /cache/data.txt

#Remote Storage Lifecycle
mount | grep cache
exit
gcloud compute --project "inspired-bus-194216" ssh --zone "europe-west3-c" $(kubectl get pods test-pd -o jsonpath="{.spec.nodeName}")
mount | grep meetup-disk
kubectl delete pod test-pd
```

### rtfm
```bash
kubectl apply -f 01-2-gce-pd.yaml 
kubectl scale deployment test-pd --replicas=2
kubectl apply -f 01-3-gce-pd.yaml
kubectl scale deployment test-pd --replicas 2
kubectl delete -f 01-2-gce-pd.yaml 
```

### nfs server
```bash
gcloud beta compute --project=inspired-bus-194216 instances create nfsserver --zone=europe-west3-c --machine-type=n1-standard-2 --subnet=default --network-tier=PREMIUM --maintenance-policy=MIGRATE --service-account=249941509274-compute@developer.gserviceaccount.com --scopes=https://www.googleapis.com/auth/devstorage.read_only,https://www.googleapis.com/auth/logging.write,https://www.googleapis.com/auth/monitoring.write,https://www.googleapis.com/auth/servicecontrol,https://www.googleapis.com/auth/service.management.readonly,https://www.googleapis.com/auth/trace.append --image=ubuntu-1804-bionic-v20181003 --image-project=ubuntu-os-cloud --boot-disk-size=20GB --boot-disk-type=pd-standard --boot-disk-device-name=nfsserver


gcloud compute --project "inspired-bus-194216" ssh --zone "europe-west3-c" "nfsserver"
sudo su -
apt install nfs-kernel-server
mkdir /nfsdata
echo /nfsdata                10.0.0.0/8(rw,sync,no_subtree_check) > /etc/exports
sudo chown nobody:nogroup /nfsdata/
systemctl restart nfs-server
exit
exit


kubectl apply -f 02-nfs-pd.yaml
kubectl scale deployment test-pd --replicas=2
kubectl exec -it <first pod> -- /bin/sh
cd /cache
touch a.txt
exit
kubectl exec -it <second pod> -- /bin/sh
ls -lart /cache
exit
kubectl delete deployment test-pd

```




