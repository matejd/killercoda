<br>

This is a note on how to access Killercoda Kubernetes
from a remote tool.

Use the following kubeconfig (update server address first!):

```
apiVersion: v1
clusters:
- cluster:
    # NOTE: replace this with your own URL
    server: https://86d69f6c-b318-4302-833a-da23b2f41e6b-10-244-8-248-8080.spch.r.killercoda.com:443
    insecure-skip-tls-verify: true
  name: killercoda
contexts:
- context:
    cluster: killercoda
    user: killercoda
  name: killercoda@killercoda
current-context: killercoda@killercoda
kind: Config
preferences: {}
users:
- name: killercoda
```

Then proxy the API server:

```plain
kubectl proxy --port=8080 --address=0.0.0.0 --accept-hosts='.*'
```{{exec}}
