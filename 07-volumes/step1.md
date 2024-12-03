
<br>

Verify that no PersistentVolumes (PV) exist:

```plain
k get pv
```{{exec}}

Create a PersistentVolumeClaim (PVC) for logs:

```plain
kubectl apply -f /root/pvc.yaml
```{{exec}}

Create a Deployment that mount the PVC:

```plain
kubectl apply -f /root/deployment.yaml
```{{exec}}

Wait for pods to get ready:

```plain
kubectl get pods -w
```{{exec}}

Inspect resources:

```plain
k get pod,pv,pvc
```{{exec}}
