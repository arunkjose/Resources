

## Create a Resource Group

```bash
az group create --name myResourceGroup --location eastus
```

### 
- `az group create` → Command to create a resource group.
- `--name` → The name of your resource group (`myResourceGroup`).
- `--location` → Azure region where the resources will be created (`eastus` is an example; you can use others like `centralindia`, `westeurope`, etc.).

---

## Create a Linux Virtual Machine

```bash
az vm create \
  --resource-group myResourceGroup \
  --name myLinuxVM \
  --image UbuntuLTS \
  -- size Standard_B1s \
  --admin-username azureuser \
  --generate-ssh-keys
```

### Explanation:
- `az vm create` → Command to create a virtual machine.
- `--resource-group` → Use the RG we created (`myResourceGroup`).
- `--name` → Name of the VM (`myLinuxVM`).
- `--image` → OS image (`UbuntuLTS` is the latest Ubuntu Long-Term Support version).
- `--admin-username` → Username to log into the VM (`azureuser` in this case).
- `--generate-ssh-keys` → Automatically creates SSH key pair (stored in `~/.ssh/`).

---

## Connect to the VM

Once the VM is created, Azure CLI will output the **public IP address**.

Use it to SSH into the VM:

```bash
ssh azureuser@<Public-IP-Address>
```

Replace `<Public-IP-Address>` with the actual IP shown in the previous output.

---
### Create Another VM in Same RG
```bash
az vm create \
  --resource-group myResourceGroup \
  --name secondLinuxVM \
  --image UbuntuLTS \
  --admin-username azureuser \
  --generate-ssh-keys
```

### List All VMs in Your Subscription
```bash
az vm list --output table
```

---

### Show Details of a Specific VM
```bash
az vm show --name myLinuxVM --resource-group myResourceGroup --output json
```

---

### Start a Stopped VM
```bash
az vm start --name myLinuxVM --resource-group myResourceGroup
```

---

### Stop (Deallocate) a VM
```bash
az vm deallocate --name myLinuxVM --resource-group myResourceGroup
```

---

### Restart a VM
```bash
az vm restart --name myLinuxVM --resource-group myResourceGroup
```

---

### Delete a VM (⚠️ Permanently deletes the VM, keep the disk if needed)
```bash
az vm delete --name myLinuxVM --resource-group myResourceGroup --yes
```

---

## NETWORK & SECURITY PRACTICE

### Open a Port (e.g., Port 80 for Web Server)
```bash
az vm open-port --port 80 --resource-group myResourceGroup --name myLinuxVM
```

---

## STORAGE & DISK

### List All Disks
```bash
az disk list --output table
```

---



### Cleanup Practice
```bash
az group delete --name myResourceGroup --yes --no-wait
```
