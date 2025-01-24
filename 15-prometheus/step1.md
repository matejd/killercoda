<br>

Let's deploy kube-prometheus-stack. This includes:

- Prometheus Operator
- Prometheus instance
- Alertmanager instance
- Prometheus node-exporter
- Prometheus blackbox-exporter
- Prometheus Adapter for Kubernetes Metrics APIs
- kube-state-metrics
- Grafana

```plain
helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
helm repo update

helm install kube-prometheus-stack prometheus-community/kube-prometheus-stack
```{{exec}}

Port-forward Grafana:

```plain
kubectl port-forward svc/kube-prometheus-stack-grafana 31000:80 --address 0.0.0.0
```{{exec}}

and visit [link]({{TRAFFIC_HOST1_31000}}).
