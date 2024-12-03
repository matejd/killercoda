
<br>

Install Deployment and Service:

```plain
kubectl apply -f /root/deployment.yaml
kubectl apply -f /root/service.yaml
```{{exec}}

Wait for pod to get ready:

```plain
kubectl get pods -w
```{{exec}}

Finally, access service at [link]({{TRAFFIC_HOST1_32080}}).
