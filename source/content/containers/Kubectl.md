---
title: Kubectl
summary: "A CLI tool for communicating with a Kubernetes cluster's control plane."
description: "A CLI tool for communicating with a Kubernetes cluster's control plane."
tags:
  - kubernetes
  - container
---

# Config

---

### Kubeconfig


 > 
 > **<font color=red>export KUBECONFIG=</font>/path/to/kubeconfig.yml**</br>
 > Export Kubeconfig path.

 > 
 > **<font color=red>kubectl config current-context</font>**</br>
 > Display current kubeconfig.
 > 
 > **<font color=red>kubectl config unset current-context</font>**</br>
 > Unset current kubeconfig.

---

### AWS EKS


 > 
 > **<font color=red>aws eks update-kubeconfig --name</font> my-cluster**</br>
 > Update `~/.kube/config` file to be able to connect to the cluster.

# Nodes

---

### Get


 > 
 > **<font color=red>kubectl get nodes</font>**</br>
 > List nodes.
 > 
 > **<font color=red>kubectl describes nodes</font> myNode**</br>
 > Return information about the node.

# Namespaces

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

# Deployments

---

### Get


 > 
 > **<font color=red>kubectl get deployments</font>**</br>
 > Show deployments.

---

### Apply


 > 
 > **<font color=red>kubctl apply -f</font> myDeployment.yml**</br>
 > Apply deployment file.
 > 
 > **<font color=red>kubctl apply -f</font> /myDeploymentsFolder**</br>
 > Apply all deployments files inside this specific folder (require `---` at the beginning of YAML files).

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

# Services

---

### Get


 > 
 > **<font color=red>kubectl get services</font>**</br>
 > Return active services.

---

### Port Forwarding

# Pods

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

---

### Run


 > 
 > **<font color=red>kubectl run</font> my-pod <font color=red>--image=</font>httpd:alpine <font color=red>--port=</font>8080**</br>
 > Start Apache Pod.
 > 
 > **<font color=red>kubectl run</font> my-pod <font color=red>--rm -it --image=</font>httpd <font color=red>-- bash</font>**</br>
 > Start Apache Pod with interactive Bash (killed when exited).

---

### Delete


 > 
 > **<font color=red>kubectl delete pod</font> my-pod  <font color=red>--now</font>**</br>
 > Delete Pod now.
 > 
 > **<font color=red>kubectl delete pod</font> my-pod <font color=red>--force</font>**</br>
 > Force delete the Pod.
 > 
 > **<font color=red>kubectl delete pods --all</font>**</br>
 > Delete all Pods.
