---
title: Helm CLI
summary: A tool for managing Charts (packages of pre-configured Kubernetes resources).
description: A tool for managing Charts (packages of pre-configured Kubernetes resources).
tags:
  - helm
  - kubernetes
  - container
---

# Repositories

---

### Explore


 > 
 > **<font color=red>helm repo list</font>**</br>
 > Show registered Charts repos.
 > 
 > **<font color=red>helm repo update</font>**</br>
 > Grab latest Charts available in registered repos.

 > 
 > **<font color=red>helm search repo</font> my-keyword**</br>
 > Look for Charts in registered repositories based on a keyword.

---

### Add


 > 
 > **<font color=red>helm repo add</font> stable https://charts.helm.sh/stable**</br>
 > Add the standard stable repo to local Helm config.
 > 
 > **<font color=red>helm repo add</font> my-repo-name https://my-repo-address/**</br>
 > Add a repo to the local Helm config .

# Charts

---

### Pull


 > 
 > **<font color=red>helm pull</font> my-chart**</br>
 > Download the chart locally.

---

### Values


 > 
 > **<font color=red>helm show values</font> my-chart**</br>
 > Display values for the chart.

---

### Validate Chart


 > 
 > **<font color=red>helm lint</font> /path/to/folder**</br>
 > Verify chart syntax and best practices.
 > 
 > **<font color=red>helm template --debug</font> /path/to/folder**</br>
 > Test chart template rendering locally.
 > 
 > **<font color=red>helm install --dry-run --debug</font> /path/to/folder <font color=red>--values</font> /path/to/valuesFiles.yml**</br>
 > Test chart template rendering locally and check potentials conflitcs on the cluster.

# Releases

---

### List


 > 
 > **<font color=red>helm list -A</font>**</br>
 > List installed releases on the kube cluster.

 > 
 > **<font color=red>helm list --pending</font>**</br>
 > List pending releases.
 > 
 > **<font color=red>helm list --uninstalling</font>**</br>
 > List releases being uninstalled.

---

### Install


 > 
 > **<font color=red>helm install</font> my-release-name my-chart <font color=red>-n</font> my-namespace**</br>
 > Install helm release.

 > 
 > **<font color=red>--version</font> 1.2.3**</br>
 > Install specific version.

 > 
 > **<font color=red>--debug</font>**</br>
 > Install helm release with debug logs.
 > 
 > **<font color=red>--wait</font>**</br>
 > Wait that resources to be in ready state to mark the relesase as successful.

 > 
 > **<font color=red>--create-namespace</font>**</br>
 > Create namespace if do not exist.

 > 
 > **<font color=red>--generate-name</font>**</br>
 > Generate a name for the deployment (don't specify my-release-name).

---

### Upgrade


 > 
 > **<font color=red>helm upgrade</font> my-release-name my-chart <font color=red>-n</font> my-namespace**</br>
 > Upgrade helm release.

---

### Uninstall


 > 
 > **<font color=red>helm uninstall</font>  my-release-name <font color=red>-n</font> my-namespace**</br>
 > Uninstall helm release.
