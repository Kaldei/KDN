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
