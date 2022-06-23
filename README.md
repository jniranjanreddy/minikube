# minikube

## What happens if minikue unable to start

Solution it worked for me
```
minikube delete --all --purge
root@minikube01 ~ # minikube delete --all --purge
* Uninstalling Kubernetes v1.20.2 using kubeadm ...
* Deleting "minikube" in none ...
* Removed all traces of the "minikube" cluster.
* Successfully deleted all profiles
* Successfully purged minikube directory located at - [/root/.minikube]


root@minikube01 ~ # minikube start --driver=none
* minikube v1.18.1 on Centos 7.9.2009
* Using the none driver based on user configuration
* Starting control plane node minikube in cluster minikube
* Running on localhost (CPUs=2, Memory=7821MB, Disk=44422MB) ...
* OS release is CentOS Linux 7 (Core)
* Preparing Kubernetes v1.20.2 on Docker 19.03.13 ...
! This bare metal machine is having trouble accessing https://k8s.gcr.io
* To pull new external images, you may need to configure a proxy: https://minikube.sigs.k8s.io/docs/reference/networking/proxy/
* minikube 1.26.0 is available! Download it: https://github.com/kubernetes/minikube/releases/tag/v1.26.0
* To disable this notice, run: 'minikube config set WantUpdateNotification false'

    > kubeadm.sha256: 64 B / 64 B [--------------------------] 100.00% ? p/s 0s
    > kubectl.sha256: 64 B / 64 B [--------------------------] 100.00% ? p/s 0s
    > kubelet.sha256: 64 B / 64 B [--------------------------] 100.00% ? p/s 0s
    > kubectl: 38.37 MiB / 38.37 MiB [----------------] 100.00% 5.14 MiB p/s 7s
    > kubeadm: 37.40 MiB / 37.40 MiB [----------------] 100.00% 4.58 MiB p/s 8s
    > kubelet: 108.73 MiB / 108.73 MiB [-------------] 100.00% 6.68 MiB p/s 16s
  - Generating certificates and keys ...
  - Booting up control plane ...
  - Configuring RBAC rules ...
* Configuring local host environment ...
*
! The 'none' driver is designed for experts who need to integrate with an existing VM
* Most users should use the newer 'docker' driver instead, which does not require root!
* For more information, see: https://minikube.sigs.k8s.io/docs/reference/drivers/none/
*
! kubectl and minikube configuration will be stored in /root
! To use kubectl or minikube commands as your own user, you may need to relocate them. For example, to overwrite your own settings, run:
*
  - sudo mv /root/.kube /root/.minikube $HOME
  - sudo chown -R $USER $HOME/.kube $HOME/.minikube
*
* This can also be done automatically by setting the env var CHANGE_MINIKUBE_NONE_USER=true
* Verifying Kubernetes components...
  - Using image gcr.io/k8s-minikube/storage-provisioner:v4
* Enabled addons: storage-provisioner, default-storageclass
* Done! kubectl is now configured to use "minikube" cluster and "default" namespace by default
```

