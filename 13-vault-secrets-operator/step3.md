
<br>

Use Helm to deploy the Vault Secrets Operator:

```plain
helm install vault-secrets-operator hashicorp/vault-secrets-operator -n vault-secrets-operator-system --create-namespace --values /root/vault-operator-values.yaml
```{{exec}}

Wait for the operator pod to get ready:

```plain
kubectl get pods -n vault-secrets-operator-system -w
```{{exec}}

Now deploy the _aspnetapp_ together with a Vault static secret:

```plain
kubectl apply -f /root/aspnetapp.yaml
```{{exec}}

Wait for the aspnetapp pod to get ready:

```plain
kubectl get pods -w
```{{exec}}

Finally, access aspnetapp at [link]({{TRAFFIC_HOST1_32080}}).
