<br>

Let's enable Kubernetes [audit logging](https://kubernetes.io/docs/tasks/debug/debug-cluster/audit/).

To enable Kubernetes audit logging, we need to change the arguments
to the kube-apiserver:

- `--audit-policy-file` specifies audit policy configuration
- `--audit-log-path` output file
- `--audit-webhook-config-file` audit webhook configuration

```plain
cat <<EOT >> /etc/kubernetes/pki/audit-policy.yaml
apiVersion: audit.k8s.io/v1
kind: Policy
rules:
# Log pod changes at Metadata level
- level: Metadata
  resources:
   - group: ""
     resources: ["pods"]
# Don't log anything else
- level: None

EOT
```{{exec}}

```plain
cat <<EOT >> /etc/kubernetes/pki/audit-webhook.yaml
apiVersion: v1
kind: Config
clusters:
- name: kube-auditing
  cluster:
    server: https://webhook.site/b002ff1f-8e0f-4473-981d-3a0bb04c7e0c
    insecure-skip-tls-verify: true
contexts:
- context:
    cluster: kube-auditing
    user: ""
  name: default-context
current-context: default-context
preferences: {}
users: []

EOT
```{{exec}}

Modify kube-apiserver static pod configuration file:

```plain
sed -i '16i\    - --audit-policy-file=/etc/kubernetes/pki/audit-policy.yaml' /etc/kubernetes/manifests/kube-apiserver.yaml

sed -i '17i\    - --audit-log-path=/tmp/audit.log' /etc/kubernetes/manifests/kube-apiserver.yaml

sed -i '18i\    - --audit-webhook-config-file=/etc/kubernetes/pki/audit-webhook.yaml' /etc/kubernetes/manifests/kube-apiserver.yaml
```{{exec}}

Now wait a few seconds for kubelet to restart the modified pod.

```plain
export KUBECONFIG=/etc/kubernetes/admin.conf

kubectl get pods --all-namespaces
```{{exec}}

See logs at <https://webhook.site/#!/view/b002ff1f-8e0f-4473-981d-3a0bb04c7e0c/72ee35e3-45ad-4256-8096-686b17f60759/1>.
