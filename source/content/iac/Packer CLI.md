---
title: Packer CLI
summary: A note about the Packer CLI.
description: A note about the Packer CLI.
tags:
  - packer
---

# Workflow

---

### Initialize


 > 
 > **<font color=red>packer init -var-file</font> .\variables.json .\myUbuntu.json**</br>
 > Initialize the directory (download plugins, ...).

---

### Validate and Format (optional)


 > 
 > **<font color=red>packer validate -var-file</font> .\variables.json .\myUbuntu.json**</br>
 > Validate config file.

 > 
 > **<font color=red>packer fmt -var-file</font> .\variables.json .\myUbuntu.json**</br>
 > Format config file.

---

### Build


 > 
 > **<font color=red>packer build -var-file</font> .\variables.json .\myUbuntu.json**</br>
 > Build config file.

# Misc

---

### Convert from JSON to HCL


 > 
 > **<font color=red>packer hcl2_upgrade</font> myUbuntu.json**</br>
 > Convert JSON file to HCL.
