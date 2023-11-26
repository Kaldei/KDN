---
tag: terraform azure
---

# Basis

---

### Provider

## Auth Azure with Azure CLI

https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs/guides/azure_cli

````hcl
terraform {
  required_providers {
    azurerm = {
      source  = "hashicorp/azurerm"
      version = "=3.0.0"
    }
  }
}

# Configure the Microsoft Azure Provider
provider "azurerm" {
  # Optional
  subscription_id = "00000000-0000-0000-0000-000000000000"
}
````

## \[TOCHECK\] - Auth Azure with Service Principal

https://learn.microsoft.com/en-us/azure/developer/terraform/get-started-cloud-shell-bash?tabs=bash#specify-service-principal-credentials-in-a-terraform-provider-block 

````hcl
terraform {
  required_providers {
    azurerm = {
      source = "hashicorp/azurerm"
      version = "~>2.0"
    }
  }
}

provider "azurerm" {
  features {}

  subscription_id   = "<azure_subscription_id>"
  tenant_id         = "<azure_subscription_tenant_id>"
  client_id         = "<service_principal_appid>"
  client_secret     = "<service_principal_password>"
}

# Your code goes here
````

---

### Resource Group


````hcl
# Create a resource group
resource "azurerm_resource_group" "MY_RESOURCE_GROUP" {
  name     = "MY_RESOURCE_GROUP"
  location = "France Central"
}
````

---

### Virtual Network


````hcl
# Create a virtual network
# https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs/resources/virtual_network
resource "azurerm_virtual_network" "MY_NETWORK" {
  name                = "MY_NETWORK"
  address_space       = ["10.0.0.0/16"]
  resource_group_name = azurerm_resource_group.MY_RESOURCE_GROUP.name
  location            = azurerm_resource_group.MY_RESOURCE_GROUP.location
}

resource "azurerm_subnet" "MY_SUBNET" {
  name                 = "MY_SUBNET"
  resource_group_name  = azurerm_resource_group.MY_RESOURCE_GROUP.name
  virtual_network_name = azurerm_virtual_network.MY_NETWORK.name
  address_prefixes     = ["10.0.0.0/24"]
}
````

# IAM

---

### Create Service Principal (TO CHECK)

https://learn.microsoft.com/en-us/azure/developer/terraform/create-k8s-cluster-with-tf-and-aks?tabs=azure-cli

````hcl
# Create Azure AD App Registration
resource "azuread_application" "app" {
  display_name = "my-app"
  owners       = [local.current_user_id]
}

# Create Service Principal
resource "azuread_service_principal" "app" {
  application_id               = azuread_application.app.application_id
  app_role_assignment_required = true
  owners                       = [local.current_user_id]
}

# Create Service Principal password
resource "azuread_service_principal_password" "app" {
  service_principal_id = azuread_service_principal.app.id
}

# Sleep for 30 seconds to allow for propagation
# of the Service Principal creation before attempting
# to create the AKS cluster.
resource "time_sleep" "wait_30_seconds" {
  create_duration = "30s"

  depends_on = [azuread_service_principal_password.app]
}

# Output the Service Principal and password
output "sp" {
  value     = azuread_service_principal.app.id
  sensitive = true
}

output "sp_password" {
  value     = azuread_service_principal_password.app.value
  sensitive = true
}
````
