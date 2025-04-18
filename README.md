# k8s-WorkLoads-ReplicaSets
k8s process of handling workloads based on ReplicaSet distribution

Example to illustrate how to create, see, and delete the replicaSets
```
➜  kubectl apply -f replicasets.yml 
replicaset.apps/nginx-replicasets created
➜  kubectl get replicasets -n nginx
NAME                          DESIRED   CURRENT   READY   AGE
nginx-deployment-6c88fc8949   0         0         0       3d
nginx-deployment-96b9d695     0         0         0       3d2h
nginx-deployment-f58b5c699    2         2         2       3d
nginx-replicasets             2         2         2       14s
➜  kubectl delete replicaset.apps/nginx-replicasets -n nginx
replicaset.apps "nginx-replicasets" deleted
➜  

```
