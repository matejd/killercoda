<br>

Let's enable Kubernetes [audit logging](https://kubernetes.io/docs/tasks/debug/debug-cluster/audit/).

To enable Kubernetes audit logging, we need to change the arguments
to the kube-apiserver to add `--audit-policy-file` and
`--audit-log-path` arguments and provide file that
sets an audit policy configuration.

```plain
cat <<EOT >> /etc/kubernetes/pki/audit-policy.yaml
apiVersion: audit.k8s.io/v1
kind: Policy
rules:
# Log pod changes at RequestResponse level
- level: RequestResponse
  resources:
   - group: ""
     resources: ["pods"]
# Log everything else at Metadata level
- level: Metadata

EOT
```{{exec}}

Modify kube-apiserver static pod configuration file:

```plain
sed -i '16i\    - --audit-policy-file=/etc/kubernetes/pki/audit-policy.yaml' /etc/kubernetes/manifests/kube-apiserver.yaml

sed -i '17i\    - --audit-log-path=/tmp/audit.log' /etc/kubernetes/manifests/kube-apiserver.yaml
```{{exec}}

Now wait a few seconds for kubelet to restart the modified pod.

```plain
export KUBECONFIG=/etc/kubernetes/admin.conf

kubectl get pods --all-namespaces
```{{exec}}
