# terraform
terraform {
  required_providers {
    azurerm = {
      source  = "hashicorp/azurerm"
      version = "=3.0.0"
    }
  }
}


provider "azurerm" {
  features {}

  client_id = "25cdfab2-22f8-49c6-91e2-7b4a48196e87"
  subscription_id = "86f09bbd-c75d-42f2-91e7-35b45b04e81d"
  tenant_id = "1fbde232-2248-4587-aa11-d8655d6c9240"
  client_secret = "8Je8Q~-fwGZ-dcbcwPRkNKhtYeU439w8ome_mbum"

}

resource "azurerm_resource_group" "test" {
  name     = "test-resources"
  location = "West US"
}

resource "azurerm_network_security_group" "test" {
  name                = "test-security-group"
  location            = azurerm_resource_group.test.location
  resource_group_name = azurerm_resource_group.test.name
}

resource "azurerm_virtual_network" "test" {
  name                = "example-network"
  location            = azurerm_resource_group.test.location
  resource_group_name = azurerm_resource_group.test.name
  address_space       = ["10.0.0.0/16"]
  

  subnet {
    name           = "subnet1"
    address_prefix = "10.0.1.0/24"
  }

  
  tags = {
    environment = "Devlopment"
  }
}
