
<br>

Now we'll install Fluent Bit and configure
it to collect logs from all containers.
It'll send collected logs a webhook at [https://webhook.site](https://webhook.site).

First, edit `fluentbit_values.yaml` to use your own webhook id.

Install Fluent Bit:

```plain
helm repo add fluent https://fluent.github.io/helm-charts
```{{exec}}

```plain
helm upgrade --install fluent-bit fluent/fluent-bit \
  --values fluentbit_values.yaml
```{{exec}}

