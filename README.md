# k8s yamlfiles
### history
```
 1993  kubectl version
 1994  kubectl apply -f pod.yaml
 1995  kubectl get pod
 1996  kubectl get po
 1997  kubectl get po -w
 1998  kubectl get pod
 1999  kubectl get pod -o wide
 2000  kubectl describe pod akpod
 ```
 ### 3feb
 ```
 akash@sky:~/mynewtest$ minikube status
minikube
type: Control Plane
host: Stopped
kubelet: Stopped
apiserver: Stopped
kubeconfig: Stopped

akash@sky:~/mynewtest$ minikube start
😄  minikube v1.30.1 on Ubuntu 20.04
🆕  Kubernetes 1.26.3 is now available. If you would like to upgrade, specify: --kubernetes-version=v1.26.3
✨  Using the docker driver based on existing profile
🎉  minikube 1.32.0 is available! Download it: https://github.com/kubernetes/minikube/releases/tag/v1.32.0
💡  To disable this notice, run: 'minikube config set WantUpdateNotification false'

akash@sky:~/mynewtest$ kubectl get ns
NAME                   STATUS   AGE
akash                  Active   23h
default                Active   11d
kube-node-lease        Active   11d
kube-public            Active   11d
kube-system            Active   11d
kubernetes-dashboard   Active   11d
openedx                Active   11d
akash@sky:~/mynewtest$ kubectl get pod --namespace akash
No resources found in akash namespace.
akash@sky:~/mynewtest$ kubectl apply -f pod1.yaml --namespace akash
pod/myapp created
akash@sky:~/mynewtest$ kubectl get pod
NAME    READY   STATUS    RESTARTS        AGE
hello   1/1     Running   1 (7m18s ago)   23h
akash@sky:~/mynewtest$ kubectl get pod --namespace akash
NAME    READY   STATUS    RESTARTS   AGE
myapp   1/1     Running   0          38s
akash@sky:~/mynewtest$ kubectl config set-context --current --namespace akash
Context "minikube" modified.
akash@sky:~/mynewtest$ kubectl get pod
NAME    READY   STATUS    RESTARTS   AGE
myapp   1/1     Running   0          110s
akash@sky:~/mynewtest$ kube
kubectl     kubernetes  
akash@sky:~/mynewtest$ kubectl get config
error: the server doesn't have a resource type "config"
akash@sky:~/mynewtest$ kubectl config get-contexts 
CURRENT   NAME                          CLUSTER      AUTHINFO           NAMESPACE
          kubernetes-admin@kubernetes   kubernetes   kubernetes-admin   default
*         minikube                      minikube     minikube           akash
akash@sky:~/mynewtest$ kubectl get ns
NAME                   STATUS   AGE
akash                  Active   23h
default                Active   11d
kube-node-lease        Active   11d
kube-public            Active   11d
kube-system            Active   11d
kubernetes-dashboard   Active   11d
openedx                Active   11d
akash@sky:~/mynewtest$ kubectl get pod --all-namespaces 
NAMESPACE              NAME                                        READY   STATUS    RESTARTS      AGE
akash                  myapp                                       1/1     Running   0             3m49s
default                hello                                       1/1     Running   1 (11m ago)   23h
kube-system            calico-kube-controllers-7bdbfc669-qrpvb     1/1     Running   5 (11m ago)   11d
kube-system            calico-node-2p8vh                           1/1     Running   6 (11m ago)   11d
kube-system            coredns-787d4945fb-c8cn2                    1/1     Running   7 (11m ago)   11d
kube-system            etcd-minikube                               1/1     Running   6 (11m ago)   11d
kube-system            kube-apiserver-minikube                     1/1     Running   6 (11m ago)   11d
kube-system            kube-controller-manager-minikube            1/1     Running   8 (11m ago)   11d
kube-system            kube-proxy-kmzvr                            1/1     Running   6 (11m ago)   11d
kube-system            kube-scheduler-minikube                     1/1     Running   7 (11m ago)   11d
kubernetes-dashboard   dashboard-metrics-scraper-5c6664855-zpvdq   1/1     Running   7 (11m ago)   11d
kubernetes-dashboard   kubernetes-dashboard-55c4cbbc7c-5ljmm       1/1     Running   7 (11m ago)   11d
akash@sky:~/mynewtest$ 
kubectl create secret docker-registry mysec --docker-server=docker.io --docker-username=akash --docker-password=xyz123 --dry-run -o yaml >sec.yaml 
 2013  kubectl create secret docker-registry mysec --docker-server=docker.io --docker-username=akash --docker-password=xyz123 --dry-run=client -o yaml >sec.yaml 
 2014  kubectl create secret docker-registry mysec --docker-server=docker.io --docker-username=akash --docker-password=xyz123  
 2015  kubectl get secrets 
```
## deployment
```
akash@sky:~/mynewtest$ kubectl create deployment mydep --replicas 5 --image nginx --port 80 --dry-run=client -o yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  creationTimestamp: null
  labels:
    app: mydep
  name: mydep
spec:
  replicas: 5
  selector:
    matchLabels:
      app: mydep
  strategy: {}
  template:
    metadata:
      creationTimestamp: null
      labels:
        app: mydep
    spec:
      containers:
```