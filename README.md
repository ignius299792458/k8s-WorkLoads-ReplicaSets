# k8s-WorkLoads-ReplicaSets

## `ReplicaSet`
`Definition`: A ReplicaSet maintains a stable set of replica pods running at any given time, ensuring that the specified number of identical pods are operational.

`Example`:
Your team has developed an internal analytics processing service that needs to run multiple identical instances for capacity.
You create a ReplicaSet to maintain 5 identical pods of this service. If any pod fails, the ReplicaSet automatically creates a replacement to maintain exactly 5 running instances. However, in practice, you rarely interact with ReplicaSets directly because Deployments provide higher-level functionality. This is similar to manually setting the cruise control in a car without the automatic adjustment features.


## Kubernetes Workload Resources
Key differences between DaemonSet, StatefulSet, ReplicaSet, and Deployment in Kubernetes:

| Feature | DaemonSet | StatefulSet | ReplicaSet | Deployment |
|---------|-----------|-------------|------------|------------|
| **Purpose** | Runs a pod on every node in the cluster | Maintains state and unique identity for pods | Maintains a stable set of replica pods | High-level resource for deploying and updating applications |
| **Pod Identity** | Each pod is unique to a node | Each pod has persistent identity and stable hostname | Pods are interchangeable | Pods are interchangeable |
| **Scaling** | Automatically scales with nodes (one pod per node) | Manual or auto-scaling with ordered creation/deletion | Manual or auto-scaling with random creation/deletion | Manual or auto-scaling with random creation/deletion |
| **Pod Naming** | Usually `<name>-<node-name>` | `<name>-0`, `<name>-1`, etc. (ordered, sequential) | Random names with hash | Random names with hash |
| **Storage** | Typically uses node storage | Supports stable persistent storage per pod | Shared storage only | Shared storage only |
| **Load Balancing** | Not inherently load-balanced (one per node) | Not automatically load-balanced (identity matters) | Load-balanced (stateless) | Load-balanced (stateless) |
| **Updates** | Rolling updates possible | Ordered, sequential updates | All pods updated simultaneously | Rolling updates, canary deployments, rollbacks |
| **Use Cases** | Monitoring, logging, networking agents | Databases, messaging queues, stateful applications | Rarely used directly (deployment uses it) | Web applications, APIs, stateless workloads |
| **Deletion Order** | Random | Reverse order (highest to lowest index) | Random | Random |
| **Owns ReplicaSet** | No | No | No | Yes (manages ReplicaSets) |

## Example to illustrate how to create, see, and delete the replicaSets
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

```
