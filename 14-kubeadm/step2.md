<br>

Now let's inspect the environment to see what kubeadm did and how it all fits
together.

First, kubelet Kubernetes node agent is running as a systemd service:

```plain
systemctl status kubelet
```{{exec}}

(press q to close)

```plain
systemctl cat kubelet
```{{exec}}

kubeadm:

- executed preflight checks
- created folder `/etc/kubernetes`
- created folder `/etc/kubernetes/pki`
- created folder `/etc/kubernetes/manifests`
- generated a certificate authority and self-signed certificates for components
- created kubeconfig configuration files
- created static pod manifests for etcd, api-server, controller-manager and scheduler
- updated kubelet configuration (`/var/lib/kubelet`)
- restarted kubelet

kubelet then picked up the static pod manifests in `/etc/kubernetes/manifests`,
which specify Pods running on this specific Node only.

kubeadm further:

- generated bootstrap tokens
- created cluster-info ConfigMap
- and more

You can see that Kubernetes is itself running in containers
except for kubelet.

Inspect files in `/etc/kubernetes`:

```plain
apt-get install -y tree && tree /etc/kubernetes
```{{exec}}

Inspect all Pods:

```plain
export KUBECONFIG=/etc/kubernetes/admin.conf

kubectl get pods -A
```{{exec}}

This should print out something like the following:

```
NAMESPACE     NAME                                       READY   STATUS    RESTARTS   AGE
kube-system   calico-kube-controllers-6879d4fcdc-6krhb   1/1     Running   0          12m
kube-system   calico-node-ngb29                          1/1     Running   0          12m
kube-system   coredns-7c65d6cfc9-m8thj                   0/1     Pending   0          13m
kube-system   coredns-7c65d6cfc9-zcvgr                   1/1     Running   0          13m
kube-system   etcd-ubuntu                                1/1     Running   0          13m
kube-system   kube-apiserver-ubuntu                      1/1     Running   0          13m
kube-system   kube-controller-manager-ubuntu             1/1     Running   0          13m
kube-system   kube-proxy-vllxd                           1/1     Running   0          13m
kube-system   kube-scheduler-ubuntu                      1/1     Running   0          13m
```

TODO:

- Calico
- API Server audit logs
