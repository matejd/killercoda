<br>

Now we'll demonstrate how to collect custom application metrics.

Install [cartservice](https://gitlab.com/solve-x-kubernetes/cartservice) Deployment and Service:

```plain
kubectl apply -f /root/deployment.yaml
kubectl apply -f /root/service.yaml
```{{exec}}

Wait for pod to get ready:

```plain
kubectl get pods -l app=cartservice -w
```{{exec}}

Now create a **ServiceMonitor** to register your metrics:

```plain
kubectl apply -f - <<EOF
apiVersion: monitoring.coreos.com/v1
kind: ServiceMonitor
metadata:
  name: cartservice
  labels:
    app: cartservice
    release: kube-prometheus-stack
spec:
  selector:
    matchLabels:
      app: cartservice
  endpoints:
  - port: web
EOF
```{{exec}}

Prometheus operator will notice this new object
and re-generate the Prometheus configuration.

Access service at [link]({{TRAFFIC_HOST1_32080}}/AddProductsToCart)
to create some traffic (and metrics).
