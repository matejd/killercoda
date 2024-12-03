
<br>

Patch StatefulSet to update configuration:

```plain
kubectl apply -f /root/statefulset_json_logging.yaml
```{{exec}}

Wait for pods to get ready:

```plain
kubectl get pods -w
```{{exec}}
