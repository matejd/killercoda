
<br>

Install Cert Manager operator:

```plain
kubectl apply -f https://github.com/cert-manager/cert-manager/releases/download/v1.16.2/cert-manager.yaml
```{{exec}}

Wait for Cert Manager to start:

```plain
kubectl get pods -n cert-manager -w
```{{exec}}

Install OpenTelemetry operator:

```plain
kubectl apply -f https://github.com/open-telemetry/opentelemetry-operator/releases/download/v0.114.1/opentelemetry-operator.yaml
```{{exec}}

Wait for OpenTelemetry to start:

```plain
kubectl get pods -n opentelemetry-operator-system -w
```{{exec}}

Install Jaeger:

```plain
helm repo add jaegertracing https://jaegertracing.github.io/helm-charts

helm install jaeger jaegertracing/jaeger --values jaeger-values.yaml
```{{exec}}

Create OpenTelemetry collector:

```plain
kubectl apply -f collector.yaml
```{{exec}}

Wait for collector to start:

```plain
kubectl get pods -w
```{{exec}}

Setup auto-instrumentation:

```plain
kubectl apply -f instrumentation.yaml
```{{exec}}

Finally, install the example app which will be auto-instrumented:

```plain
kubectl apply -f /root/deployment.yaml
kubectl apply -f /root/service.yaml
```{{exec}}
