
### EmptyDir 
```bash
vim 01-2-emptydir-pod.yaml
kubectl apply -f 01-2-emptydir-pod.yaml
kubectl port-forward test-pd 8080:80
curl -XGET http://localhost:8080/helloworld/helloworld.html
kubectl delete -f 01-2-emptydir-pod.yaml
```

### Bad Practice
```bash
kubectl apply -f 01-3-emptydir-pod.yaml
kubectl port-forward test-pd 8080:80
curl -XGET http://localhost:8080/helloworld/helloworld.html
kubectl delete -f 01-3-emptydir-pod.yaml
```

### Secret Volume
```bash
echo mysql://root:topsecretpassword@remote_mysql:3306/acedemand > mysql.conn
kubectl create secret generic mysqlconnection --from-file=mysql.conn
kubectl apply -f 03-secretdir.yaml
kubectl exec -it test-pd  -- /bin/sh
ls /secret
cat /secret/mysql.conn
```

### configmap readonly
```bash
kubectl create configmap mysql-conn --from-file mysql.conn
kubectl apply -f 01-4-emptydir-pod.yaml
kubectl exec -it test-pd -- /bin/sh
cd /usr/share/nginx/html
ls -lart
# find executable rights
kubectl delete configmap mysql-conn
kubectl delete -f 01-4-emptydir-pod.yaml
```





