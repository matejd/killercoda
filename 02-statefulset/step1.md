
<br>

Install StatefulSet and Service:

```plain
kubectl apply -f /root/statefulset.yaml
kubectl apply -f /root/service.yaml
```{{exec}}

Wait for pod to get ready:

```plain
kubectl get pods
```{{exec}}

Finally, access service at [link]({{TRAFFIC_HOST1_32080}}).
