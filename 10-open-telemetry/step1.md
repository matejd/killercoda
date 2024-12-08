
<br>

Install Cert Manager operator:

```plain
kubectl apply -f https://github.com/cert-manager/cert-manager/releases/download/v1.16.2/cert-manager.yaml
```{{exec}}

Install OpenTelemetry operator:

```plain
kubectl apply -f https://github.com/open-telemetry/opentelemetry-operator/releases/v0.114.1/download/opentelemetry-operator.yaml
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

Setup instrumentation:

```plain
kubectl apply -f instrumentation.yaml
```{{exec}}
