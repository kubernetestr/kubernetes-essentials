#### Headless Service
```bash
kubectl apply -f cassandra-statefulset.yaml
kubectl apply -f cassandra-svc.yaml 
kubectl get endpoints
kubectl run --image=raesene/alpine-nettools nettools --restart=Never 
kubectl exec -it nettools -- /bin/sh
curl -XGET http://cassandra-0.cassandra.default.svc.cluster.local:9042

```

####cleanup
```bash
kubectl delete -f cassandra-svc.yaml
kubectl delete -f cassandra-statefulset.yaml
kubectl delete pod nettools
```
