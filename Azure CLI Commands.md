---

## **1. Create a Resource Group**

```bash
az group create --name myResourceGroup --location eastus
```

- `--name` → Name of the Resource Group.
- `--location` → Azure Region (e.g., eastus, centralindia).

---

## **2. List Resource Groups**

```bash
az group list --output table
```

---

## **3. Create a Linux Virtual Machine**

```bash
az vm create \
  --resource-group myResourceGroup \
  --name myLinuxVM \
  --image UbuntuLTS \
  --size Standard_B1s \
  --admin-username azureuser \
  --generate-ssh-keys
```

- `--image` → Use UbuntuLTS or specific versions like `Ubuntu2204`.
- `--generate-ssh-keys` → Automatically generates and stores keys in `~/.ssh/`.

---

## **4. Connect to the VM via SSH**

```bash
ssh azureuser@<Public-IP-Address>
```

> Replace `<Public-IP-Address>` with the actual IP from the VM creation output.

---

## **5. Create Another VM in Same Resource Group**

```bash
az vm create \
  --resource-group myResourceGroup \
  --name secondLinuxVM \
  --image UbuntuLTS \
  --size Standard_B1s \
  --admin-username azureuser \
  --generate-ssh-keys
```

---

## **6. List All Virtual Machines**

```bash
az vm list --output table
```

---

## **7. Show VM Details**

```bash
az vm show \
  --name myLinuxVM \
  --resource-group myResourceGroup \
  --output json
```

---

## **8. Manage VM Power States**

- **Start a VM**

  ```bash
  az vm start --name myLinuxVM --resource-group myResourceGroup
  ```

- **Stop/Deallocate a VM**

  ```bash
  az vm deallocate --name myLinuxVM --resource-group myResourceGroup
  ```

- **Restart a VM**

  ```bash
  az vm restart --name myLinuxVM --resource-group myResourceGroup
  ```

- **Delete a VM**

  ```bash
  az vm delete --name myLinuxVM --resource-group myResourceGroup --yes
  ```

---

## **9. Open Network Ports (e.g., HTTP - Port 80)**

```bash
az vm open-port \
  --port 80 \
  --resource-group myResourceGroup \
  --name myLinuxVM
```

---

## **10. Manage Disks**

- **List All Disks**

  ```bash
  az disk list --output table
  ```

---

## **11. Clean Up Resources**

```bash
az group delete --name myResourceGroup --yes --no-wait
```

- `--no-wait` → Returns immediately without waiting for deletion to complete.

---
