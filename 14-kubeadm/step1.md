<br>

kubeadm is an official tool for bootstraping Kubernetes clusters. In this
tutorial we'll use it to create a single-node Kubernetes cluster, meaning a
single machine will run both the control plane and the actual workloads. This is
not a production setup.

kubeadm configures the following components:

- etcd
- kube-apiserver
- kube-controller-manager
- kube-scheduler
- kube-proxy

This killercoda environment is running Ubuntu with the following already
installed:

- Docker (try `docker run hello-world`)
- containerd (see `systemctl status containerd`)

so we'll skip installing containerd (Kubernetes needs a container runtime).

Besides kubeadm we'll need to install:

- kubelet: the Kubernetes node agent,
- kubectl: the command line util to access the Kubernetes API Server,

Let's test that Kubernetes is not installed yet, the following directory does
not exist yet:

```plain
ls /etc/kubernetes/
```{{exec}}

First, install kubelet, kubeadm and kubectl from Kubernetes repositories:

```plain
apt-get install -y apt-transport-https ca-certificates curl gpg
mkdir -p -m 755 /etc/apt/keyrings
curl -fsSL https://pkgs.k8s.io/core:/stable:/v1.31/deb/Release.key | gpg --dearmor -o /etc/apt/keyrings/kubernetes-apt-keyring.gpg
echo 'deb [signed-by=/etc/apt/keyrings/kubernetes-apt-keyring.gpg] https://pkgs.k8s.io/core:/stable:/v1.31/deb/ /' | tee /etc/apt/sources.list.d/kubernetes.list
apt-get update
apt-get install -y kubelet=1.31.5-1.1 kubectl=1.31.5-1.1 kubeadm=1.31.5-1.1
```{{exec}}

Disable swap, kubelet will not run with swap enabled:

```plain
swapoff -a
```{{exec}}

Now initialize the control plane components:

```plain
kubeadm init \
  --kubernetes-version=1.31.0 \
  --pod-network-cidr 192.168.0.0/16 \
  --ignore-preflight-errors=NumCPU \
  --ignore-preflight-errors=Mem
```{{exec}}

Untaint the single node so that it's able to run normal workloads. Also, install
Calico CNI.

```plain
export KUBECONFIG=/etc/kubernetes/admin.conf

kubectl get nodes
```{{exec}}

```plain
kubectl taint nodes --all node-role.kubernetes.io/control-plane-

kubectl apply -f https://docs.projectcalico.org/manifests/calico.yaml

kubectl get pods -n kube-system -w
```{{exec}}

```plain
kubectl get nodes
```
