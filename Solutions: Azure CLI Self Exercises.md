
---

# **Solutions: Azure CLI Self Exercises**

---

## **Exercise 1: Create and List a Resource Group**

### Command to Create Resource Group:
```bash
az group create --name practiceRG --location centralindia
```

### List Resource Groups:
```bash
az group list --output table
```

---

## **Exercise 2: Create Your First Linux VM**

### Command to Create VM:
```bash
az vm create \
  --resource-group practiceRG \
  --name ubuntuVM01 \
  --image UbuntuLTS \
  --size Standard_B1s \
  --admin-username devuser \
  --generate-ssh-keys
```

After successful creation, note the **public IP** from the output.

---

## **Exercise 3: Connect to the VM via SSH**

### SSH Command:
```bash
ssh devuser@<Public-IP>
```

> Replace `<Public-IP>` with the actual IP from the output.

---

## **Exercise 4: Create a Second VM**

### Command:
```bash
az vm create \
  --resource-group practiceRG \
  --name ubuntuVM02 \
  --image Ubuntu2204 \
  --size Standard_B1s \
  --admin-username devuser \
  --generate-ssh-keys
```

---

## **Exercise 5: Explore and Manage VMs**

### List VMs:
```bash
az vm list --output table
```

### Show VM Details:
```bash
az vm show --name ubuntuVM01 --resource-group practiceRG --output json
```

### Stop VM:
```bash
az vm deallocate --name ubuntuVM01 --resource-group practiceRG
```

### Start VM:
```bash
az vm start --name ubuntuVM01 --resource-group practiceRG
```

### Restart VM:
```bash
az vm restart --name ubuntuVM02 --resource-group practiceRG
```

---

## **Exercise 6: Open a Port**

### Open Port 80 (HTTP):
```bash
az vm open-port --port 80 --resource-group practiceRG --name ubuntuVM01
```

### Install Apache:
SSH into the VM first:
```bash
ssh devuser@<Public-IP>
```

Then run:
```bash
sudo apt update
sudo apt install apache2 -y
```

> Now, visit `http://<Public-IP>` in your browser. You should see the Apache default page.

---

## **Exercise 7: List Disks**

### Command:
```bash
az disk list --output table
```

---

## **Exercise 8: Clean Up Resources**

### Delete VM only:
```bash
az vm delete --name ubuntuVM02 --resource-group practiceRG --yes
```

### Delete Entire Resource Group:
```bash
az group delete --name practiceRG --yes --no-wait
```

---

