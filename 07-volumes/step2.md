
<br>

Copy logs from PVC to local file system:

```plain
export POD_NAME=$(kubectl get pod -l app=aspnetapp -o jsonpath="{.items[0].metadata.name}")

mkdir Logs
```{{exec}}

```plain
kubectl cp $POD_NAME:/app/Logs ./Logs
```{{exec}}

```plain
ls -lah Logs
```{{exec}}
