
---

# **Mini Project: Deploy a Linux VM on Azure Using Terraform**

---

### **Problem Statement**

You are hired as a Cloud Engineer for a startup that wants to begin experimenting with cloud infrastructure. Your task is to **provision a simple Ubuntu Linux Virtual Machine on Microsoft Azure using Infrastructure as Code (IaC) with Terraform**.

The startup needs:
- A **Resource Group**
- A **Virtual Network and Subnet**
- A **Public IP and NIC**
- A **Virtual Machine** running Ubuntu 18.04 LTS
- SSH access using a provided public key

This project should follow **best practices** for modular, readable, and minimal infrastructure as code using Terraform.

---

### **Goals of This Project**
- Understand how to structure Terraform files.
- Use Terraform to provision basic Azure resources.
- SSH into a Linux VM created on Azure.

---

### **Technologies Used**
- Terraform (v1.0+)
- Microsoft Azure (Free Tier)
- Azure CLI (for authentication)
- SSH (for secure access)

---

## **Solution Steps**

---

### **File Structure**
```bash
azure-vm-simple/
├── main.tf
├── variables.tf
```

---

---

### **Provider Configuration**

```hcl
provider "azurerm" {
  features {}
}
```
**Explanation**:  
This tells Terraform to use the **Azure Resource Manager (azurerm)** provider. `features {}` is a required empty block for newer versions of the provider.

---

### **Resource Group**

```hcl
resource "azurerm_resource_group" "rg" {
  name     = "simple-vm-rg"
  location = "East US"
}
```

**Explanation**:  
Creates a **Resource Group** to logically group all related resources in a specific Azure region.

---

### **Virtual Network (VNet)**

```hcl
resource "azurerm_virtual_network" "vnet" {
  name                = "simpleVNet"
  address_space       = ["10.0.0.0/16"]
  location            = azurerm_resource_group.rg.location
  resource_group_name = azurerm_resource_group.rg.name
}
```

**Explanation**:  
Defines a private virtual network (`10.0.0.0/16`) for the VM to live in. This is like your private network inside Azure.

---

### **Subnet**

```hcl
resource "azurerm_subnet" "subnet" {
  name                 = "simpleSubnet"
  resource_group_name  = azurerm_resource_group.rg.name
  virtual_network_name = azurerm_virtual_network.vnet.name
  address_prefixes     = ["10.0.1.0/24"]
}
```

 **Explanation**:  
Creates a subnet inside the VNet. Subnets divide a virtual network into smaller address spaces.

---

### **Public IP Address**

```hcl
resource "azurerm_public_ip" "pip" {
  name                = "simplePublicIP"
  location            = azurerm_resource_group.rg.location
  resource_group_name = azurerm_resource_group.rg.name
  allocation_method   = "Dynamic"
}
```

**Explanation**:  
Allocates a dynamic **public IP** for the VM, which will allow SSH access from the internet.

---

### **Network Interface (NIC)**

```hcl
resource "azurerm_network_interface" "nic" {
  name                = "simpleNIC"
  location            = azurerm_resource_group.rg.location
  resource_group_name = azurerm_resource_group.rg.name

  ip_configuration {
    name                          = "internal"
    subnet_id                     = azurerm_subnet.subnet.id
    private_ip_address_allocation = "Dynamic"
    public_ip_address_id          = azurerm_public_ip.pip.id
  }
}
```

**Explanation**:  
Creates a **network interface card (NIC)** and attaches it to the subnet and public IP.

---

### **Virtual Machine (Ubuntu)**

```hcl
resource "azurerm_linux_virtual_machine" "vm" {
  name                = "simpleVM"
  resource_group_name = azurerm_resource_group.rg.name
  location            = azurerm_resource_group.rg.location
  size                = "Standard_B1s"
  admin_username      = "azureuser"
  network_interface_ids = [azurerm_network_interface.nic.id]

  admin_ssh_key {
    username   = "azureuser"
    public_key = file(var.ssh_public_key_path)
  }

  os_disk {
    caching              = "ReadWrite"
    storage_account_type = "Standard_LRS"
  }

  source_image_reference {
    publisher = "Canonical"
    offer     = "UbuntuServer"
    sku       = "18.04-LTS"
    version   = "latest"
  }
}
```

**Explanation**:  
Creates a **Linux Virtual Machine** with:
- Size `Standard_B1s` (low-cost/free tier eligible)
- SSH key authentication (no password)
- Ubuntu 18.04 LTS image

---

### **Output Public IP**

```hcl
output "public_ip" {
  value = azurerm_public_ip.pip.ip_address
}
```

**Explanation**:  
Prints the VM’s **public IP address** after deployment so you can SSH into it.

---

### **variables.tf**

```hcl
variable "ssh_public_key_path" {
  default = "~/.ssh/id_rsa.pub"
}
```

**Explanation**:  
Stores the path to your local SSH public key used to log in to the VM.

Generate one if needed using:

```bash
ssh-keygen -t rsa -b 2048
```

---

## **How to Run**

### Step 1: Initialize Terraform

```bash
terraform init
```

### Step 2: Apply the Configuration

```bash
terraform apply
```

Type `yes` when prompted.

### Step 3: SSH into the VM

```bash
ssh azureuser@<public_ip_output>
```

(Use the public IP from the output)

---

## **Cleanup**

```bash
terraform destroy
```

---
