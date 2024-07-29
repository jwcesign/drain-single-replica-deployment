# drain-single-replica-deployment

A demo to test the stability of draining a single replica's deployment.

## Init env

```
kind create cluster --config cluster-config.yaml
kubectl apply -f hey-pod.yaml
kubectl apply -f nginx.yaml
```

## Drain a node

```
kubectl drain  kind-worker3  --ignore-daemonsets  --delete-emptydir-data --force
```

## Rollout deployment


```
kubectl rollout restart deployment/nginx
```

## Run hey test


Run following command with the up different command, you can see different failure rate.
```
kubectl exec hey -- /hey -t 3 -n 100 -c 1 -q 3 http://nginx.default
```
