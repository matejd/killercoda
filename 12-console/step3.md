<br>

Let's also install [Portainer](https://www.portainer.io).

```plain
helm repo add portainer https://portainer.github.io/k8s/
helm repo update
```{{exec}}

```plain
helm upgrade --install --create-namespace -n portainer portainer portainer/portainer \
    --set image.tag=2.21.5
```{{exec}}

Wait for pod to start:

```plain
kubectl get pods -n portainer -w
```{{exec}}

Then visit [this link]({{TRAFFIC_HOST1_30777}}).
