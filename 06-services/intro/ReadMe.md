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
