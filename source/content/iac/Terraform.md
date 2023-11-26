---
tag: terraform
---

# Files

---

### Terraform Directory

---

## tag: terraform

* This directory is used to store the project's providers and modules.
* It contains two subdirectories: `modules` and `providers`.

---

### Manage Providers Version

---

## tag: terraform

* **[.terraform.lock.hcl](https://developer.hashicorp.com/terraform/language/files/dependency-lock)** :
  
  * Used to lock dependencies (providers and modules) versions.
  * To be included in the VSC.
  * By default, Terraform will attempt to download the provider version specified by the lock file.  If the lock file does not exist, Terraform will use the `required_providers` block.  If neither exists, Terraform will download the latest provider version.
* **terraform.tf**: 
  
  * Contain the `terraform` block.

---

### State

---

## tag: terraform

* **terraform.tfstate**
  * Stores the IDs and properties of the resources
  * Can contain credentials

**Note: Descriptions (of variables outputs, ...) are not stored in the state file.**

---

### CLI Config File

---

## tag: terraform

* Windows: `%APPDATA%\terraform.rc`
* Others: `~/.terraformrc`

---

### Resources Files

---

## tag: terraform

* **main.tf**: Deploy resources using providers.

# Variables

---

### Precedence

Terraform loads variables in the following order, with **later sources taking precedence over earlier ones**:

* Environment variables
* The `terraform.tfvars` file, if present.
* The `terraform.tfvars.json` file, if present.
* Any `*.auto.tfvars` or `*.auto.tfvars.json` files, processed in lexical order of their filenames.
* Any `-var` and `-var-file` options on the command line, in the order they are provided. (This includes variables set by a Terraform Cloud workspace.)

---

### Variables

---

## tag: terraform

All attributes in a variable block are optional.

Here is an example of a String variable:

````hcl
variable "my_map_variable" {
	type          = string             # Type of the variable
	defautl       = "my_value"         # Default value for the varaible
	descritption  = "This a variable"  # Descritpion
	
	# Warning: the value will still be in the state file
    sensitive     = true               # Do not show this value in output 
    validation    = ...                # Constraint or condition on the varaible
}
````

Here is an example of a Map Variable:

````hcl
variable "my_map_variable" {
	type = map
	my_map = {key1 = "value1", key2 = "value2", key3 = "value3"}
}

# Access a value
ressource "my_resource_type" "my_resource_name"{
	...
	my_value = my_map_variable.my_map[key1]
}
````

---

### Variable Provisioning

---

## tag: terraform

There are 3 ways to provision variables

#### Variables Files

In **my_file.tf**:

````hcl
variable "my_variable" {

}
````

In **my_variables_file.tfvars**:

````hcl
my_variable = "my_value"
````

Then use `-var-file="my_variables_file.tfvars"` in the CLI.

Notes: 

* Variables in the `variables.tf` files are "required". Terraform will not run if these variables do not have values.\`
* Terraform load by automatically default variables files:
  * that are named exactly `terraform.tfvars` or `terraform.tfvars.json`.
  * any files with names ending in `.auto.tfvars` or `.auto.tfvars.json`.

#### CLI Parameter

If a variable is used, but no value is attributed to it, the CLI will ask to enter a value. 
The value can also directly be passed with the command with `-var="my_var=my_value"` or by ).

#### Environment Variables

Create environment variables starting with `TF_VAR_`:

````bash
export TF_VAR_myVar=myValue
````

---

### Local Variables

---

## tag: terraform

Local variables are only accessible within the module they are declared.

````hcl
locals {
	my_varaible_1 = "my_value_1"
	my_varaible_2 = "my_value_2"
	
	my_varaible_3 = {
		my_sub_varaible_1 = "my_value_3"
		my_sub_varaible_2 = "my_value_4"
	}
}
````

Then in resources, use the following:

````hcl
ressource "my_resource_type" "my_resource_name"{
	...
	
	my_parameter1 = local.my_varaible_1
	my_parameter2 = local.my_varaible_1
	my_parameter_list = local.my_varaible_3
}
````

# Blocks

---

### Terraform

---

## tag: terraform

The `terraform` block contains the settings including:

* `required_providers` block: specifies the provider local name, the source address, and the version.

#### Required Providers

By default, Terraform will attempt to download the provider version specified by the lock file.  If the lock file does not exist, Terraform will use the `required_providers` block.  If neither exists, Terraform will download the latest provider version.

````hcl
terraform {
  required_providers {
    azurerm = {
      source  = "hashicorp/azurerm"
      version = "=3.0.0"
    }
  }
}
````

---

### Provider

This block contains providers configurations.

````hcl
provider "my_provider" {
	...
}
````

When you need to use the same provider but with different parameters, it is required to specify aliases (otherwise Terraform will not be able to know which provider to use). 
And then specify the alias in resource blocks.

````hcl
provider "my_provider" {
  ...
  alias = "my_provider_alias"
}


ressource "my_resource_type" "my_resource_name"{
	...
	provider = my_provider.my_provider_alias
}
````

---

### Backend

---

## tag: terraform

Note: When a change is made to the backend configuration, it is required to re-run `terraform init`.

#### Local Backend

When there is no `cloud` or `backend` Terraform defaults to the local backend. The local backend can be explicitly described like this (optional):

````hcl
terraform {
  backend "local" {
    path = "relative/path/to/terraform.tfstate"
  }
}
````

#### Remote Backends

Available Remote Backends:

* azurerm
* consul
* cos
* gcs
* http
* Kubernetes
* oss
* pg
* s3

Backend that support State Storage with default locking:

* azurem
* gcs

#### Terraform Cloud Backend

https://developer.hashicorp.com/terraform/tutorials/cloud/cloud-migrate
If the `cloud` block is present, Terraform will integrate with Terraform Cloud and create a Terraform Cloud workspace with the name specified in the block.

Warning: For the Cloud backend to work, it is required to set the deployment environment credentials in the Variables section of the workspace on Terraform Cloud.

````hcl
terraform {
  backend {
	# Organization name can be found on Terraform Cloud
    organization = "my-organization-name"
    workspaces {
      name = "my-workspace"
    }
  }
}
````

1. 
    > 
    > **<font color=red>terraform login</font>**</br>

 > 
 > Login to Terraform Cloud.

2. 
    > 
    > **<font color=red>terraform init</font>**</br>

 > 
 > Reinitialize configuration, create the `my-workspace` workspace in Terraform Cloud and migrate state to Terraform Cloud.

3. 
    > 
    > **<font color=red>rm terraform.tfstate</font>**</br>

 > 
 > Delete local Terraform State.

---

### Outputs

---

## tag: terraform

Outputs are used for showing information to the admin and passing information between modules.

````hcl
output "my_output" {
	value = my_ressource.my_attribute
	description  = "This an output"
	
	# Warning: the value will still be in the state file
    sensitive     = true               # Do not show this value in output 
}
````

---

### For In Structure

---

## tag: terraform

````hcl
output "my_output" {
  value = { for subnet in aws_subnet.public : subnet.tags.Name => subnet.id }
}
````

````hcl
my_output = {
  subnet_public_0 = "subnet-0fb6244694b0541cc"
  subnet_public_1 = "subnet-01fee6936ba518b49"
  subnet_public_2 = "subnet-0399dad1114e521aa"
}
````

---

### Resource

---

## tag: terraform

Define the resource.
The ID of the resource is `my_ressource_type.my_ressource_name`

````hcl
ressource "my_ressource_type" "my_ressource_name" {}
````

# Functions

---

### String Functions


 > 
 > **<font color=red>upper("</font>myString<font color=red>")</font>**</br>
 > Return uppercased string.

---

### Collection Functions


 > 
 > **<font color=red>element(</font>list<font color=red>,</font> index<font color=red>)</font>**</br>
 > Return an element in a list by its index.

 > 
 > **<font color=red>zipmap(</font>keyslist<font color=red>,</font> valueslist<font color=red>)</font>**</br>
 > Create a map from a list of keys and a list of values

# Meta-Arguments

---

The `count` meta-argument is used to create a defined number of instances of the resource or module.

# Terraform Cloud

VCS that can be added to Terraform cloud private registry:

* GitHub
* GitLab
* Bitbucket
* Azure DevOps

 > 
 > **<font color=red>terraform login</font>**</br>
 > Login to Terraform Cloud.
 > 
 > **<font color=red>terraform logout</font>**</br>
 > Logout form Terraform Cloud.

Terraform Cloud Workspace specific features:

* Access controls for state data.
* Cost estimation and alerts.

Terraform Cloud features:

* Remote state storage
* Web UI

# Terraform Enterprise

![Terragorm-Basis-Entreprise-OS.png](../../attachments/Terragorm-Basis-Entreprise-OS.png)

Terraform Enterprise use Postgresql as a backend.

# Policy as Code

Policy as Code has the following benefits:

* Sandboxing
* Codification
* Version Control
* Testing
* Automation

# Plugins

* Can only be written in Go.
