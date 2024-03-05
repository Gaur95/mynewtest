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
### 14feb history
```
 kubectl get node
 1996  kubectl get pod
 1997  kubectl delete deployments.apps mydeployment 
 1998  kubectl get deploy
 1999  kubectl get pod
 2000  kubectl get pod -A
 2001  kubectl get pod -A -o wide
 2002  kubectl get ds
 2003  kubectl get ds -A
 2004  kubectl get ds -A -o yaml
 2005  kubectl apply -f https://raw.githubusercontent.com/Gaur95/mynewtest/k8s/ns.yaml
 2006  kubectl get ns
 2007  cd mynewtest/
 2008  ls
 2009  code .
 2010  kubectl get nsvc
 2011  kubectl get svc
 2012  kubectl apply -f deployment.yaml 
 2013  kubectl get svc
 2014  kubectl get deployments.apps 
 2015  kubectl get pod
 2016  kubectl get pod -o wide
```
## dashboard
Accessing the Dashboard UI
To protect your cluster data, Dashboard deploys with a minimal RBAC configuration by default. Currently, Dashboard only supports logging in with a <b>Bearer Token</b>. To create a token for this demo, you can follow our guide on creating a sample user.

You can enable access to the Dashboard using the kubectl command-line tool, by running the following command:
```
kubectl proxy
```
Kubectl will make Dashboard available at 
http://localhost:8001/api/v1/namespaces/kubernetes-dashboard/services/https:kubernetes-dashboard:/proxy/.

