# Chapter 5 walkthrough - Pods
## Creating a Pod
To create pod run:  
`kubectl run <pod_name> --image=<image_repository>`

To list all pods run:  
`kubectl get pods`

To delete pod run:  
`kubectl delete deployments/<pod_name>`

Note that when creating in a imperative manner a pod it will be created by `Deployment` and `ReplicaSet` objects - so you need to specify this in the `delete` command.

## Pod Manifest
Pod manifest is a JSON or YAML file which describes a pod.

Pod manifest can replace a following command:  
```
docker run -d --name <pod_name> --publish 8080:8080 <docker_image_path>:<version>
```

with a following YAML file:
```
apiVersion: v1
kind: Pod
metadata:
  name: <pod_name>
spec:
  containers:
    - image: <docker_image_path>:<version>
      name: <pod_name>
    ports:
      - containerPort: 8080
        name: http
        protocol: TCP
```

To run pod based on the manifest run:  
`kubectl apply -f <your_yaml_file>`

## Get Details

To get details about most of kubernetes objects run:  
`kubectl describe <object_type> <object_name>`  
For example:  
`kubectl describe pods <pod_name>`

## Delete pod
To delete pod created in a declarative manner run:  
`kubectl delete pods/<pod_name>`  
or   
`kubectl delete -f <your_yaml_file>`


## Access the Pod

To start port-forwarding run:  
`kubectl port-forward <pod_name> <local_port>:<pod_port>`


To download the current logs from running pod run:  
`kubectl logs <pod_name>`  
Add `-f` flag for continuous stream of logs.  
Add `--previous` flag for logs from a previous instance of the container.

To execute single command inside container run:  
`kubectl exec <pod_name> <command>`  
Add `-it` flags for an interactive session.

To copy file from or to a container run:  
`kubectl cp <local or pod path> <local or pod path>`


## Health Checks

Liveness Probe is a kubernetes feature which makes sure if you pod is working correctly.  
It can be a simple HTTP request or more sophisticated check.

Example of a pod manifest with a liveness probe:  
```
apiVersion: v1
kind: Pod
metadata:
  name: <pod_name>
spec:
  containers:
    - image: <docker_image_path>:<version>
      name: <pod_name>
      livenessProbe:
        httpGet:
          path: <http_path>
          port: <port>
        initialDelaySeconds: <sec no before start probing>
        timeoutSeconds: <sec waiting for a response>
        periodSeconds: <sec between checks>
        failureThreshold: <no of failures before kill>
    ports:
      - containerPort: <port>
        name: http
        protocol: TCP
```

Readiness Probe in comparision to the liveness probe checks if the pod is ready to serve user requests.  
 If it's not, pod will be removed from the service load balancer.

 ## Resource Management

Resource request is a minimal required amount of resources for a container to operate.  
Resource limit is a maximal allowed amount of resources for a container.

Example of a pod manifest with a resource request and limit:  
```
apiVersion: v1
kind: Pod
metadata:
  name: <pod_name>
spec:
  containers:
    - image: <docker_image_path>:<version>
      name: <pod_name>
      resources:
        requests:
          cpu: "500m"
          memory: "128Mi"
        limits:
          cpu: "1000m"
          memory: "256Mi"
    ports:
      - containerPort: 8080
        name: http
        protocol: TCP
```

## Persisting Data

Adding a volume to a Pod manifest allows to store data in persistent way.

Example of pod manifest with mounted volumes:  

```
apiVersion: v1
kind: Pod
metadata:
  name: <pod_name>
spec:
  volumes:
    - name: "<volume_name>"
      hostPath:
        path: "<local_path>"
  containers:
    - image: <docker_image_path>:<version>
      name: <pod_name>
      volumeMounts:
        - mountPath: "<pod_path>"
          name: "<volume_name>"
    ports:
      - containerPort: 8080
        name: http
        protocol: TCP
```
