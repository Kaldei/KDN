---
title: Ansible CLI
summary: A note about the Ansible CLI.
description: A note about the Ansible CLI.
tags:
  - ansible
---

# CLI

---

### Basis


 > 
 > **<font color=red>ansible all -m ping</font>**</br>
 > Check if all hosts (specified in the inventory file) are reachable.
 > 
 > **<font color=red>ansible</font> myHosts <font color=red>-a "</font>whoami<font color=red>"</font>**</br>
 > Execute command on myHosts (specified in the inventory file).

 > 
 > **<font color=red>ansible-playbook</font> myPlaybook.yml**</br>
 > Execute a playbook.

---

### Inventory


 > 
 > **<font color=red>ansible-inventory -i</font> myHostsFile <font color=red>--list</font>**</br>
 > List hosts in the inventory.
 > 
 > **<font color=red>ansible-inventory -i</font> myHostsFile <font color=red>--list --yaml --output</font> myHostsFile.yml**</br>
 > Convert inventory file format form INI to YAML.

---

### Vault


 > 
 > **<font color=red>ansible-vault create</font> secret.yml**</br>
 > Create a secure file (secured by password) to store secrets.
 > 
 > **<font color=red>ansible-vault edit</font> secret.yml**</br>
 > Edit the secure file.

---

### Flags


 > 
 > **<font color=red>-i</font>**</br>
 > Specify inventory file to use.

 > 
 > **<font color=red>-u</font> myUser**</br>
 > Execute command as myUser.
 > 
 > **<font color=red>-k</font>**</br>
 > Prompt user to enter SSH password.

 > 
 > **<font color=red>--become</font>**</br>
 > Use sudo when executing commands.
 > 
 > **<font color=red>-K</font>**</br>
 > Prompt user to enter Become password.

 > 
 > **<font color=red>---ask-vault-pass</font>**</br>
 > Prompt user to enter Secure Variables's Vault password.

 > 
 > **<font color=red>-c</font>**</br>
 > Show expected output of playbook (`--check`).
 > 
 > **<font color=red>-d</font>**</br>
 > Show details of the changes (`--diff`).
