---
title: Kubectl
summary: "A CLI tool for communicating with a Kubernetes cluster's control plane."
description: "A CLI tool for communicating with a Kubernetes cluster's control plane."
tags:
  - kubernetes
  - container
---

# Basis

---

### Kubeconfig


 > 
 > **<font color=red>export KUBECONFIG=</font>/path/to/kubeconfig.yml**</br>
 > Export Kubeconfig path.
 > 
 > **<font color=red>kubectl config view</font>**</br>
 > Show configured clusters.
 > 
 > **<font color=red>kubectl config view --minify | grep namespace:</font>**</br>
 > Show current namespace.

 > 
 > **<font color=red>kubectl config current-context</font>**</br>
 > Display current context.
 > 
 > **<font color=red>kubectl config set-context --current --namespace</font> myNameSpace**</br>
 > Switch namespace.
 > 
 > **<font color=red>kubectl config unset current-context</font>**</br>
 > Unset current context.

 > 
 > **<font color=red>kubectl -context</font> my-context-name <font color=red>-n</font> my-namespace get pods**</br>
 > Set context and namespace in a command.

---

### AWS EKS Kubeconfig


 > 
 > **<font color=red>aws eks update-kubeconfig --name</font> my-cluster**</br>
 > Update `~/.kube/config` file to be able to connect to the cluster.

---

### Flags


 > 
 > **<font color=red>--no-headers</font>**</br>
 > Do not output headers.

 > 
 > **<font color=red>--as</font> myUser**</br>
 > Execute command as another user.

# Monitoring

---

### Metrics Server

**Note:** For the Metrics API to be available, `metrics-server` has to be installed on the cluster.

 > 
 > **<font color=red>kubectl top nodes</font>**</br>
 > Show nodes metrics.
 > 
 > **<font color=red>kubectl top pods</font>**</br>
 > Show pods metrics.

# Metadata

---

### Labels


 > 
 > **<font color=red>kubectl label node</font> myNode myLabel<font color=red>=</font>myValue**</br>
 > Add a Label to a Node.
 > 
 > **<font color=red>kubectl label node</font> myNode myLabel<font color=red>-</font>**</br>
 > Remove a Label from a Node.

### Label Selector


 > 
 > **<font color=red>kubectl get</font> pod <font color=red>--selector</font> myLablel<font color=red>=</font>myValue**</br>
 > Get pods based on label value.

 > 
 > **<font color=red>kubectl get</font> pod <font color=red>--selector</font> myLablel<font color=red>=</font>myValue<font color=red>,</font>myLablel2<font color=red>=</font>myValue2**</br>
 > Get pods based on multiple labels values.

# Nodes

---

### Get


 > 
 > **<font color=red>kubectl get nodes</font>**</br>
 > List nodes.
 > 
 > **<font color=red>kubectl describes nodes</font> myNode**</br>
 > Return information about the node.

---

### Unschedule


 > 
 > **<font color=red>kubectl cordon</font> myNode**</br>
 > Mark the node as unschedulable (node status will be `Ready,SchedulingDisabled`).
 > 
 > **<font color=red>kubectl uncordon</font> myNode**</br>
 > Mark the node as schedulable (node status will be `Ready`).

 > 
 > **<font color=red>kubectl drain</font> myNode**</br>
 > Mark the node as unschedulable and empty it from its pods.
 > 
 > **<font color=red>kubectl drain</font> myNode <font color=red>--ignore-daemonsets</font>**</br>
 > Allows to drain node even if there are DaemonSets (DaemonSets can create Pods that ignore unschedulable taints).
 > 
 > **<font color=red>kubectl drain</font> myNode <font color=red>--force</font>**</br>
 > Allows to drain node even if there are Pods that are not declared in the controller (Pods not in Job, DaemonSet, ReplicationSet, ...). 
 > Warning: pods that are not in the controller will be lost.

---

### Taint


 > 
 > **<font color=red>kubectl taint node</font> myNode myKey<font color=red>=</font>myValue<font color=red>:</font>myEffect**</br>
 > Add a Taint to a Node (effect can be `NoExecute`, `NoSchedule`,  `PreferNoSchedule`...)

 > 
 > **<font color=red>kubectl taint node</font> myNode myKey<font color=red>=</font>myValue<font color=red>:</font>myEffect<font color=red>-</font>**</br>
 > Remove Taint from a Node.

# Namespaces

---

### Create


 > 
 > **<font color=red>kubectl create namespace</font> myNameSpace**</br>
 > Create a namespace.

---

### Select


 > 
 > \*\*<font color=red>kubectl --all namespaces</font> get pods \*\*</br>
 > Get pods from all namespaces.
 > 
 > \*\*<font color=red>kubectl -n</font> my-namespace get pods \*\*</br>
 > Get pods from a spcific namespace.

# Networking

---

### IP Ranges Configurations


 > 
 > **<font color=red>kubectl logs -n kube-system</font> weave-net<font color=red> | grep ipalloc-range</font>**</br> 
 > Find Pods IP range configuration.
 > 
 > **<font color=red>cat /etc/kubernetes/manifests/kube-apiserver.yaml  | grep "--service-cluster-ip-range="</font>**</br>
 > Find Services IP range configuration.

