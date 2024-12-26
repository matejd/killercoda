
<br>

Use Vault UI to enable and configure Kubernetes authentication,
KV secrets engine, a role and policy for Kubernetes,
and create a static secret.

Enable Kubernetes authentication:
- navigate to Access -> Enable new method -> Kubernetes
- use path _kubernetes_
- save
- use _https://kubernetes.default:443_ for Kubernetes host

From the main menu create a new ACL policy named _aspnetapp_:

```
path "secret/data/aspnetapp" {
   capabilities = ["read", "list"]
}
```

Now create a Kubernetes role:
- go back to Kubernetes authentication
- create a new role _aspnetapp_ with:
  * Bound service account names: _aspnetapp_
  * Bound service account namespaces: _default_
  * Generated Token's Policies: _aspnetapp_
  * Audience: _vault_

This role enables service account _aspnetapp_ to use
policy _aspnetapp_ which allows access to secrets
under a specific path in the KV secrets engine.

Finally, add secrets under _secret/aspnetapp_, e.g.:

```json
{
  "Redis__Password": "password123"
}
```

