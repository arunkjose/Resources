---

## Lab Guide: Automating Ubuntu VM Creation on Azure

---

### **Pre-Requisites**

| Tool            | Cloud Shell | Local Machine       |
|-----------------|-------------|---------------------|
| Azure CLI       | Installed | Must install     |
| jq              | Installed | Must install     |
| Logged in Azure | Already   | Run `az login`   |

---

### Step-by-Step Instructions

#### Open Azure Cloud Shell
- Go to [https://shell.azure.com](https://shell.azure.com)  
- Or click the Cloud Shell icon in the [Azure Portal](https://portal.azure.com)

> Select **Bash** if prompted.

---

#### Create the Script File

```bash
vi create_vm.sh
```

Paste the following content:

```bash
#!/bin/bash

# Variables
RG_NAME="autoRG"
VM_NAME="autoVM"
LOCATION="eastus"
ADMIN_USER="autoUser"

# Create Resource Group
az group create --name $RG_NAME --location $LOCATION

# Create VM
az vm create \
  --resource-group $RG_NAME \
  --name $VM_NAME \
  --image UbuntuLTS \
  --size Standard_B1s \
  --admin-username $ADMIN_USER \
  --generate-ssh-keys \
  --output json > vm_output.json

# Open Ports
az vm open-port --port 22 --resource-group $RG_NAME --name $VM_NAME
az vm open-port --port 80 --resource-group $RG_NAME --name $VM_NAME

# Extract and show Public IP
PUBLIC_IP=$(jq -r '.publicIpAddress' vm_output.json)
echo "Public IP: $PUBLIC_IP"
```

Save and exit:  
- Press `esc`, then `:wq` to save & exit

---

#### Make the Script Executable

```bash
chmod +x create_vm.sh
```

---

#### Run the Script

```bash
./create_vm.sh
```

---

#### Check the Output

After the script runs, you will see output like:

```bash
Public IP: 20.123.45.67
```

This is the IP address of your new VM.

---

#### Connect to the VM

If you’re using **Cloud Shell**:
```bash
ssh autoUser@<Public-IP>
```
---

### Clean Up Resources

To delete everything created by the script:

```bash
az group delete --name autoRG --yes --no-wait
```

---


