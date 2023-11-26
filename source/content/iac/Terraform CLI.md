---
tag: terraform
---

# Workflow

---

### Initialize

---

## tag: terraform

 > 
 > **<font color=red>terraform init</font>**</br>
 > Initialize working directory (configure the backend, install providers and modules, and create lock file).
 > 
 > **<font color=red>terraform init -backend-config=myBackendVars.tfvars</font>**</br>
 > Initialize with a backend var file.

 > 
 > **<font color=red>terraform init -upgrade</font>**</br>
 > Initialize and upgrade providers to the latest version that respects the constraint in the `required_providers` block. Update the version and signature in the lock file.

 > 
 > **<font color=red>terraform get</font>**</br>
 > Upgrade module version when you change a module's source or version (same as doing `terraform init` again).

 > 
 > **<font color=red>terraform providers</font>**</br>
 > Show providers used in the current configuration. 
 > 
 > **<font color=red>terraform providers -schema</font>**</br>
 > Print detailed schemas for the providers. 

---

### Validate and Format (optional)

---

## tag: terraform

 > 
 > **<font color=red>terraform validate</font>**</br>
 > Check for syntax errors in configuration files.

 > 
 > **<font color=red>terraform init -backend=false</font>**</br>
 > **<font color=red>terraform validate</font>**</br>
 > Validate the configuration withour accessing the backend.

 > 
 > **<font color=red>terraform fmt</font>**</br>
 > Format configuration files in current directory (print out names of modified files).
 > 
 > **<font color=red>terraform fmt -recursive</font>**</br>
 > Format configuration files in current directory and subdirectories.

---

### Plan

---

## tag: terraform

**Warning: Terraform plan files can contain sensitive data. Never commit a plan file to version control.**

 > 
 > **<font color=red>terraform plan</font>**</br>
 > Show expected changes (Execution Plan).

 > 
 > **<font color=red>terraform plan -destroy</font>**</br>
 > Show expected deletions (Destruction Plan).

Output Signification:

* `+`: Create
* `-`: Destroy
* `-/+`: Destroy and Recreate
* `~`: Update

---

### Apply

---

## tag: terraform

 > 
 > **<font color=red>terraform apply</font>**</br>
 > Run Plan, then Apply changes.

 > 
 > **<font color=red>terraform apply -replace=</font>my_resource**</br>
 > Force the replacement of a resource even if there are no changes in its configuration.

 > 
 > **<font color=red>terraform apply -parallelism=</font>12**</br>
 > Set the number of concurrent operations (default is 10).

---

### Destroy

---

## tag: terraform

 > 
 > **<font color=red>terraform destroy</font>**</br>
 > Delete provisioned infrastructure.

# Workspaces

---

### Explore


 > 
 > **<font color=red>terraform workspace list</font>**</br>
 > List current workspace. 

 > 
 > **<font color=red>terraform workspace select</font> myWorkspace**</br>
 > Change workspace.

---

### Create


 > 
 > **<font color=red>terraform workspace new</font> myWorkspace**</br>
 > Create new workspace.

---

### Delete


 > 
 > **<font color=red>terraform workspace delete</font> myWorkspace**</br>
 > Delete a workspace. Note: The `Default` workspace can't be deleted.

# State

---

### Browse State


 > 
 > **<font color=red>terraform state list</font>**</br>
 > List resources in current state.
 > 
 > **<font color=red>terraform state show myResource.myProperty</font>**</br>
 > Display resource property.

---

### Update State


 > 
 > **<font color=red>terraform state mv</font>  my_old_resource my_new_resource**</br>
 > Rename a resource.

 > 
 > **<font color=red>terraform state push</font>  my_state.json**</br>
 > Overwrite remote state with a local state file (this should be avoided).

---

### Import


 > 
 > **<font color=red>terraform refresh</font>**</br>
 > Update state to match actual remote resources. Deprecated because it is unsafe. It is an alias for `terraform apply -refresh-only -auto-approve`.

 > 
 > **<font color=red>terraform import</font> myResourceType.myResourceName cloudResourceID**</br>
 > Import a resource (add it to the state). The resource has to be defines in a tf file.

---

### Remove


 > 
 > **<font color=red>terraform state remove</font> myResourceType.myResourceName**</br>
 > Remove resource from state (the resource still exists on the target).

---

### Lock


 > 
 > **<font color=red>terraform force-unlock</font> my_lock_ID**</br>
 > Manually unlock state.

# Environment Variables


 > 
 > **<font color=red>export TF_LOG=trace</font>**</br>
 > Enable maximum verbosity (TRACE > DEBUG > INFO > WARN > ERROR).
 > 
 > **<font color=red>export TF_LOG=off</font>**</br>
 > Disable detailed logs.

 > 
 > **<font color=red>export TF_CLI_CONFIG_FILE="</font>$HOME/.terraformrc-custom<font color=red>"</font>**</br>
 > Set the location of the CLI config file.

 > 
 > **<font color=red>export TF_INPUT=0</font>**</br>
 > Disable prompts for variables that haven't had their values specified (same as `-input=false`).
