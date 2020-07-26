
# postgresql-k8s



https://chartcenter.io/bitnami/postgresql


The following commands will install PostgreSQL on Kubernetes. 
```
helm repo add bitnami https://charts.bitnami.com/bitnami
helm install postgresql --set persistence.storageClass=rook-cephfs bitnami/postgresql
```

Note: I've set a custom `persistence.storageClass` to `rook-cephfs`.