# Services

---

### Get


 > 
 > **<font color=red>kubectl get services</font>**</br>
 > Return active services.

---

### Expose (imperative)


 > 
 > **<font color=red>kubectl expose</font> my-pod <font color=red>--type=</font>ClusterIP <font color=red>--port=</font>80 <font color=red>--name</font> my-service**</br>
 > Create a service of type ClusterIP.
 > 
 > **<font color=red>kubectl expose</font> my-pod <font color=red>--type=</font>NodePort <font color=red>--port=</font>80 <font color=red>--name</font> my-service**</br>
 > Create a service of type NodePort.

---

### Port Forwarding


 > 
 > **<font color=red>kubectl port-forward</font> my-pod \[HOST_PORT\]:\[POD_PORT\]**</br>
 > Create a port forward to the specified pod.

# Ingress

---

### Get


 > 
 > **<font color=red>kubectl get ingress</font>**</br>
 > Show ingress.

---

### Create (Imperative)


 > 
 > **<font color=red>kubectl create ingress</font> my-ingress <font color=red>--rule="</font>/mypath<font color=red>=</font>my-app-service<font color=red>:</font>8282"**</br>
 > Create an Ingress that route `/mypath` to the `my-app-service`.


Here are some annotations that could be usefull when using an Ingress of type Nginx.

````yml
metadata:
  annotations:
    # Allow to do /myapp -> /
    nginx.ingress.kubernetes.io/rewrite-target: /
    # Redirect HTTP traffic to HTTPS
    nginx.ingress.kubernetes.io/ssl-redirect: "true"
````

# Deployments

---

### Get


 > 
 > **<font color=red>kubectl get deployments</font>**</br>
 > Show deployments.

---

### Create (imperative)


 > 
 > **<font color=red>kubectl create</font> my-deployment <font color=red>--image=</font>httpd:alpine <font color=red>--replicas=</font>4**</br>
 > Create a deployment with 4 replicas.

---

### Apply (from file)


 > 
 > **<font color=red>kubctl apply -f</font> myDeployment.yml**</br>
 > Apply Deployment from a YAML file.
 > 
 > **<font color=red>kubctl apply -f</font> /myDeploymentsFolder**</br>
 > Apply multiple Deployments form YAML files in a folder (requires `---` at the beginning of files).

---

### Update


 > 
 > **<font color=red>kubctl set image deployment/</font>my-deployment my-container<font color=red>=</font>my-new-image**</br>
 > Change the image used in a Deployment.

 > 
 > **<font color=red>kubctl rollout status deployment/</font>my-deployment**</br>
 > Show rollout status.

---

### Delete


 > 
 > **<font color=red>kubctl delete -f</font> myDeployment.yml**</br>
 > Delete deployment.

# Pods

---

### Get


 > 
 > **<font color=red>kubectl get pods</font>**</br>
 > Get info about Pods.
 > 
 > **<font color=red>kubectl get pods -o wide</font>**</br>
 > Get more info about Pods (Node and IP).

 > 
 > **<font color=red>kubectl get pod</font> my-pod**</br>
 > Get info about one specific Pod.
 > 
 > **<font color=red>kubctl get pod</font> my-pod <font color=red>-o yaml ></font> my-pod.yml**</br>
 > Get YAML of deployed resource.

---

### Static Pods

To create a static pod, look at the path configured for `staticPodPath` in `/var/lib/kubelet/config.yaml`. Then create a manifest and move it in the specified path.

 > 
 > **<font color=red>kubectl describe pods -A | grep "Controlled By"</font>**</br>
 > Find Static Pods (they are the ones controlled by `Node/controlplane`).

---

### Run (imperative)


 > 
 > **<font color=red>kubectl run</font> webserver <font color=red>--image=</font>httpd <font color=red>--port=</font>80**</br>
 > Start Apache Pod.

 > 
 > **<font color=red>kubectl run</font> my-pod <font color=red>--image=</font>myImage <font color=red>--</font> /bin/bash**</br>
 > Run a Pod that overrides the `CMD` of the container. 
 > 
 > **<font color=red>kubectl run</font> my-pod <font color=red>--image=</font>myImage <font color=red>--command --</font> /bin/bash --myArg**</br>
 > Run a Pod that overrides the `ENTRYPOINT` and the `CMD` of the container. 
 > 
 > **<font color=red>kubectl run</font> my-pod <font color=red>--image=</font>myImage <font color=red>-rm -it --command --</font> /bin/bash --myArg**</br>
 > Run a Pod that is interactive (`-it`) and gets deleted when exited (`--rm`)

---

### Exec


 > 
 > **<font color=red>kubectl exec -it</font> my-pod <font color=red>-c</font> my-container <font color=red>--</font> /bin/bash**</br>
 > Exec a command in a container (when there is only one container `-c` is not required).

---

### Logs


 > 
 > **<font color=red>kubectl logs</font> my-pod <font color=red>-c</font> my-container**</br>
 > Show logs of the specified container (when there is only one container `-c` is not required).

 > 
 > **<font color=red>kubectl logs  -f</font> my-pod**</br>
 > Show and follows logs.

