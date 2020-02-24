---
title: Kubernetes quick answers
---


## Create a plain password

Create a secret and be able to update in a easy way

```shell
kubectl create secret generic mariadb 
	--from-literal=root-password={password}
	--dry-run -o yaml | kubectl apply -f -
```

Can be used in deployment configuration

```yaml
env:
  - name: MYSQL_ROOT_PASSWORD
    valueFrom:
      secretKeyRef:
        name: mariadb
        key: root-password

```

## Create a configmap

```shell
kubectl create configmap mariadb-my.cnf --from-file=my.cnf
```
