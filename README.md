# postgres-on-kind

## Steps to deploy a Kind cluster

```sh
kind create cluster --config=kind.yaml 
```

## Steps to deploy Postgres database in the Kind cluster

### step 1: create namespace

```sh
kubectl apply -f ns.yaml
```

### step 2: create configmap

```sh
kubectl apply -f cm.yaml
```

### step 3: create persistent volume

```sh
kubectl apply -f pv.yaml
```

### step 3: create persistent volume claim

```sh
kubectl apply -f pvc.yaml
```

### step 4: create deployment

```sh
kubectl apply -f deploy.yaml
```

### step 5: create service

```sh
kubectl apply -f svc.yaml
```

### step 6: exec into postgres pod

```sh
kubectl exec -it -n postgres $(kubectl get pods -n postgres -l app=postgres --output jsonpath='{.items[0].metadata.name}') --  psql -h localhost -U admin --password -p 5432 postgresdb
```

**Note:** Refer https://phoenixnap.com/kb/postgresql-kubernetes for more details

### Important points
- Use `\q` to exit from psql shell

## Steps to deploy pgadmin tool in the Ubuntu

```sh
sudo curl https://www.pgadmin.org/static/packages_pgadmin_org.pub | sudo apt-key add
```

```sh
sudo sh -c 'echo "deb https://ftp.postgresql.org/pub/pgadmin/pgadmin4/apt/$(lsb_release -cs) pgadmin4 main" > /etc/apt/sources.list.d/pgadmin4.list && apt update'
```

```sh
sudo apt install pgadmin4
```

**Note:** Refer https://www.commandprompt.com/education/how-to-install-pgadmin-on-ubuntu/ for more details

