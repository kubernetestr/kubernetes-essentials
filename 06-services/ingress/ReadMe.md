### Ingress
#### Services
```bash
kubectl apply -f kuard-dpl-svc.yaml
kubectl apply -f kuard-deployment.yaml
kubectl get endpoints -w
kubectl apply -f kuard-ingress.yaml

#watch for changes
kubectl describe ingress kuard

#go to network loadbalancer section on gcp console
#look at probes / health status / ports

gcloud compute addresses create kuardstatic-ip --global
kubectl apply -f kuard-ingress-static.yaml

#go to static ip address section in gcp console
```
#### CleanUp
```bash
kubectl delete kuard-dpl-svc.yaml
kubectl delete -f kuard-dpl-svc.yaml
kubectl delete -f kuard-deployment.yaml
```

#### Context Bases Routing
```bash

```





