---
title: Ansible Basics
summary: A note about the basics of Ansible (Files and Structures).
description: A note about the basics of Ansible (Files and Structures).
tags:
  - ansible
---

# Files

---

### Ansible Config

Ansible config file: `ansible.cgf`

````ini
[defaults]
# Define default path to inventory file
inventory = /path/to/hosts


[ssh_connections]
# Speed up ansible commands (don’t know whyn to check)
pipelining = true
````

---

### Hosts

The Ansible `hosts` file is where targets and some parameters are specified.

````ini
[myhosts]
10.0.0.12


[myhosts:vars]
# Connect with SSH and Password
ansible_connection=ssh
ansible_port=1212
ansible_user=myUser
ansible_password=myPassword


# Connect with SSH and Private Key
ansible_connection=ssh
ansible_port=1212
ansible_user=myUser
ansible_ssh_private_key_file=/path/to/private/key


# Connect to Cisco Device (probably more config is needed)
ansible_connection=network_cli	# Cisco
ansible_network_os=ios      	#Cisco
ansible_port=1212
````

---

### Variables

A file to specify variables: `myVars.yml`

````yaml
---
	myVar: myValue
	username: myUser
	packages:
	     - neofetch
	     - htop
````

---

### Task

File used to define little units of tasks (`myTask.yml`), that can be imported in playbooks. The goal here is modularity.

````yml
- name: Update Debian Packages
  apt:
    update_cache: yes
    upgrade: yes


- name: Install Package
  package:
    name: neofetch
    state: latest
````

---

### Playbook

File that specify tasks to run on hosts: `myPlaybook.yml`

````yaml
---
- hosts: all
  become: yes

  - import_playbook: playbooks/base_clock.yml

  roles:
    - myRole

  tasks:
    - import_tasks: myTask.yml
    - name: Install Package
	  package:
	    name: neofetch
	    state: latest
````

# Playbook Structures

---

### Debug


````yml
- name: Print a simple statement
  debug:
    msg: "This is the value: {{ my_var }}"
````

---

### Condition


````yml
- name: Run the command if "epic" or "monumental" is true
	ansible.builtin.shell: echo "This certainly is epic!"
	when: epic or monumental | bool


- name: Run the command if "epic" is false
	ansible.builtin.shell: echo "This certainly isn't epic!"
	when: not epic
````

---

### Loops


````yaml
- name: Loop
  package:
    name: "{{ item }}"
    state: latest
  with_items:
      - neofetch
      - htop

````

````yaml
- name: Loop (same as above but different syntax)
  package:
    name: "{{ item }}"
    state: latest
  loop:
      - neofetch
      - htop
````

````yaml
- name: Loop with Kev Value Variables
  ansible.builtin.user:
    name: "{{ item.name }}"
    state: present
    groups: "{{ item.groups }}"
  loop:
    - { name: 'user1', groups: 'wheel' }
    - { name: 'user2', groups: 'root' }
````

---

### Register

Save task output in a variable.

````yaml
- name: Register example
   shell: "find /somedir/*.txt"
   register: find_output
````

---

### Notify & Handlers


````yaml
tasks:
	-name: Task that notify ("call") the handler
	  lineinfile:
	    dest: /etc/ssh/sshd_config
	    regexp: "^#PasswordAuthentication yes"
	    line: "PasswordAuthentication no"
	  notify: Restart SSH daemon


handlers:
  - name: Restart SSH daemon
    service:
      name: sshd
      state: restarted
````

# Ansible Facts

Ansible Facts are information about the target that can be used in conditions.
https://docs.ansible.com/ansible/latest/user_guide/playbooks_conditionals.html#commonly-used-facts 

---

### OS and Distribution


 > 
 > **<font color=red>ansible_facts\['os_family'\]</font>**</br>
 > OS Family (ex: RedHat, Debian, ...).
 > 
 > **<font color=red>ansible_facts\[‘distribution’\]</font>**</br>
 > OS Distribution (ex: RedHat can be RedHat, CentOS, Fedora, ..., and Debian can be Debian, Ubuntu, Kali, ...).

 > 
 > **<font color=red>ansible_facts\['distribution_major_version'\]</font>**</br>
 > OS major version.
