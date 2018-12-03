#### Installation
```bash
kubectl create serviceaccount --namespace kube-system tiller
kubectl create clusterrolebinding tiller-cluster-rule --clusterrole=cluster-admin --serviceaccount=kube-system:tiller
helm init --service-account tiller --upgrade
kubectl get deployment -n kube-system -o yaml tiller-deploy | grep serviceAccount
```

#### Helm uninstall from cluster
```bash
helm reset
kubectl get pods -n kube-system
```

#### Forget to create service account

```bash
#https://github.com/fnproject/fn-helm/issues/21
helm init
helm list
kubectl create serviceaccount --namespace kube-system tiller
kubectl create clusterrolebinding tiller-cluster-rule --clusterrole=cluster-admin --serviceaccount=kube-system:tiller
kubectl patch deploy --namespace kube-system tiller-deploy -p '{"spec":{"template":{"spec":{"serviceAccount":"tiller"}}}}'
helm --help
helm list --help
helm list
helm list -a
```

#### Stable Charts && Incubator Charts
```bash
helm search mysql
helm repo add incubator https://kubernetes-charts-incubator.storage.googleapis.com/
helm search cassandra
curl -XGET https://kubernetes-charts-incubator.storage.googleapis.com/
```

open from Chrome https://console.cloud.google.com/storage/browser/kubernetes-charts-incubator </br>

```bash
helm install stable/nginx-ingress --name nginx-ing --namespace app
kubectl get all -n app
helm list
helm delete --help
helm delete nginx-ing --purge
```

### Managing dependencies
```bash
mkdir -p $HOME/dev/tools_data
cd ~/dev/tools_data
git clonehttps://github.com/helm/charts.git 
cd charts/stable
cd sonarqube
cat requirements.yaml
mkdir charts/postgresql
cp -R ../postgresql charts/postgresql
helm install . --name sonarqube --namespace app -f values.yaml
helm list
```

#### Helm Commands
```bash
helm status sonarqube
helm inspect .
helm inspect stable/mysql
```
change limits in values.yaml </br>
```yaml
resources:
  limits:
    cpu: 100m
    memory: 128Mi
  requests:
    cpu: 100m
    memory: 128Mi
```
```bash
helm upgrade sonarqube .  -f values.yaml 
helm history sonarqube
helm rollback --dry-run=true sonarqube 1
helm rollback sonarqube 1
kubectl get pods -n app
```

