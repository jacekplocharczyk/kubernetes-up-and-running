# ReplicaSets
Based on the pod manifest ReplicaSet make sure that all desired pods are up and running.

Example of the replicaset definition:

```
apiVersion: extensions/v1beta1
kind: ReplicaSet
metadata:
  name: <rs_name>
spec:
  replicas: 1
  template:
    metadata:
      labels:
        app: <app_name>
        version: "<version>"
    spec:
      containers:
        - name: <container_name>
          image: "<image_path>:<image_version>"
```

To describe ReplicaSet run:  
`kubectl describe rs <rs_name>`

## Find which ReplicaSet is managing a Pod
To find out more about a pod run:  
`kubectl get pods <pod-name> -o yaml`

**Note: I didn't make more about this chapter because the rest is irrelevant to me at the moment.**