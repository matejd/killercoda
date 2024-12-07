
<br>

Bitnami Sealed Secrets allows you to safely store
secrets in git repositories, even public ones.

You encrypt your secret into a `SealedSecret` custom resource,
which can be decrypted only by the Sealed Secrets operator
running in the target cluster. Let's see an example.

First, install the operator using a YAML file:

```plain
kubectl apply -f https://github.com/bitnami-labs/sealed-secrets/releases/download/v0.27.3/controller.yaml
```{{exec}}

Also install the CLI tool:

```plain
curl -OL "https://github.com/bitnami-labs/sealed-secrets/releases/download/v0.27.3/kubeseal-0.27.3-linux-amd64.tar.gz"
tar -xvzf kubeseal-0.27.3-linux-amd64.tar.gz kubeseal
sudo install -m 755 kubeseal /usr/local/bin/kubeseal
```{{exec}}

Inspect resources:

```plain
kubectl get all --all-namespaces
```{{exec}}
