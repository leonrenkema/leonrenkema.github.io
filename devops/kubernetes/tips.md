

## Create secret from a plain password

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

## Create secret from a TLS certificate

```shell
kubectl create secret tls tls-name-ingress
  --cert=tls.crt
  --key=tls.key
```

## Create a configmap

Create a file with the name `my.cnf` and create a configmap with the following command.

```shell
kubectl create configmap mariadb-my.cnf --from-file=my.cnf
```

The configmap can be edited with the following command

```shell
kubectl edit configmap mariadb-my.cnf
```

```yaml
containers:
  - name: database
    volumeMounts:
    - name: mariadb-configmap
      mountPath: /etc/mysql
   volumes:
   - name: mariadb-configmap
      configMap:
        name: mariadb-my.cnf
```
## Start random pod

Start any image and obtain a shell

```shell
 kubectl run -i --tty busybox --image=busybox --restart=Never -- sh  
```
