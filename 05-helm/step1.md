
<br>

Deploy a Postgres instance:

```plain
helm install aspnetapp oci://registry-1.docker.io/bitnamicharts/postgresql
```{{exec}}

Read command output. Inspect created resources.

```plain
kubectl get all
```{{exec}}

```plain
kubectl get pvc
```{{exec}}

```plain
kubectl get pv
```{{exec}}

Get generated Postgres password and store it in an environment variable:

```plain
export POSTGRES_PASSWORD=$(kubectl get secret --namespace default aspnetapp-postgresql -o jsonpath="{.data.postgres-password}" | base64 -d)
```{{exec}}

Connect to Postgres with command line client (in a new container):

```plain
kubectl run aspnetapp-postgresql-client --rm --tty -i --restart='Never' \
  --namespace default \
  --image docker.io/bitnami/postgresql:17.2.0-debian-12-r1 \
  --env="PGPASSWORD=$POSTGRES_PASSWORD" \
  --command -- psql --host aspnetapp-postgresql -U postgres -d postgres -p 5432
```{{exec}}
