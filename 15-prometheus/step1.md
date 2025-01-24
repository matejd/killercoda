<br>

Let's deploy kube-prometheus-stack. This includes:

- **Prometheus Operator** for spinning up and managing Prometheus instances
- **Grafana** for visualizing metrics and plot data using dashboards
- **Alertmanager** for configuring various notifications (Slack, email, etc)
  based on various alerts received from the Prometheus

```plain
helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
helm repo update

helm install kube-prometheus-stack prometheus-community/kube-prometheus-stack
```{{exec}}

Port-forward Grafana:

```plain
kubectl port-forward svc/kube-prometheus-stack-grafana 31000:80 --address 0.0.0.0
```{{exec}}

and visit [this link]({{TRAFFIC_HOST1_31000}}).
