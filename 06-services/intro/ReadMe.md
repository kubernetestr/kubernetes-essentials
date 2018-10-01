### Kubernetes Networking

#### 3-Tier

Pod to Pod communication happens without NAT
All Nodes communicate each other without NAT
```bash
ip addr
brctl show
docker ps
docker inspect <INSTANCEID>
docker inspect 3ed6c7b2c4a5 -f '{{.NetworkSettings.IPAddress}}'
docker ps | awk '{print $1}'
for i in $(docker ps | awk '{print $1}'); do docker inspect 3ed6c7b2c4a5 -f '{{.NetworkSettings.IPAddress}}' $1; done;
route show
```
https://github.com/acedemand/kubernetes-cluster


### CNI
Layer2 Switching
layer3 Routing
overlay networking

```bash
ps -ef | grep cni
kubectl get svc -o wide -n kube-system | grep 10.19.240.10
```


```bash
#service types
kubectl apply -f kuard-pod.yaml
kubectl get pod -w
kubectl expose pod kuard --type=ClusterIP --dry-run=true -o yaml
kubectl expose pod kuard --type=ClusterIP  -o yaml > kuard-pod-svc.yaml
kubectl delete svc kuard
kubectl expose pod kuard --type=NodePort --dry-run=true -o yaml > kuard-pod-svc-np.yaml
kubectl expose pod kuard --type=LoadBalancer --dry-run=true -o yaml > kuard-pod-svc-lb.yaml

#no endpoint
kubectl apply -f kuard-pod-svc.yaml 
kubectl get endpoints
kubectl delete pod kuard
kubectl get endpoints

kubectl apply -f kuard-deployment.yaml
kubectl get endpoints 
#edit svc kuard
kubectl edit svc kuard
kubectl get endpoints

```

#### NodePort
```bash
kubectl delete svc kuard
kubectl apply -f kuard-dpl-svc.yaml
kubectl get endpoints
kubectl scale deployment kuard --replicas=2
kubectl get endpoints -w

```
```yaml
  ports:
  - nodePort: 30792
    port: 8080
    protocol: TCP
    targetPort: 8080
```
