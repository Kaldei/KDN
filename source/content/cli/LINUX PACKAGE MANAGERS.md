---
title: LINUX PACKAGE MANAGERS
summary: A note about Linux packages managers.
description: A note about Linux packages managers.
tags:
  - linux
---

# Debian Based Distros

---

### APT (Advanced Package Tool) - High Level

Source repos config files: **/etc/apt/sources.list**

````
# versionCodeName examples: jammy jammy-security (for security updates only)
# packageGroup example: main
deb http://source/ versionCodeName packageGroup
````

 > 
 > **<font color=red>apt update</font>**</br>
 > Go to sources list and update packages version cache file (/var/cache/pkgcache).
 > 
 > **<font color=red>apt upgrade</font>**</br>
 > Upgrade Packages with new versions from the cache.
 > 
 > **<font color=red>apt dist-upgrade</font>**</br>
 > Stronger upgrade (some packages are told by the maintainer to not upgrade just with upgrade).
 > 
 > **<font color=red>apt-mark hold</font> myPackage**</br>
 > Do not update this package when doing upgrade.

 > 
 > **<font color=red>apt search</font> myString**</br>
 > Search package with myString in the name.
 > 
 > **<font color=red>apt info</font> myPackage**</br>
 > Give infos about a package (Version, Origin, Maintainer).

 > 
 > **<font color=red>apt remove</font> myPackage**</br>
 > Remove myPackage (only the package).

 > 
 > **<font color=red>apt install</font> myPackage**</br>
 > Install myPackage (check in the cache file).
 > 
 > **<font color=red>apt install -s</font> myPackage**</br>
 > Simulate installation.
 > 
 > **<font color=red>apt install -f</font> myPackage**</br>
 > Fix Broken (install missing dependencies).

 > 
 > **<font color=red>apt download</font> myPackage**</br>
 > Download the deb file myPackage without installing.

 > 
 > **<font color=red>apt remove</font> myPackage**</br>
 > Remove myPackage (only the package).
 > 
 > **<font color=red>apt autoremove</font> myPackage**</br>
 > Remove myPackage and dependencies.
 > 
 > **<font color=red>apt autoremove --purge</font> myPackage**</br>
 > Remove myPackage, dependencies and config files with purge.

---

### DPKG – Low Level


 > 
 > **<font color=red>dpkg -l</font>**</br>
 > Show installed packages.

 > 
 > **<font color=red>dpkg -i</font> myPackage.deb**</br>
 > Install package.

 > 
 > **<font color=red>dpkg-reconfigure</font> myPackage**</br>
 > Re-run installation configuration scripts.

# RedHat Based Distros

---

### DNF (Dandified YUM) - High Level

DNF is the modern replacement for YUM (faster and memory efficient).
Sub-commands are the same as YUM.

---

### YUM (Yellowdog Updater Modified) – High Level

Main config file: **/etc/yum.conf**
Source repos config file: **/etc/yum.repos.d/**

 > 
 > **<font color=red>yum update</font>**</br>
 > Update repositories and packages.
 > 
 > **<font color=red>yum upgrade</font>**</br>
 > Upgrade packages and remove obsolete ones.

 > 
 > **<font color=red>yum search</font> myString**</br>
 > Search package with myString in the name.

 > 
 > **<font color=red>yum install</font> myPackage**</br>
 > Install a package.

---

### RPM (Red Hat PackMan) – Low Level


 > 
 > **<font color=red>rpm query</font> myString**</br>
 > Search package with myString in the name.

 > 
 > **<font color=red>rpm -U</font> myFile.rpm**</br>
 > Install or Upgrade a package.
 > 
 > **<font color=red>rpm -i</font> myFile.rpm**</br>
 > Install a package.
 > 
 > **<font color=red>rpm -i -v -h</font> myFile.rpm**</br>
 > Install a package with verbose and loadfing bar.
