# ConfigMaps and Secrets

## ConfigMaps

To create ConfigMap from a file run:  

`kubectl create configmap <config_name> --from-file=<file_path>`

To create ConfigMap from a literal run:  

`kubectl create configmap <config_name> --from-literal=<param_name>=<param_value>`

To see config run:  
`kubectl get configmaps <config_name> -o yaml`


You can use ConfigMaps to create environment variables or you can mount the whole config as a volume.  
 Example below shows such case.

```
apiVersion: v1
kind: Pod
metadata:
  name: <pod_name>
spec:
  volumes:
    - name: "<volume_name>"
      configMap:
        name: <config_name>
  containers:
    - image: <docker_image_path>:<version>
      name: <pod_name>
      volumeMounts:
        - mountPath: "<pod_path>"
          name: "<volume_name>"
      env:
        - name: <ENV_VAR_NAME>
          valueFrom:
            configMapKeyRef:
              name: <config_name>
              key: <key_name>
```

## Secrets

To create secret from a literal or file run:  
`kubectl create secret generic <secret_name> --from-file=<file_path> --from-literal=<key>=<value>`

To get help run:  
`kubectl help create secret generic`

To consume secrets expose them as a volume - see an example below:

```
apiVersion: v1
kind: Pod
metadata:
  name: <pod_name>
spec:
  volumes:
    - name: "<volume_name>"
      secret:
        secretName: <secret_name>
  containers:
    - image: <docker_image_path>:<version>
      name: <pod_name>
      volumeMounts:
        - mountPath: "<pod_path>"
          name: "<volume_name>"
          readOnly: true
```

## Private Docker Registries - skipped
## Managing ConfigMaps and Secrets
To get list of configs or secrets run:  
`kubectl get configmaps` or `kubectl get secrets`

To get more detailed info run:  
`kubectl describe configmap <config_name>`

To get raw yaml file run:  
`kubectl get configmap <config_name> -o yaml`