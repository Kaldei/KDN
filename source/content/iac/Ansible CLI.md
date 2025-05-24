---
title: Ansible CLI
summary: A note about the Ansible CLI.
description: A note about the Ansible CLI.
tags:
  - ansible
---

# Commands

---

### Ansible


 > 
 > **<font color=red>ansible</font> all <font color=red>-a "</font>whoami<font color=red>"</font>**</br>
 > Execute command on all hosts specified in inventory file.

 > 
 > **<font color=red>ansible</font> all <font color=red>-m</font> ping**</br>
 > Execute a module on all hosts.
 > 
 > **<font color=red>ansible</font> all <font color=red>-m ansible.builtin.setup -a "filter=ansible_os_family"</font>**</br>
 > Return the `ansible_os_family` Ansible fact.

---

### Playbook


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

# Flags

---

### Variables


 > 
 > **<font color=red>-e</font> ansible_python_interpreter=/usr/bin/python3**</br>
 > Set additional variable.

---

### Inventory


 > 
 > **<font color=red>-i</font> myHostsFile**</br>
 > Specify inventory file to use.

 > 
 > **<font color=red>-i "</font>192.168.1.1<font color=red>,"</font>**</br>
 > Specify a host inline.
 > 
 > **<font color=red>-i "</font>localhost<font color=red>," --connection=local</font>**</br>
 > Run on localhost.

---

### User


 > 
 > **<font color=red>-u</font> myUser**</br>
 > Specify the user to use for remote connection.
 > 
 > **<font color=red>--become</font>**</br>
 > Use sudo when executing commands.

---

### Passwords


 > 
 > **<font color=red>-k</font>**</br>
 > Prompt user to enter SSH password (`--ask-pass`).
 > 
 > **<font color=red>-K</font>**</br>
 > Prompt user to enter Become password (`--ask-become-pass`).
 > 
 > **<font color=red>-J</font>**</br>
 > Prompt user to enter Secure Variables's Vault password (`--ask-vault-pass`).

---

### Misc


 > 
 > **<font color=red>-C</font>**</br>
 > Dry run, show expected output of playbook (`--check`).

 > 
 > **<font color=red>-D</font>**</br>
 > Show details of the changes (`--diff`).
