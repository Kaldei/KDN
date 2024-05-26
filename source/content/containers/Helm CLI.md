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

### Remote Repo


 > 
 > **<font color=red>helm search repo</font> my-keyword**</br>
 > Find repositories based on a keyword.
 > 
 > **<font color=red>helm repo add</font> my-repo-name https://my-repo-address**</br>
 > Add source repo to local.

---

### Local Repo


 > 
 > **<font color=red>helm repo update</font>**</br>
 > Grab latest list of available chart repos.

 > 
 > **<font color=red>helm repo list</font>**</br>
 > Show local configured chart repos.

# Chart

---

### Pull


 > 
 > **<font color=red>helm pull</font> my-chart**</br>
 > Pull a chart locally.

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

# Release

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
 > **<font color=red>--debug</font>**</br>
 > Install helm release with debug logs.
 > 
 > **<font color=red>--version</font> 1.2.3**</br>
 > Install specific version.

---

### Uninstall


 > 
 > **<font color=red>helm uninstall</font>  my-release-name <font color=red>-n</font> my-namespace**</br>
 > Uninstall helm release.
