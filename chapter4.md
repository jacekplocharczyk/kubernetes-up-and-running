# Chapter 4 walkthrough - Common `kubectl` Commands
## Namespaces
Used for organization of kubernetes objects - e.g. `kube-system`.  
If you want to run command in specific namespace add `--namespace=$namespace$` flag  
To list all namespaces use `kubectl get namespaces`

## Contexts
To use some namespace as a default you can create configuration called *context*.  
It will be recorded in the `$HOME/.kube/config` file.

To create context run:  
`kubectl config set-context jaceks_context --namespace=my_namespace`

To use it run:  
`kubectl config use-context jaceks_context`


Context can be also used to manage different users or clusters by using `--users` or `--clusters` flag in the `set-context` command.

## Everything as a REST API object
Get list of specific resources:  
`kubectl get <resource-name>`  
Example: `kubectl get namespaces`

Get specific resource:  
`kubectl get <resource-name> <object-name>`
Example: `kubectl get namespaces kube-system`

To get more info add `-o json` flag.  
To skip headers add `--no-headers` flag.  
To get single field use `--template={.primary_key.secondary_key} -o jsonpath` flags.  
Example: `kubectl get namespaces kube-system --template={.metadata.name} -o jsonpath`

To get detailed info use `describe` instead of `get`:  
`kubectl describe <resource-name> <obj-name>`  
Example: `kubectl describe namespaces kube-system`

## Manipulating Kubernetes Objects (create, update, and destroy)

You can create or update object based on the JSON/YAML file. :
`kubectl apply -f obj.yaml`  

You can also make an interactive edit:  
`kubectl edit <resource-name> <obj-name>`  
Example: `kubectl edit namespaces kube-system`

To delete object run:  
`kubectl delete -f obj.yaml`  
or  
`kubectl delete <resource-name> <obj-name>`  

## Labels and Annotations

To add label for object run:  
`kubectl label <resource-name> <obj-name> <label>=<string>`  

To add annotation for object run:  
`kubectl annotate <resource-name> <obj-name> <label>=<string>`  

If you want to overrigth existing label add `--overwrite` flag.

To remove label run:  
`kubectl label <resource-name> <obj-name> -<label>`  


## Debugging

To see logs run:
`kubectl logs <pod-name>`  

If there are multiple containers inside a pod you can choose container by adding `-c` flag.  
To see continous stream of logs add `-f` flag

To start interactive execute commands in a running container run:  
`kubectl exec -it <pod-name> -- bash`

To copy files from or to a container run:  
`kubectl cp <pod-name>:/path/to/remote/file /path/to/local/file`


