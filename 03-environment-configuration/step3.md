
<br>

Now update StatefulSet to use a Secret:

```plain
kubectl create secret generic app-secrets \
    --from-literal=Redis__Host=secret_redis:6666 \
    --from-literal=Redis__Password=MySecretPassword'

kubectl apply -f /root/statefulset_secret.yaml
```{{exec}}

Wait for pods to rollout:

```plain
kubectl get pods -w
```{{exec}}

Observe changes at [link]({{TRAFFIC_HOST1_32080}}).
