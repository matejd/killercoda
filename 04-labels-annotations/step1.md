
<br>

Create a demo StatefulSet and Service:

```plain
kubectl apply -f /root/statefulset.yaml
kubectl apply -f /root/service.yaml
```{{exec}}

Wait for pods to get ready:

```plain
kubectl get pods -w
```{{exec}}

Access service at [link]({{TRAFFIC_HOST1_32080}}).
