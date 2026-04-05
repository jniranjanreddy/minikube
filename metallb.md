## MetallM works as a cloud loadbalancer
```
devops@ubuntu24:~$ minikube addons enable metallb
❗  metallb is a 3rd party addon and is not maintained or verified by minikube maintainers, enable at your own risk.
❗  metallb does not currently have an associated maintainer.
    ▪ Using image quay.io/metallb/controller:v0.9.6
    ▪ Using image quay.io/metallb/speaker:v0.9.6
🌟  The 'metallb' addon is enabled

 k get svc -A
NAMESPACE      NAME                   TYPE           CLUSTER-IP       EXTERNAL-IP   PORT(S)                                                                      AGE
default        kubernetes             ClusterIP      10.96.0.1        <none>        443/TCP                                                                      25m
istio-system   istio-egressgateway    ClusterIP      10.110.182.1     <none>        80/TCP,443/TCP                                                               11m
istio-system   istio-ingressgateway   LoadBalancer   10.105.239.9     <pending>     15021:31571/TCP,80:31162/TCP,443:30780/TCP,31400:32467/TCP,15443:30232/TCP   11m
istio-system   istiod                 ClusterIP      10.111.166.241   <none>        15010/TCP,15012/TCP,443/TCP,15014/TCP                                        14m
kube-system    kube-dns               ClusterIP      10.96.0.10       <none>        53/UDP,53/TCP,9153/TCP                                                       25m
devops@ubuntu24:~$ kubectl get pods -n metallb-system
NAME                         READY   STATUS    RESTARTS   AGE
controller-cff57fcb5-485n2   1/1     Running   0          3m3s
speaker-stbl4                1/1     Running   0          3m3s
```





## Add IP
```
minikube ip
192.168.49.2




minikube addons configure metallb
-- Enter Load Balancer Start IP: 192.168.49.10
-- Enter Load Balancer End IP: 192.168.49.20
    ▪ Using image quay.io/metallb/controller:v0.9.6
    ▪ Using image quay.io/metallb/speaker:v0.9.6
✅  metallb was successfully configured
devops@ubuntu24:~$ k get svc -A
NAMESPACE      NAME                   TYPE           CLUSTER-IP       EXTERNAL-IP     PORT(S)                                                                      AGE
default        kubernetes             ClusterIP      10.96.0.1        <none>          443/TCP                                                                      26m
istio-system   istio-egressgateway    ClusterIP      10.110.182.1     <none>          80/TCP,443/TCP                                                               11m
istio-system   istio-ingressgateway   LoadBalancer   10.105.239.9     192.168.49.10   15021:31571/TCP,80:31162/TCP,443:30780/TCP,31400:32467/TCP,15443:30232/TCP   11m
istio-system   istiod                 ClusterIP      10.111.166.241   <none>          15010/TCP,15012/TCP,443/TCP,15014/TCP                                        15m
kube-system    kube-dns               ClusterIP      10.96.0.10       <none>          53/UDP,53/TCP,9153/TCP                                                       25m
devops@ubuntu24:~$
```
## Verify
```
devops@ubuntu24:~$ kubectl get configmap config -n metallb-system -o yaml
apiVersion: v1
data:
  config: |
    address-pools:
    - name: default
      protocol: layer2
      addresses:
      - 192.168.49.10-192.168.49.20
kind: ConfigMap
metadata:
  annotations:
    kubectl.kubernetes.io/last-applied-configuration: |
      {"apiVersion":"v1","data":{"config":"address-pools:\n- name: default\n  protocol: layer2\n  addresses:\n  - 192.168.49.10-192.168.49.20\n"},"kind":"ConfigMap","metadata":{"annotations":{},"name":"config","namespace":"metallb-system"}}
  creationTimestamp: "2026-04-05T00:19:28Z"
  name: config
  namespace: metallb-system
  resourceVersion: "2267"
  uid: 7ae02f6c-fb69-4ce3-9482-95c73a8c90dc
```
