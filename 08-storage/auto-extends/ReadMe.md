### Auto extend
https://kubernetes.io/blog/2018/07/12/resizing-persistent-volumes-using-kubernetes/
In Kubernetes v1.11 the persistent volume expansion feature is being promoted to beta. This feature allows users to easily resize an existing volume by editing the PersistentVolumeClaim (PVC) object. Users no longer have to manually interact with the storage backend or delete and recreate PV and PVC objects to increase the size of a volume. Shrinking persistent volumes is not supported.


