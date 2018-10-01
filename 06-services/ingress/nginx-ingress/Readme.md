#### Nginx Ingress
```bash
helm install --name nginx-ingress stable/nginx-ingress --set rbac.create=true
kubectl get pods
kubectl get svc

openssl genrsa -out ca.key 2048
openssl req -x509 -new -nodes -key ca.key -subj \
   "/CN=$(kubectl get ingress color-ingress \
    -o jsonpath="{.status.loadBalancer.ingress[*].ip}")" -days 10000 -out ca.crt


kubectl create secret tls web-tls --key=ca.key --cert=ca.crt
kubectl apply -f web-v2-fixed.yaml
kubectl apply -f web-v1-fixed.yaml
kubectl apply -f web-v1-svc.yaml
kubectl apply -f web-v2-svc.yaml

curl -k -XGET https://$(kubectl get svc  nginx-ingress-controller \
   -o jsonpath="{.status.loadBalancer.ingress[*].ip}")/v1/

curl -k -XGET https://$(kubectl get svc  nginx-ingress-controller \
   -o jsonpath="{.status.loadBalancer.ingress[*].ip}")/v2/


```
#### TODO
Fix the certificate error

