---
title: Ansible Modules
summary: A note about the Ansible Modules.
description: A note about the Ansible Modules.
tags:
  - ansible
---

# System

---

### Update


````yaml
- name: Update packages (Fedora)
  dnf:
    name: “*”
    state: lastest
````

````yaml
- name: Update packages (Debian)
  apt:
    update_cache: yes
    upgrade: yes
````

---

### Install Packages


````yaml
-name: Install packages
  package:
    name:
      - neofetch
      - htop
    state: latest
````

---

### Restart Service


````yaml
-name: Restart SSH daemon
  service:
    name: sshd
    state: restarted
````

# Files

---

### Replace Line in a File


````yaml
-name: Disable SSH password auth
  lineinfile:
    dest: /etc/ssh/sshd_config
    regexp: "^#PasswordAuthentication yes"
    line: "PasswordAuthentication no"
````

---

### Copy File


````yml
  - name: Install Vault service file
	ansible.builtin.copy:
	  src: ../config_files/vault/vault.service
	  dest: /etc/systemd/system/vault.service
	  owner: vault
	  group: vault
	  mode: '0660'
````

````yml
	- name: Install GitLab config file
	  ansible.builtin.copy:
	    dest: /etc/gitlab/gitlab.rb
	    owner: root
	    group: root
	    mode: '0600'
	    content : |
		external_url 'https://{{ inventory_hostname }}'
		letsencrypt['enable'] = true
````

# Services

---

### Disable SSH


````yaml
-name: Diable SSH password auth
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

---

### Docker

\#docker 

````yaml
- name: Pull Docker Image
  docker_image:
    name: ubuntu
````

````yaml
- name: Build Docker Image (Deprecated?)
  docker_image:
    path: /path/to/Dockerfile
    name: myImageName
````

````yaml
- name: Create/Start Docker Container
  docker_container:
    name: myContainerName
    image: myImage
    container_default_behavior: no_defaults
    state: started
    ports:
      - “80:80”
    tty: true
    detach: true
````
