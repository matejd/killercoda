
<br>

List all pods:

```plain
kubectl get pods
```{{exec}}

Install Deployment and Service:

```plain
kubectl apply -f /root/deployment.yaml
kubectl apply -f /root/service.yaml
```{{exec}}

Access service at [link]({{TRAFFIC_HOST1_32080}}).
