
<br>

First, deploy Vault using Helm:

```plain
helm repo add hashicorp https://helm.releases.hashicorp.com
helm repo update

helm install vault hashicorp/vault -n vault --create-namespace --values /root/vault-values.yaml
```{{exec}}

Wait for the Vault pod to get ready:

```plain
kubectl wait --for=condition=Ready -n vault pod/vault-0
```{{exec}}

Port-forward and access Vault UI:

```plain
kubectl port-forward --address 0.0.0.0 -n vault svc/vault-ui 8200:8200
```{{exec}}

Open [Vault UI]({{TRAFFIC_HOST1_8200}}).
