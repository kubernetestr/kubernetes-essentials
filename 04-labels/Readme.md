kubectl apply -f 1_kuard.yaml </br>
kubectl get pods --show-labels </br>
kubectl get pods -l appVersion=0.0.1 </br>
kubectl get pods -l appVersion=1.0.0 </br>
kubectl get pods --all-namespaces -l appVersion!=1.0.0,app=prometheus </br>
kubectl get pods --all-namespaces -l "k8s-app in(heapster,kube-state-metrics)" </br>
kubectl get pods --all-namespaces -l "k8s-app notin(heapster,kube-state-metrics)" </br>
kubectl get pods --all-namespaces -l "k8s-app,k8s-app notin(heapster,kube-state-metrics)" </br>
kubectl get pods --field-selector=status.phase!=Running --all-namespaces </br>
kubectl get pods -o json | jq  ".items[].status.containerStatuses[].name" </br>
kubectl port-forward $(kubectl get pods -o jsonpath={.items[0].metadata.name}) 8080:8080 </br>
kubectl port-forward $(kubectl get pod — selector=weave-scope-component=app -o jsonpath={.items..metadata.name}) 4040 </br>

#Modifying patch / labels / annotations when to restart 
kubectl label nodes gke-prometheus-demo-default-pool-f423e0de-knrv konu=meetup </br>
kubectl patch deployment kuard -p  '{"metadata": {"labels": {"version":"0.0.3"}}}' </br>
kubectl patch deployment kuard -p '"spec": {"template":{"metadata":{"labels":{"version":"2.0.0"}}}}' </br>
kubectl annotate deployment kuard durum=iyi </br>


