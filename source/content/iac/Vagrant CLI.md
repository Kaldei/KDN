---
title: Vagrant CLI
summary: A note about the Vagrant CLI.
description: A note about the Vagrant CLI.
tags:
  - vagrant
---

# Basis

---

### Basis


 > 
 > **<font color=red>vagrant init</font>**</br>
 > Create default Vagrant file.

 > 
 > **<font color=red>vagrant up</font>**</br>
 > Create VMs.
 > 
 > **<font color=red>vagrant reload</font>**</br>
 > Restart VMs.
 > 
 > **<font color=red>vagrant destroy</font>**</br>
 > Delete VMs.

 > 
 > **<font color=red>vagrant ssh</font>**</br>
 > Connect to VM with SSH.
 > 
 > **<font color=red>vagrant suspend</font>**</br>
 > Pause VMs.
 > 
 > **<font color=red>vagrant resume</font>**</br>
 > Unpause VMs

---

### Boxes

Boxes are ready to use Vagrant VMs. 
They can be find here: https://app.vagrantup.com/boxes/search 

 > 
 > **<font color=red>vagrant box list</font>**</br>
 > Show locally available boxes.
 > 
 > **<font color=red>vagrant box add</font> myBox**</br>
 > Download a box from Vagrant Cloud.
 > 
 > **<font color=red>vagrant box remove</font> myBox**</br>
 > Remove a local box.

# Plugins

---

### Basis


 > 
 > **<font color=red>vagrant plugin list</font>**</br>
 > Show locally available boxes.
 > 
 > **<font color=red>vagrant plugin install</font> myPlugin**</br>
 > Install a plugin.

---

### VMware Workstation

https://developer.hashicorp.com/vagrant/docs/providers/vmware/configuration 

 > 
 > **<font color=red>vagrant plugin install vagrant-vmware-desktop</font>**</br>
 > Install VMware Workstation Plugin

For it to work, it is required to install Vagrant VMware Utility:
https://developer.hashicorp.com/vagrant/docs/providers/vmware/vagrant-vmware-utility

---

### VMware ESXi

https://github.com/josenk/vagrant-vmware-esxi

 > 
 > **<font color=red>vagrant plugin install vagrant-vmware-esxi</font>**</br>
 > Install VMware ESXi plugin
 > 
 > **<font color=red>vagrant up --provider=vmware_esxi</font>**</br>
 > To use the plugin specify the provider when using Vagrant commands.
