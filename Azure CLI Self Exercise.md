
---

# **Self Exercises: Azure CLI – Resource Groups & Linux VMs**

---

### **Exercise 1: Create and List a Resource Group**

- [ ] Create a resource group named `practiceRG` in the region `centralindia`.
- [ ] List all resource groups in your subscription.
- [ ] Verify `practiceRG` appears in the list.

---

### **Exercise 2: Create Your First Linux VM**

- [ ] Use the `practiceRG` to create a VM named `ubuntuVM01`.
- [ ] Use the image `UbuntuLTS` and size `Standard_B1s`.
- [ ] Use `devuser` as the admin username.
- [ ] Generate SSH keys automatically.
---

### **Exercise 3: Connect to the VM**

- [ ] Retrieve the public IP address from the CLI output.
- [ ] SSH into the VM

---

### **Exercise 4: Create a Second VM**

- [ ] Create a second VM named `ubuntuVM02` using the same `practiceRG`.
- [ ] Use the image `Ubuntu2204` this time.
- [ ] Use the same SSH key for access.

---

### **Exercise 5: Explore and Manage VMs**

- [ ] List all your VMs in a table format.
- [ ] Show detailed info of `ubuntuVM01`.
- [ ] Stop (deallocate) `ubuntuVM01`.
- [ ] Start it again.
- [ ] Restart `ubuntuVM02`.

---

### **Exercise 6: Open a Port**

- [ ] Open port 80 on `ubuntuVM01`.
- [ ] Install Apache using SSH (`sudo apt update && sudo apt install apache2 -y`).
- [ ] Access the Apache default page via the VM’s public IP in your browser.

---

### **Exercise 7: Disk Management**

- [ ] List all disks in your subscription using CLI.

---

### **Exercise 8: Clean Up**

- [ ] Delete only `ubuntuVM02`.
- [ ] Delete the entire resource group `practiceRG`.

---

