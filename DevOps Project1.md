---

## Phase 1: Provision Terraform Workstation (Azure Ubuntu VM)

> **Goal**: Set up a base VM on Azure that will act as both your **Terraform machine** and **Ansible control node**, and will also be the **target (localhost)** for Ansible tasks.

---

### Step-by-step:

1. Login to [Azure Portal](https://portal.azure.com)

2. Create a **new Ubuntu VM**:
   - **Name**: `terraform-vm`
   - **Region**: Choose nearest (e.g., East US)
   - **Image**: Ubuntu 20.04 LTS
   - **Size**: `Standard_B1s` (part of Azure free tier)
   - **Authentication type**: SSH public key  
   - **Inbound ports**: Allow **SSH (22)**

3. After creation, SSH into it from your local system:

```bash
ssh -i mykey.pem azureuser@<Public-IP>
```

Replace `mykey.pem` with your actual private key, and `<Public-IP>` with your VM's IP.

---

## Phase 2: Install Terraform & Ansible Inside Azure VM

> **Goal**: Prepare the VM by installing required tools.

---

### Install Terraform:

```bash
sudo apt update -y
sudo apt install -y wget unzip

# Download and install Terraform
wget https://releases.hashicorp.com/terraform/1.0.11/terraform_1.0.11_linux_amd64.zip
unzip terraform_1.0.11_linux_amd64.zip
sudo mv terraform /usr/local/bin/
terraform --version
```

> **Terraform** is used to provision cloud resources using code.

---

### Install Ansible & Python tools:

```bash
sudo apt install -y python3-pip
pip3 install --upgrade pip
pip3 install awscli boto boto3 ansible
ansible --version
```

> Ansible is used for post-deployment **configuration**, like installing packages and copying files.

---

## Phase 3: Write Terraform Code to Create a Second Azure VM

> **Goal**: Use Terraform to provision another Ubuntu VM (e.g., a web server) from inside your Terraform workstation.

---

### Create project folder:

```bash
mkdir ~/azure-terraform-project && cd ~/azure-terraform-project
```

### Generate SSH key (for the VM you're going to create):

```bash
ssh-keygen -t rsa -b 2048 -f mykey -N ""
```

> This generates `mykey` (private) and `mykey.pub` (public). The `.pub` key is injected into the new VM.

---

### `provider.tf` – Tells Terraform you're using Azure

```hcl
provider "azurerm" {
  features {}
}
```

---

### `variables.tf` – Keeps values organized and reusable

```hcl
variable "location" {
  default = "eastus"
}
variable "resource_group_name" {
  default = "quickkart-rg"
}
variable "admin_username" {
  default = "azureuser"
}
```

---

### `main.tf` – The actual infrastructure setup

```hcl
# Resource Group
resource "azurerm_resource_group" "main" {
  name     = var.resource_group_name
  location = var.location
}

# Virtual Network and Subnet
resource "azurerm_virtual_network" "main" {
  name                = "quickkart-vnet"
  address_space       = ["10.0.0.0/16"]
  location            = var.location
  resource_group_name = var.resource_group_name
}

resource "azurerm_subnet" "main" {
  name                 = "quickkart-subnet"
  virtual_network_name = azurerm_virtual_network.main.name
  address_prefixes     = ["10.0.1.0/24"]
  resource_group_name  = var.resource_group_name
}

# Network Security Group with SSH & HTTP allowed
resource "azurerm_network_security_group" "main" {
  name     = "quickkart-nsg"
  location = var.location
  resource_group_name = var.resource_group_name

  security_rule {
    name                       = "AllowSSH"
    priority                   = 100
    direction                  = "Inbound"
    access                     = "Allow"
    protocol                   = "Tcp"
    source_port_range          = "*"
    destination_port_range     = "22"
    source_address_prefix      = "*"
    destination_address_prefix = "*"
  }

  security_rule {
    name                       = "AllowHTTP"
    priority                   = 101
    direction                  = "Inbound"
    access                     = "Allow"
    protocol                   = "Tcp"
    source_port_range          = "*"
    destination_port_range     = "80"
    source_address_prefix      = "*"
    destination_address_prefix = "*"
  }
}

# Public IP
resource "azurerm_public_ip" "main" {
  name                = "quickkart-public-ip"
  location            = var.location
  resource_group_name = var.resource_group_name
  allocation_method   = "Dynamic"
}

# NIC
resource "azurerm_network_interface" "main" {
  name                = "quickkart-nic"
  location            = var.location
  resource_group_name = var.resource_group_name

  ip_configuration {
    name                          = "internal"
    subnet_id                     = azurerm_subnet.main.id
    private_ip_address_allocation = "Dynamic"
    public_ip_address_id          = azurerm_public_ip.main.id
  }

  network_security_group_id = azurerm_network_security_group.main.id
}

# Linux VM (Web Server)
resource "azurerm_linux_virtual_machine" "main" {
  name                = "quickkart-webvm"
  location            = var.location
  resource_group_name = var.resource_group_name
  size                = "Standard_B1s"
  admin_username      = var.admin_username

  network_interface_ids = [
    azurerm_network_interface.main.id,
  ]

  admin_ssh_key {
    username   = var.admin_username
    public_key = file("mykey.pub")
  }

  disable_password_authentication = true

  os_disk {
    caching              = "ReadWrite"
    storage_account_type = "Standard_LRS"
  }

  source_image_reference {
    publisher = "Canonical"
    offer     = "0001-com-ubuntu-server-focal"
    sku       = "20_04-lts"
    version   = "latest"
  }
}
```

---

### Run Terraform commands:

```bash
terraform init       # One-time plugin setup
terraform fmt        # Format code
terraform validate   # Validate syntax
terraform plan       # Preview resources to be created
terraform apply      # Deploy infrastructure
```

---

## Phase 4: Use Ansible to Configure Apache on Localhost

> **Goal**: Use Ansible to install a web server and copy a webpage on the *same* VM where Ansible is running (localhost).

---

### Create Ansible folder:

```bash
mkdir ~/ansible && cd ~/ansible
```

---

### Create `hosts` inventory file:

```ini
[local]
localhost ansible_connection=local
```

> This tells Ansible to use the current machine itself as the target.

---

### Create `install-apache.yml` Ansible Playbook:

```yaml
---
- name: Install Apache and deploy index page
  hosts: local
  become: yes

  tasks:
    - name: Install Apache
      apt:
        name: apache2
        state: present
        update_cache: yes

    - name: Copy index.html
      copy:
        src: index.html
        dest: /var/www/html/index.html
        owner: www-data
        group: www-data
        mode: '0644'

    - name: Start Apache service
      service:
        name: apache2
        state: started
        enabled: true
```

---

### Create `index.html`:

```html
<html>
  <body>
    <h1>DevOps Project!</h1>
  </body>
</html>
```

---

### Run the playbook:

```bash
ansible-playbook -i hosts install-apache.yml
```

---

## Final Step: Verify Web Page

Open a browser and go to:

```
http://<Public-IP-of-this-VM>
```

You should see:

> `DevOps Project!`

---

