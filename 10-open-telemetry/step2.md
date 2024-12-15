
<br>

Make a few requests to the example app at [link]({{TRAFFIC_HOST1_32080}}).

Then access Jaeger to inspect traces:

```plain
export POD_NAME=$(k get pods -l "app.kubernetes.io/instance=jaeger" -o jsonpath="{.items[0].metadata.name}")

kubectl port-forward --address 0.0.0.0 $POD_NAME 16686:16686
```{{exec}}

Access Jaeger at [link]({{TRAFFIC_HOST1_16686}}).
