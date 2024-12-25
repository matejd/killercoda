
<br>

Create resources:

```plain
kubectl apply -f /root/console.yaml
```{{exec}}

Wait for pod to get ready:

```plain
kubectl get pods -w
```{{exec}}

Finally, access OpenShift Console at [link]({{TRAFFIC_HOST1_32080}}).
