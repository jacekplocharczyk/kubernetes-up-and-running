# Chapter 3 walkthrough
## `minikube` on WSL
To use `minikube` on Windows 10 you can use Hyper-V.  
However, you need to create external network by Hyper-V management tool.
All values can be default.

After creating network run following command (WSL):  
`minikube.exe start --vm-driver hyperv --hyperv-virtual-switch "Primary Virtual Switch"`

Ref:  
https://medium.com/@JockDaRock/minikube-on-windows-10-with-hyper-v-6ef0f4dc158c



