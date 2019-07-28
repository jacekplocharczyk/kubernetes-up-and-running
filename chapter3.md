# Chapter 3 walkthrough
## Installing Kubernetes on WSL
To start you need Kubernetes up and running so there are a few things to do:  
1. Enable kubernetes in Docker for Windows
2. Install `kubectl` in WSL:  
   ```
   curl -LO https://storage.googleapis.com/kubernetes-release/release/  
   $(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt)
   /bin/linux/amd64/kubectl \
   && chmod +x ./kubectl \
   && sudo mv ./kubectl /usr/local/bin/kubectl
   ```
3. Copy setting from Windows to WSL  
   `mkdir ~/.kube && cp /mnt/c/Users/[USERNAME]/.kube/config ~/.kube`

Ref:  
https://devkimchi.com/2018/06/05/running-kubernetes-on-wsl/

## `minikube` on WSL
To use `minikube` on Windows 10 you can use Hyper-V.  
However, you need to create external network by Hyper-V management tool.
All values can be default.

After creating network run following command (WSL):  
`minikube.exe start --vm-driver hyperv --hyperv-virtual-switch "Primary Virtual Switch"`

To enable dashboard run:  
`minikube.exe dashboard`

Ref:  
https://medium.com/@JockDaRock/minikube-on-windows-10-with-hyper-v-6ef0f4dc158c


## The Kubernetes Client - `kubectl`
List of commands used in this chapter:  
1. `kubectl version`
2. `kubectl get componentstatuses`
3. `kubectl get nodes`
4. `kubectl describe nodes [node name if there are more than one]`
5. `kubectl get daemonSets --namespace=kube-system kube-proxy`
6. `kubectl get deployments --namespace=kube-system kube-dns`
7. `kubectl get services --namespace=kube-system kube-dns`
8. `kubectl proxy`

Commands which didn't work (it's probably related to `minikube` but I'm not 100% sure):

1. `kubectl get deployments --namespace=kube-system kubernetes-dashboard`
2. `kubectl get services --namespace=kube-system kubernetes-dashboard`

