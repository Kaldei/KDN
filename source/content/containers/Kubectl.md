---
title: Kubectl
summary: "A CLI tool for communicating with a Kubernetes cluster's control plane."
description: "A CLI tool for communicating with a Kubernetes cluster's control plane."
tags:
  - kubernetes
  - container
---

# Basis

### Kubeconfig


 > 
 > **<font color=red>export KUBECONFIG=</font>/path/to/kubeconfig.yml**</br>
 > Export Kubeconfig path.
 > 
 > **<font color=red>kubectl config view</font>**</br>
 > Show configured clusters.

 > 
 > **<font color=red>kubectl config current-context</font>**</br>
 > Display current kubeconfig.
 > 
 > **<font color=red>kubectl config unset current-context</font>**</br>
 > Unset current kubeconfig.

 > 
 > **<font color=red>kubectl -context</font> my-context-name -n <font color=red>my-namespace</font> get pods**</br>
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
 > Do not output headers

# Node

---

### Get


 > 
 > **<font color=red>kubectl get nodes</font>**</br>
 > List nodes.
 > 
 > **<font color=red>kubectl describes nodes</font> myNode**</br>
 > Return information about the node.

---

### Unschdule


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
 > Allows to drain node even if there are DaemonSets (DaemonSet can create Pods that ignore unschedulable taints).
 > 
 > **<font color=red>kubectl drain</font> myNode <font color=red>--force</font>**</br>
 > Allows to drain node even if there are Pods that are not declared in the controller (pods not in Job, DaemonSet, ReplicationSet, ...). Warning: pods that are not in the controller will lost.

---

### Taint


 > 
 > **<font color=red>kubectl taint node</font> myNode myKey<font color=red>=</font>myValue<font color=red>:</font>myEffect**</br>
 > Add a Taint to a Node (effect can be `NoExecute`, `NoSchedule`,  `PreferNoSchedule`...)

 > 
 > **<font color=red>kubectl taint node</font> myNode myKey<font color=red>=</font>myValue<font color=red>:</font>myEffect<font color=red>-</font>**</br>
 > Remove Taint from a Node.

# Namespace

---

### Config


 > 
 > **<font color=red>kubectl config set-context --current --namespace</font> myNameSpace**</br>
 > Switch namespace.
 > 
 > **<font color=red>kubectl config view --minify | grep namespace:</font>**</br>
 > Show current namespace.

---

### Create


 > 
 > **<font color=red>kubectl create namespace</font> myNameSpace**</br>
 > Create a namespace.

# Deployment

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
 > Apply deployment file.
 > 
 > **<font color=red>kubctl apply -f</font> /myDeploymentsFolder**</br>
 > Apply all deployments files inside this specific folder (require `---` at the beginning of YAML files).

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

# Ingress

---

### Get


 > 
 > **<font color=red>kubectl get ingress</font>**</br>
 > Show ingress.

# Service

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

# Pod

---

### Get


 > 
 > **<font color=red>kubectl get pods</font>**</br>
 > Get info about pods.
 > 
 > **<font color=red>kubectl get pods -o wide</font>**</br>
 > Get more info about pods (Node and IP).

 > 
 > **<font color=red>kubectl get pods --all namespaces</font>**</br>
 > Get pods from all namespaces.
 > 
 > **<font color=red>kubectl get pods -n</font> my-namespace**</br>
 > Get pods from a spcific namespace.

 > 
 > **<font color=red>kubectl get pod</font> my-pod**</br>
 > Get info about one specific pod.

 > 
 > **<font color=red>kubectl top pods</font>**</br>
 > Show metrics about pods (requires Metrics Server to be installed on the cluster).

---

### Run (imperative)


 > 
 > **<font color=red>kubectl run</font> my-pod <font color=red>--image=</font>myImage <font color=red>--</font> /bin/bash**</br>
 > Run a pod that overrides the `CMD` of the container. 
 > 
 > **<font color=red>kubectl run</font> my-pod <font color=red>--image=</font>myImage <font color=red>--command --</font> /bin/bash --myArg**</br>
 > Run a pod that overrides the `ENTRYPOINT` and the `CMD` of the container. 

 > 
 > **<font color=red>kubectl run</font> webserver <font color=red>--image=</font>httpd <font color=red>--port=</font>8080**</br>
 > Start Apache Pod.
 > 
 > **<font color=red>kubectl run</font> webserver <font color=red>--rm -it --image=</font>httpd <font color=red>-- bash</font>**</br>
 > Start Apache Pod with interactive Bash (killed when exited).

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

### Metrics


 > 
 > **<font color=red>kubectl top pods</font>**</br>
 > Show pods metrics (`metrics-server` has to be installed on the cluster).

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

# Labels

---

### Selector


 > 
 > **<font color=red>kubectl get</font> pod <font color=red>--selector</font> myLablel<font color=red>=</font>myValue**</br>
 > Get pods based on label value.

 > 
 > **<font color=red>kubectl get</font> pod <font color=red>--selector</font> myLablel<font color=red>=</font>myValue<font color=red>,</font>myLablel2<font color=red>=</font>myValue2**</br>
 > Get pods based on multiple labels values.

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

# Misc

---

### Get all Objects


 > 
 > **<font color=red>kubectl get all</font>**</br>
 > Get info about objects.

---

### Get all Images


 > 
 > **<font color=red>kubectl get pods --all-namespaces -o jsonpath="{.items\[*\].spec.containers\[*\].image}" | \ </font>**
 > **<font color=red>tr -s '*:space:*' '\n' | \ </font>**  
 > **<font color=red>sort | \ </font>**
 > **<font color=red>uniq -c </font>**</br>
 > Retrieve all images used by pods in the cluster.

---

### Expose Kube-apiserver


 > 
 > **<font color=red>kubectl proxy</font>**</br>
 > Expose Kube-apiserver to localhost.
