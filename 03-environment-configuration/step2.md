
<br>

Now update StatefulSet to use a ConfigMap:

```plain
kubectl apply -f /root/configmap.yaml
kubectl apply -f /root/statefulset_configmap.yaml
```{{exec}}

Wait for pods to rollout:

```plain
kubectl get pods -w
```{{exec}}

Observe changes at [link]({{TRAFFIC_HOST1_32080}}).
