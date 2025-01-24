<br>

Let's deploy kube-prometheus-stack Helm chart. This includes:

- **Prometheus operator** for spinning up and managing Prometheus instances
- **Prometheus instance**
- **Grafana** for visualizing metrics and plot data using dashboards
- **Alertmanager** for configuring various notifications (Slack, email, etc)
  based on various alerts received from the Prometheus
- **node-exporter** providing OS metrics
- **kube-state-metrics** providing metrics based on Kubernetes objects

```plain
helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
helm repo update

helm install kube-prometheus-stack prometheus-community/kube-prometheus-stack
```{{exec}}

Watch pods get created:

```plain
kubectl get pods -w
```{{exec}}

```
NAME                                                        READY   STATUS    RESTARTS   AGE
alertmanager-kube-prometheus-stack-alertmanager-0           2/2     Running   0          86s
kube-prometheus-stack-grafana-749ddbf894-6jcrz              3/3     Running   0          110s
kube-prometheus-stack-kube-state-metrics-55cd9669cd-brhcg   1/1     Running   0          110s
kube-prometheus-stack-operator-87b5f75c7-29grd              1/1     Running   0          110s
kube-prometheus-stack-prometheus-node-exporter-wp4x2        1/1     Running   0          110s
prometheus-kube-prometheus-stack-prometheus-0               2/2     Running   0          84s
```

Port-forward Grafana:

```plain
kubectl port-forward svc/kube-prometheus-stack-grafana 31000:80 --address 0.0.0.0
```{{exec}}

and visit [this link]({{TRAFFIC_HOST1_31000}}).

(username `admin`, password `prom-operator`)
