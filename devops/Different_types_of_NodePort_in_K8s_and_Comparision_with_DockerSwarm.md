## NodePort
  Exposes the service on each Node’s IP. Accessing as `<NodeIP>:<NodePort>`. Lets say we have 10 Nodes and our svc points to 3 pods. Even if we hit a Node in which the pod is not running, we will be able to get the result. K8s will take care of that i.e it will internally sent to the node in which the pod is running.

When are creating `NodePort` service(svc), we can specify `externalTrafficPolicy` as Local or Cluster

- Cluster(Default) - As explain above, svc is reacable in all Nodes.
- Local - Route traffic locally. svc is reacable only in Nodes in which Pods are running.

## Comparision with Docker Swarm:
- `--publish` is same as NodePort with `externalTrafficPolicy` as `Cluster`
```
docker service create --name nginx \
  --publish published=80,target=80\
  nginx:latest
```
- `--publish` + `mode=host` is same as NodePort with `externalTrafficPolicy` as `Local`
```
docker service create --name nginx \
  --publish published=80,target=80,mode=host\
  nginx:latest
```


>   More details 
>    - For K8s `kubectl explain svc.spec.externalTrafficPolicy`
>    - For swarm "Bypass the routing mesh" section in https://docs.docker.com/engine/swarm/ingress/