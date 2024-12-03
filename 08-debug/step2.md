
<br>

Exec doesn't work in a chiseled container:

```plain
export POD_NAME=$(kubectl get pod -l app=aspnetapp -o jsonpath="{.items[0].metadata.name}")
```{{exec}}

```plain
kubectl exec -it $POD_NAME -- sh
```{{exec}}

```plain
Defaulted container "aspnetapp" out of: aspnetapp, debugger-wcdl4 (ephem), debugger-t6x8s (ephem)
error: Internal error occurred: Internal error occurred: error executing command in container: failed to exec in container: failed to start exec "8691879a2f0fece5197038e7612fe008a09e2343a260d21a7e0b905993741ffe": OCI runtime exec failed: exec failed: unable to start container process: exec: "sh": executable file not found in $PATH: unknow
```

`kubectl debug` creates an ephemeral container with shared resources:

```plain
kubectl debug -it $POD_NAME --image=busybox:1.28 --target=aspnetapp
```{{exec}}

Inspect running processes:

```plain
ps aux
```{{exec}}

Additional steps are needed to access container's filesystem:

```plain
addgroup -g 1654 debug
adduser -HD -u 1654 -G debug debug
su debug
```{{exec}}

```plain
cd /proc/1/root/app

ls -lah
```{{exec}}