### creat token for serviceaccount
```
kubectl create token kubernetes-dashboard --namespace kubernetes-dashboard
```
## config
```
akash@sky:~/mynewtest$ export KUBECONFIG=/home/akash/Downloads/sonu.conf 
akash@sky:~/mynewtest$ kubectl get node
NAME      STATUS   ROLES           AGE   VERSION
master    Ready    control-plane   19d   v1.28.2
worker1   Ready    <none>          19d   v1.28.2
worker2   Ready    <none>          19d   v1.28.2
akash@sky:~/mynewtest$ kubectl get sa
NAME         SECRETS   AGE
default      0         19d
monitor-sa   0         4d23h
akash@sky:~/mynewtest$ kubectl get clusterrole
NAME                                                                   CREATED AT
admin                                                                  2024-02-15T07:14:28Z
calico-kube-controllers                                                2024-02-15T07:20:48Z
calico-node                                                            2024-02-15T07:20:48Z
cluster-admin                                                          2024-02-15T07:14:28Z
edit                                                                   2024-02-15T07:14:28Z
kubeadm:get-nodes                                                      2024-02-15T07:14:30Z
kubernetes-dashboard                                                   2024-02-19T12:08:29Z
monitor-sa-cluster-role                                                2024-02-29T15:48:15Z
system:aggregate-to-admin                                              2024-02-15T07:14:28Z
system:aggregate-to-edit                                               2024-02-15T07:14:28Z
system:aggregate-to-view                                               2024-02-15T07:14:28Z
system:aggregated-metrics-reader                                       2024-02-28T14:53:25Z
system:auth-delegator                                                  2024-02-15T07:14:28Z
system:basic-user                                                      2024-02-15T07:14:28Z
system:certificates.k8s.io:certificatesigningrequests:nodeclient       2024-02-15T07:14:28Z
system:certificates.k8s.io:certificatesigningrequests:selfnodeclient   2024-02-15T07:14:28Z
system:certificates.k8s.io:kube-apiserver-client-approver              2024-02-15T07:14:28Z
system:certificates.k8s.io:kube-apiserver-client-kubelet-approver      2024-02-15T07:14:28Z
system:certificates.k8s.io:kubelet-serving-approver                    2024-02-15T07:14:28Z
system:certificates.k8s.io:legacy-unknown-approver                     2024-02-15T07:14:28Z
system:controller:attachdetach-controller                              2024-02-15T07:14:28Z
system:controller:certificate-controller                               2024-02-15T07:14:29Z
system:controller:clusterrole-aggregation-controller                   2024-02-15T07:14:28Z
system:controller:cronjob-controller                                   2024-02-15T07:14:28Z
system:controller:daemon-set-controller                                2024-02-15T07:14:28Z
system:controller:deployment-controller                                2024-02-15T07:14:28Z
system:controller:disruption-controller                                2024-02-15T07:14:28Z
system:controller:endpoint-controller                                  2024-02-15T07:14:28Z
system:controller:endpointslice-controller                             2024-02-15T07:14:28Z
system:controller:endpointslicemirroring-controller                    2024-02-15T07:14:28Z
system:controller:ephemeral-volume-controller                          2024-02-15T07:14:28Z
system:controller:expand-controller                                    2024-02-15T07:14:28Z
system:controller:generic-garbage-collector                            2024-02-15T07:14:28Z
system:controller:horizontal-pod-autoscaler                            2024-02-15T07:14:28Z
system:controller:job-controller                                       2024-02-15T07:14:28Z
system:controller:namespace-controller                                 2024-02-15T07:14:28Z
system:controller:node-controller                                      2024-02-15T07:14:28Z
system:controller:persistent-volume-binder                             2024-02-15T07:14:28Z
system:controller:pod-garbage-collector                                2024-02-15T07:14:28Z
system:controller:pv-protection-controller                             2024-02-15T07:14:29Z
system:controller:pvc-protection-controller                            2024-02-15T07:14:29Z
system:controller:replicaset-controller                                2024-02-15T07:14:28Z
system:controller:replication-controller                               2024-02-15T07:14:28Z
system:controller:resourcequota-controller                             2024-02-15T07:14:28Z
system:controller:root-ca-cert-publisher                               2024-02-15T07:14:29Z
system:controller:route-controller                                     2024-02-15T07:14:28Z
system:controller:service-account-controller                           2024-02-15T07:14:28Z
system:controller:service-controller                                   2024-02-15T07:14:28Z
system:controller:statefulset-controller                               2024-02-15T07:14:28Z
system:controller:ttl-after-finished-controller                        2024-02-15T07:14:29Z
system:controller:ttl-controller                                       2024-02-15T07:14:28Z
system:coredns                                                         2024-02-15T07:14:30Z
system:discovery                                                       2024-02-15T07:14:28Z
system:heapster                                                        2024-02-15T07:14:28Z
system:kube-aggregator                                                 2024-02-15T07:14:28Z
system:kube-controller-manager                                         2024-02-15T07:14:28Z
system:kube-dns                                                        2024-02-15T07:14:28Z
system:kube-scheduler                                                  2024-02-15T07:14:28Z
akash@sky:~/mynewtest$ kubectl apply -f clusterrolebinding.yaml 
clusterrolebinding.rbac.authorization.k8s.io/monitor-sa-cluster-role-binding created
akash@sky:~/mynewtest$ kubectl get clusterrolebinding.yaml 
^C
akash@sky:~/mynewtest$ kubectl get clusterrolebinding
NAME                                                   ROLE                                                                               AGE
calico-kube-controllers                                ClusterRole/calico-kube-controllers                                                19d
calico-node                                            ClusterRole/calico-node                                                            19d
cluster-admin                                          ClusterRole/cluster-admin                                                          19d
kubeadm:get-nodes                                      ClusterRole/kubeadm:get-nodes                                                      19d
kubeadm:kubelet-bootstrap                              ClusterRole/system:node-bootstrapper                                               19d
kubeadm:node-autoapprove-bootstrap                     ClusterRole/system:certificates.k8s.io:certificatesigningrequests:nodeclient       19d
kubeadm:node-autoapprove-certificate-rotation          ClusterRole/system:certificates.k8s.io:certificatesigningrequests:selfnodeclient   19d
kubeadm:node-proxier                                   ClusterRole/system:node-proxier                                                    19d
kubernetes-dashboard                                   ClusterRole/kubernetes-dashboard                                                   15d
metrics-server:system:auth-delegator                   ClusterRole/system:auth-delegator                                                  6d
monitor-sa-cluster-role-binding                        ClusterRole/monitor-sa-cluster-role                                                18s
system:basic-user                                      ClusterRole/system:basic-user                                                      19d
system:controller:attachdetach-controller              ClusterRole/system:controller:attachdetach-controller                              19d
system:controller:certificate-controller               ClusterRole/system:controller:certificate-controller                               19d
system:controller:clusterrole-aggregation-controller   ClusterRole/system:controller:clusterrole-aggregation-controller                   19d
system:controller:cronjob-controller                   ClusterRole/system:controller:cronjob-controller                                   19d
system:controller:daemon-set-controller                ClusterRole/system:controller:daemon-set-controller                                19d
system:controller:deployment-controller                ClusterRole/system:controller:deployment-controller                                19d
system:controller:disruption-controller                ClusterRole/system:controller:disruption-controller                                19d
system:controller:endpoint-controller                  ClusterRole/system:controller:endpoint-controller                                  19d
system:controller:endpointslice-controller             ClusterRole/system:controller:endpointslice-controller                             19d
system:controller:endpointslicemirroring-controller    ClusterRole/system:controller:endpointslicemirroring-controller                    19d
system:controller:ephemeral-volume-controller          ClusterRole/system:controller:ephemeral-volume-controller                          19d
system:controller:expand-controller                    ClusterRole/system:controller:expand-controller                                    19d
system:controller:generic-garbage-collector            ClusterRole/system:controller:generic-garbage-collector                            19d
system:controller:horizontal-pod-autoscaler            ClusterRole/system:controller:horizontal-pod-autoscaler                            19d
system:controller:job-controller                       ClusterRole/system:controller:job-controller                                       19d
system:controller:namespace-controller                 ClusterRole/system:controller:namespace-controller                                 19d
system:controller:node-controller                      ClusterRole/system:controller:node-controller                                      19d
system:controller:persistent-volume-binder             ClusterRole/system:controller:persistent-volume-binder                             19d
system:controller:pod-garbage-collector                ClusterRole/system:controller:pod-garbage-collector                                19d
system:controller:pv-protection-controller             ClusterRole/system:controller:pv-protection-controller                             19d
system:controller:pvc-protection-controller            ClusterRole/system:controller:pvc-protection-controller                            19d
system:controller:replicaset-controller                ClusterRole/system:controller:replicaset-controller                                19d
system:controller:replication-controller               ClusterRole/system:controller:replication-controller                               19d
system:controller:resourcequota-controller             ClusterRole/system:controller:resourcequota-controller                             19d
system:controller:root-ca-cert-publisher               ClusterRole/system:controller:root-ca-cert-publisher                               19d
system:controller:route-controller                     ClusterRole/system:controller:route-controller                                     19d
system:controller:service-account-controller           ClusterRole/system:controller:service-account-controller                           19d
system:controller:service-controller                   ClusterRole/system:controller:service-controller                                   19d
system:controller:statefulset-controller               ClusterRole/system:controller:statefulset-controller                               19d
system:controller:ttl-after-finished-controller        ClusterRole/system:controller:ttl-after-finished-controller                        19d
system:controller:ttl-controller                       ClusterRole/system:controller:ttl-controller                                       19d
system:coredns                                         ClusterRole/system:coredns                                                         19d
akash@sky:~/mynewtest$ kubectl create config monitor-sa -n default
Error: must specify one of -f and -k

error: unknown command "config monitor-sa"
See 'kubectl create -h' for help and examples
akash@sky:~/mynewtest$ kubectl create -h
Create a resource from a file or from stdin.

 JSON and YAML formats are accepted.

Examples:
  # Create a pod using the data in pod.json
  kubectl create -f ./pod.json
  
  # Create a pod based on the JSON passed into stdin
  cat pod.json | kubectl create -f -
  
  # Edit the data in registry.yaml in JSON then create the resource using the edited data
  kubectl create -f registry.yaml --edit -o json

Available Commands:
  clusterrole           Create a cluster role
  clusterrolebinding    Create a cluster role binding for a particular cluster role
  configmap             Create a config map from a local file, directory or literal value
  cronjob               Create a cron job with the specified name
  deployment            Create a deployment with the specified name
  ingress               Create an ingress with the specified name
  job                   Create a job with the specified name
  namespace             Create a namespace with the specified name
  poddisruptionbudget   Create a pod disruption budget with the specified name
  priorityclass         Create a priority class with the specified name
  quota                 Create a quota with the specified name
  role                  Create a role with single rule
  rolebinding           Create a role binding for a particular role or cluster role
  secret                Create a secret using a specified subcommand
  service               Create a service using a specified subcommand
  serviceaccount        Create a service account with the specified name
  token                 Request a service account token

Options:
    --allow-missing-template-keys=true:
        If true, ignore any errors in templates when a field or map key is missing in the
        template. Only applies to golang and jsonpath output formats.

    --dry-run='none':
        Must be "none", "server", or "client". If client strategy, only print the object that
        would be sent, without sending it. If server strategy, submit server-side request without
        persisting the resource.

    --edit=false:
        Edit the API resource before creating

    --field-manager='kubectl-create':
        Name of the manager used to track field ownership.

    -f, --filename=[]:
        Filename, directory, or URL to files to use to create the resource

    -k, --kustomize='':
        Process the kustomization directory. This flag can't be used together with -f or -R.

    -o, --output='':
        Output format. One of: (json, yaml, name, go-template, go-template-file, template,
        templatefile, jsonpath, jsonpath-as-json, jsonpath-file).

    --raw='':
        Raw URI to POST to the server.  Uses the transport specified by the kubeconfig file.

    -R, --recursive=false:
        Process the directory used in -f, --filename recursively. Useful when you want to manage
        related manifests organized within the same directory.

    --save-config=false:
        If true, the configuration of current object will be saved in its annotation. Otherwise,
        the annotation will be unchanged. This flag is useful when you want to perform kubectl
        apply on this object in the future.

    -l, --selector='':
        Selector (label query) to filter on, supports '=', '==', and '!='.(e.g. -l
        key1=value1,key2=value2). Matching objects must satisfy all of the specified label
        constraints.

    --show-managed-fields=false:
        If true, keep the managedFields when printing objects in JSON or YAML format.

    --template='':
        Template string or path to template file to use when -o=go-template, -o=go-template-file.
        The template format is golang templates
        [http://golang.org/pkg/text/template/#pkg-overview].

    --validate='strict':
        Must be one of: strict (or true), warn, ignore (or false).              "true" or "strict" will use a
        schema to validate the input and fail the request if invalid. It will perform server side
        validation if ServerSideFieldValidation is enabled on the api-server, but will fall back
        to less reliable client-side validation if not.                 "warn" will warn about unknown or
        duplicate fields without blocking the request if server-side field validation is enabled
        on the API server, and behave as "ignore" otherwise.            "false" or "ignore" will not
        perform any schema validation, silently dropping any unknown or duplicate fields.

    --windows-line-endings=false:
        Only relevant if --edit=true. Defaults to the line ending native to your platform.

Usage:
  kubectl create -f FILENAME [options]

Use "kubectl create <command> --help" for more information about a given command.
Use "kubectl options" for a list of global command-line options (applies to all commands).
akash@sky:~/mynewtest$ kubectl create config sa monitor-sa
Error: must specify one of -f and -k

error: unknown command "config sa monitor-sa"
See 'kubectl create -h' for help and examples
akash@sky:~/mynewtest$ kubectl create config  monitor-sa -n default
akash@sky:~/mynewtest$ kubectl get pod --kubeconfig=config
E0305 20:56:03.789601   50559 memcache.go:265] couldn't get current server API group list: Get "http://localhost:8080/api?timeout=32s": dial tcp 127.0.0.1:8080: connect: connection refused
E0305 20:56:03.789984   50559 memcache.go:265] couldn't get current server API group list: Get "http://localhost:8080/api?timeout=32s": dial tcp 127.0.0.1:8080: connect: connection refused
E0305 20:56:03.792421   50559 memcache.go:265] couldn't get current server API group list: Get "http://localhost:8080/api?timeout=32s": dial tcp 127.0.0.1:8080: connect: connection refused
E0305 20:56:03.792686   50559 memcache.go:265] couldn't get current server API group list: Get "http://localhost:8080/api?timeout=32s": dial tcp 127.0.0.1:8080: connect: connection refused
E0305 20:56:03.794157   50559 memcache.go:265] couldn't get current server API group list: Get "http://localhost:8080/api?timeout=32s": dial tcp 127.0.0.1:8080: connect: connection refused
The connection to the server localhost:8080 was refused - did you specify the right host or port?
akash@sky:~/mynewtest$ kubectl info
error: unknown command "info" for "kubectl"
akash@sky:~/mynewtest$ kubectl cluster-info
Kubernetes control plane is running at https://3.111.137.153:6443
CoreDNS is running at https://3.111.137.153:6443/api/v1/namespaces/kube-system/services/kube-dns:dns/proxy

To further debug and diagnose cluster problems, use 'kubectl cluster-info dump'.
akash@sky:~/mynewtest$ kubectl get pod --kubeconfig=config
E0305 21:03:09.396144   57197 memcache.go:265] couldn't get current server API group list: Get "http://localhost:8080/api?timeout=32s": dial tcp 127.0.0.1:8080: connect: connection refused
E0305 21:03:09.396424   57197 memcache.go:265] couldn't get current server API group list: Get "http://localhost:8080/api?timeout=32s": dial tcp 127.0.0.1:8080: connect: connection refused
E0305 21:03:09.398804   57197 memcache.go:265] couldn't get current server API group list: Get "http://localhost:8080/api?timeout=32s": dial tcp 127.0.0.1:8080: connect: connection refused
E0305 21:03:09.399113   57197 memcache.go:265] couldn't get current server API group list: Get "http://localhost:8080/api?timeout=32s": dial tcp 127.0.0.1:8080: connect: connection refused
E0305 21:03:09.400539   57197 memcache.go:265] couldn't get current server API group list: Get "http://localhost:8080/api?timeout=32s": dial tcp 127.0.0.1:8080: connect: connection refused
The connection to the server localhost:8080 was refused - did you specify the right host or port?
akash@sky:~/mynewtest$ kubectl get pod --kubeconfig=config
Unable to connect to the server: tls: failed to verify certificate: x509: certificate signed by unknown authority
akash@sky:~/mynewtest$ kubectl get pod --kubeconfig=config --insecure-skip-tls-verify
NAME                    READY   STATUS    RESTARTS       AGE
akpo1d                  1/1     Running   0              95m
mydep-b6757d7fd-b7v99   1/1     Running   1 (144m ago)   3d
next                    1/1     Running   0              95m
akash@sky:~/mynewtest$ kubectl get svc --kubeconfig=config --insecure-skip-tls-verify
Error from server (Forbidden): services is forbidden: User "system:serviceaccount:default:monitor-sa" cannot list resource "services" in API group "" in the namespace "default
```