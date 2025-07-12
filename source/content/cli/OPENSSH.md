---
title: OPENSSH
summary: Suite of secure tunneling capabilities.
description: Suite of secure tunneling capabilities.
tags:
  - linux
---

# Remote Operations

---

### SSH


 > 
 > **<font color=red>ssh</font> myUser<font color=red>@</font>myTargetHost**</br>
 > Open a secure interactive session to the targeted host.
 > 
 > **<font color=red>ssh</font> myUser<font color=red>@</font>myTargetHost myCommand**</br>
 > Run a command in the targeted host.

 > 
 > **<font color=red>ssh</font> myUser<font color=red>@</font>myTargetHost <font color=red>-N -L</font> localhost<font color=red>:</font>1212<font color=red>:</font>myUnreachableHost<font color=red>:</font>1212**</br>
 > Create a local port forward.
 > Allows local machine to access a port on a mahcine that is in another network.
 > Scenario where local machine has access to `myTargetHost` but not to `myUnreachableHost`, while `myTargetHost` has access to local machine and `myUnreachableHost` networks.
 > 
 > **<font color=red>ssh</font> myUser<font color=red>@</font>myTargetHost <font color=red>-N -R</font> 0.0.0.0<font color=red>:</font>8080<font color=red>:</font>localhost<font color=red>:</font>80**</br>
 > Create a remote port forward.
 > Allows target machine to access a local machine port.
 > Scenario where remote machine is not allowed to open connections to local machine, but the contrary is allowed.

---

### SSH Flags


 > 
 > **<font color=red>-p</font>**</br>
 > Specify the port to connect to on the target.

 > 
 > **<font color=red>-i</font> myPrivateKeyFile**</br>
 > Connect using private key (need that target trust public key beforehand).

 > 
 > **<font color=red>-t</font>**</br>
 > Force pseudo-terminal allocation (e.g. allows connecting to a user that do not have a default shell).

 > 
 > **<font color=red>-L</font> myLocalBindAddr<font color=red>:</font>myLocalPort<font color=red>:</font>myUnreachableHost<font color=red>:</font>myUnreachableHostPort**</br>
 > Local port forward.
 > 
 > **<font color=red>-R</font> myTargetHostAddr<font color=red>:</font>myTargetHostPort<font color=red>:</font>localhost<font color=red>:</font>myLocalPort**</br>
 > Remote port forward.
 > 
 > **<font color=red>-D</font> myBindAddr<font color=red>:</font>1212**</br>
 > Dynamic port forward via specified port (ssh will act as a SOCKS proxy server).

 > 
 > **<font color=red>-N</font>**</br>
 > Do not execute a remote command (useful for just forwarding ports).
 > 
 > **<font color=red>-f</font>**</br>
 > Run in background (useful for just forwarding ports).

---

### SCP


 > 
 > **<font color=red>scp</font> /path/to/myLocalFile.txt myUser<font color=red>@</font>myTargetHost<font color=red>:</font>/destination/path/**</br>
 > Copy a local file to a remote host.

 > 
 > **<font color=red>scp -r</font> /path/to/myFolder myUser<font color=red>@</font>myTargetHost<font color=red>:</font>/destination/path/**</br>
 > Copy a folder and its content to a remote host.
 > 
 > \**<font color=red>scp -r</font> /path/to/myFolder/* myUser<font color=red>@</font>myTargetHost<font color=red>:</font>/destination/path/myFolder/\*\*</br>
 > Copy the content of a folder to a remote host.

---

### SFTP


 > 
 > **<font color=red>sftp</font> myUser<font color=red>@</font>myTargetHost**</br>
 > Create an SFTP session.

 > 
 > **<font color=red>help</font>**</br> 
 > Display help.

 > 
 > **<font color=red>pwd</font>**</br>
 > Returns remote current folder.
 > 
 > **<font color=red>lpwd</font>**</br>
 > Returns local current folder.
 > 
 > **<font color=red>ls</font>**</br>
 > Lists folders and files in remote current folder.
 > 
 > **<font color=red>lls</font>**</br>
 > Lists folders and files in local current folder.
 > 
 > **<font color=red>cd</font>**</br>
 > Changes remote directory.
 > 
 > **<font color=red>lcd</font>**</br>
 > Changes local directory

 > 
 > **<font color=red>get</font>**</br>
 > Downloads a file from server to client (-r for a directory).
 > 
 > **<font color=red>put</font>**</br>
 > Uploads a file from client to server (-r for a directory).

 > 
 > **<font color=red>mkdir</font>**</br>
 > Creates a folder in remote.
 > 
 > **<font color=red>lmkdir</font>**</br>
 > Creates a folder in local.
 > 
 > **<font color=red>rmdir</font>**</br>
 > Deletes a folder.
 > 
 > **<font color=red>rm</font>**</br>
 > Deletes a file.

 > 
 > **<font color=red>exit</font>**</br> 
 > Exit SFTP session.

# Key Management

---

### Generate


 > 
 > **<font color=red>ssh-keygen -t</font> rsa**</br>
 > Generate a OpenSSH key pair (public and private keys).

---

### Trust Keys


 > 
 > **<font color=red>ssh-copy-id</font> myUser<font color=red>@</font>myHost**</br>
 > Copy public key to target host (allows connecting with private key `-i`).
