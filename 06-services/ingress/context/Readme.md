```bash
kubectl apply -f web-v1.yaml
kubectl apply -f web-v2.yaml
kubectl apply -f web-v1-svc.yaml
kubectl apply -f web-v2-svc.yaml

# Find the problem


#Fix the problem
kubectl apply -f web-v1-fixed.yaml
kubectl apply -f web-v2-fixed.yaml
kubectl get ingress web-ingress -o jsonpath="{.status.loadBalancer.ingress[*].ip}"
curl -XGET http://$(kubectl get ingress color-ingress -o jsonpath="{.status.loadBalancer.ingress[*].ip}")/v1/
curl -XGET http://$(kubectl get ingress color-ingress -o jsonpath="{.status.loadBalancer.ingress[*].ip}")/v2/
```


#### Enable HTTPS
```bash
openssl genrsa -out ca.key 2048
openssl req -x509 -new -nodes -key ca.key -subj \
  "/CN=$(kubectl get ingress color-ingress \
   -o jsonpath="{.status.loadBalancer.ingress[*].ip}")" -days 10000 -out ca.crt
kubectl create secret tls web-tls --key=ca.key --cert=ca.crt
kubectl apply -f ingress-tls.yaml
#watch for changes in gcp console
```
```yaml
apiVersion: extensions/v1beta1
kind: Ingress
metadata:
  name: web-ingress
  annotations:
    kubernetes.io/ingress.allow-http: "false"
spec:
```

```bash
#force https
kubectl apply -f ingress-tls-forcehttps.yaml
```
#### References
1- https://github.com/kubernetes/ingress-gce

