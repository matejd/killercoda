
<br>

Create a demo StatefulSet and Service:

```plain
kubectl apply -f /root/statefulset.yaml
kubectl apply -f /root/service.yaml
```{{exec}}

Wait for pod to get ready:

```plain
kubectl get pods -w
```{{exec}}

Access service at [link]({{TRAFFIC_HOST1_32080}}).

Observe that `Redis host` setting changed based on the value in environment
variable.
