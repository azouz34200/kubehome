# README

### Storage class
Localpath provisionner
```bash
kubectl apply -f localpath-persistant.yaml
kubectl get storageclass
```

### Dasboard kubernetes UI

```bash
kubectl apply -f dashboard/dashboard-admin.yml
kubectl apply -f https://raw.githubusercontent.com/kubernetes/dashboard/master/aio/deploy/recommended/kubernetes-dashboard.yaml
k apply -f dashboard/ingress-dasboard.yml -n kube-system
```

### Get Token

```bash
kubectl -n kube-system describe secret $(kubectl -n kube-system get secret | grep admin-user | awk '{print $1}')
```

### Heml

```bash
kubectl -n kube-system create serviceaccount tiller
kubectl create clusterrolebinding tiller --clusterrole cluster-admin --serviceaccount=kube-system:tiller
helm init --service-account tiller --upgrade
```

### Label node

```bash
k label node node01.lan kubernetes.io/role=infra
k label node node02.lan kubernetes.io/role=app
k label node master.lan kubernetes.io/role=router
```

### Traefik

```bash
helm install stable/traefik --name traefik -f traefik-value.yaml --namespace traefik
```

### Registry

#### Generate user and password

```bash
docker run --entrypoint htpasswd registry:2 -Bbn mickael "password > ./httpasswd
```

#### Deploy

```bash
helm install --name registry stable/docker-registry -f docker-registry-value.yaml -n registr
```

#### Install

```bash
helm install stable/nfs-client-provisioner --name nfs-client --namespace nfs-client -f nfs-client-values.yaml
```

#### Ugrade

```bash
helm upgrade nfs-client stable/nfs-client-provisioner -f nfs-client-values.yaml  
```bash