---

### Edit


 > 
 > **<font color=red>kubectl edit pod </font>myPod**</br>
 > Edit pod configuration

The only specifications that can be edited are the following: 

* `spec.containers[*].image`
* `spec.initContainers[*].image`
* `spec.activeDeadlineSeconds`
* `spec.tolerations`

---

### Delete


 > 
 > **<font color=red>kubectl delete pod</font> my-pod <font color=red></font>**</br>
 > Delete Pod.
 > 
 > **<font color=red>kubectl delete pod</font> my-pod  <font color=red>--now</font>**</br>
 > Delete Pod now.
 > 
 > **<font color=red>kubectl delete pod</font> my-pod <font color=red>--force</font>**</br>
 > Force delete the Pod.
 > 
 > **<font color=red>kubectl delete pods --all</font>**</br>
 > Delete all Pods.

# Secrets

---

### Create (imperative)


 > 
 > **<font color=red>kubectl create secret generic</font> mySecret <font color=red>--from-literal</font> my_key_1<font color=red>=</font>my_value_1 <font color=red>--from-literal</font> my_key_2<font color=red>=</font>my_value_2**</br>
 > Create a `generic` Secret.

 > 
 > **<font color=red>kubectl create secret docker-registry</font> my-private-reg-creds <font color=red>--docker-server=</font>myprivateregistry.com:5000 <font color=red>--docker-username=</font>dock_user<font color=red> --docker-password=</font>dock_password --docker-email=dock_user@myprivateregistry.com**</br> 
 > Create a `docker-registry` Secret.

Example of the usage of a `docker-registry` Secret:

````yaml
deployment
  spec:
      imagePullSecrets:
      - name: private-reg-cred
      containers:
      - image: myprivateregistry.com:5000/nginx:alpine
        imagePullPolicy: IfNotPresent
````

# Certificates

---

### Signing Requests


 > 
 > **<font color=red>kubect get certificatesigningrequests.certificates.k8s.io</font>**</br> 
 > Return Signing Requests.

 > 
 > **<font color=red>cat</font> my-signing-request.csr <font color=red>\| base64 -w 0</font>**</br>
 > Ouput base64 as only one line 

````yml
apiVersion: certificates.k8s.io/v1
kind: CertificateSigningRequest
metadata:
  name: my-singing-request
spec:
  request: LS0tLS1CRUdJTiBDRV...
  signerName: kubernetes.io/kube-apiserver-client
  usages:
    - client auth
````

 > 
 > Create a Singing Request.

 > 
 > **<font color=red>kubectl certificate approve</font> my-singing-request**</br>
 > Approve Singning Request.

---

### OpenSSL


 > 
 > **<font color=red>openssl x509 -in</font> /etc/kubernetes/pki/apiserver.crt <font color=red>-text -noout</font>**</br>
 > Output certificate content.

# RBAC

---

### Roles


 > 
 > **<font color=red>kubectl create role</font> developer <font color=red>--verb=</font>list<font color=red>,</font>create<font color=red>,</font>delete <font color=red>--resource=</font>pods**</br>
 > Create a Role (can `list`, `create`, `delete` Pods).

 > 
 > **<font color=red>kubectl create rolebinding</font> dev-user-binding <font color=red>--role=</font>developer <font color=red>--serviceaccount=</font>default:dev-user**</br>
 > Create a Binding between a Role and a Service Account.

---

### Cluster Roles


 > 
 > **<font color=red>kubectl create clusterrole</font> storage-admin <font color=red>--verb=</font>* <font color=red>--resource=</font>storageclasses <font color=red>--resource=</font>persistentvolumes*\*</br>
 > Create a Cluster Role  (can do anything on Persistant Volumes).

 > 
 > **<font color=red>kubectl create clusterrolebinding</font> myUser-storage-admin <font color=red>--clusterrole=</font>storage-admin <font color=red>--user=</font>myUser**</br>
 > Create a Binding between a Role and a User.

# Misc

---

### Get all Objects


 > 
 > **<font color=red>kubectl get all</font>**</br>
 > Get info about all objects.

---

### Get all Images


 > 
 > **<font color=red>kubectl get pods --all-namespaces -o jsonpath="{.items\[*\].spec.containers\[*\].image}" | \ </font>**
 > **<font color=red>tr -s '*:space:*' '\n' | \ </font>**  
 > **<font color=red>sort | \ </font>**
 > **<font color=red>uniq -c </font>**</br>
 > Retrieve all images used by pods in the cluster.

---

### Find Resouces API Name


 > 
 > **<font color=red>kubectl api-resources | grep</font> storage**</br>
 > Find the API name of a resource using keyword.

---

### Expose Kube-apiserver


 > 
 > **<font color=red>kubectl proxy</font>**</br>
 > Expose Kube-apiserver to localhost.

---

### Troubleshoot Containers


 > 
 > **<font color=red>crictl ps -a</font>**</br>
 > See Containers that are CRI-compatible.

 > 
 > **<font color=red>crictl logs </font>containerID**</br>
 > See Logs for a container.
