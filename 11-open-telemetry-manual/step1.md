
<br>

Install Deployment and Service:

```plain
kubectl apply -f /root/deployment.yaml
kubectl apply -f /root/service.yaml
```{{exec}}

Also install .NET Aspire dashboard in standalone mode:

```plain
kubectl apply -f /root/aspire.yaml
```{{exec}}

Wait for pods to get ready:

```plain
kubectl get pods -w
```{{exec}}

Access service at [link]({{TRAFFIC_HOST1_32080}}/AddProductsToCart).

Access Aspire dashboard at [link]({{TRAFFIC_HOST1_31888}}).

