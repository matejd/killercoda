
<br>

Fetch the certificate (public key) used for sealing secrets:

```plain
kubeseal --fetch-cert
```{{exec}}

Now create a SealedSecret using [WebSeal](https://socialgouv.github.io/webseal/).

Store it in `sealed-secret.yaml` and decrypt it:

```plain
kubectl apply -f sealed-secret.yaml
```{{exec}}

```plain
kubectl get secrets
```{{exec}}
