
<br>

Patch StatefulSet to update configuration:

```plain
kubectl apply -f /root/statefulset_json_logging.yaml
```{{exec}}

Wait for pods to get ready:

```plain
kubectl get pods -w
```{{exec}}

Install Fluent Bit:

```plain
helm repo add fluent https://fluent.github.io/helm-charts

helm upgrade --install fluent-bit fluent/fluent-bit
```{{exec}}

