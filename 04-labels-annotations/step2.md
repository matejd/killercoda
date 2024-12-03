
<br>

Find pods by labels:

```plain
kubectl get pods -lapp.kubernetes.io/name=aspnetapp,app.kubernetes.io/instance=aspnetapp-labels-demo
```{{exec}}

List all resources by labels:

```plain
kubectl get all -lapp.kubernetes.io/name=aspnetapp,app.kubernetes.io/instance=aspnetapp-labels-demo
```{{exec}}

Inspect labels and annotations:

```plain
kubectl describe pod aspnetapp-0
```{{exec}}
