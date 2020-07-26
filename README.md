
# postgresql-k8s


## Install

The following commands will install PostgreSQL on Kubernetes with a release name of `postgresql` and a namespace of `db`: 
```bash
helm repo add bitnami https://charts.bitnami.com/bitnami
helm install postgresql --set persistence.storageClass=rook-cephfs bitnami/postgresql --create-namespace -n db
```
Note: I've set a custom `persistence.storageClass` to `rook-cephfs`.

Something like the following will be the response from the `install` command:
```bash
NAME: postgresql
LAST DEPLOYED: Sun Jul 26 15:06:32 2020
NAMESPACE: db
STATUS: deployed
REVISION: 1
TEST SUITE: None
NOTES:
** Please be patient while the chart is being deployed **

PostgreSQL can be accessed via port 5432 on the following DNS name from within your cluster:

    postgresql.db.svc.cluster.local - Read/Write connection

To get the password for "postgres" run:

    export POSTGRES_PASSWORD=$(kubectl get secret --namespace db postgresql -o jsonpath="{.data.postgresql-password}" | base64 --decode)

To connect to your database run the following command:

    kubectl run postgresql-client --rm --tty -i --restart='Never' --namespace db --image docker.io/bitnami/postgresql:11.8.0-debian-10-r61 --env="PGPASSWORD=$POSTGRES_PASSWORD" --command -- psql --host postgresql -U postgres -d postgres -p 5432



To connect to your database from outside the cluster execute the following commands:

    kubectl port-forward --namespace db svc/postgresql 5432:5432 &
    PGPASSWORD="$POSTGRES_PASSWORD" psql --host 127.0.0.1 -U postgres -d postgres -p 5432

```


## Uninstall

```bash
helm delete postgresql -n db
```


## Reference

* https://chartcenter.io/bitnami/postgresql