# Kubernetes Gateway API

## Simple external HTTP Gateway

### Create a GKE cluster and enable `gateway-api`

```sh
gcloud container  clusters create "my-cluster" \
    --zone "europe-west1-c" \
    --no-enable-basic-auth \
    --gateway-api=standard \
    --num-nodes "1"
```

### Apply the manifests

```sh
kubectl apply -f ./ext-http-gateway
```

### Wait a few minutes until the gateway gets a public IP

```sh
kubectl get gateway --namespace infra --watch
```

### Testing

```sh
curl -H "host: app1.domain.com" XXX.XXX.XXX.XXX
```

```sh
curl -H "host: my.domain.com" -H "app: app1" 34.111.73.217
```

```sh
curl -H "host: my.domain.com" 34.111.73.217/app1
```
