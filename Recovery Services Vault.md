---

## **LAB: Backup & Restore a Linux VM using Recovery Services Vault**

### Scenario:
You manage a **Linux VM** in Azure. The company wants **daily backups** and the ability to **recover specific files** when needed.

---

 

---

### **Pre-requisites:**
- A valid Azure **Free Tier subscription**

---

## Step 1: Create a Linux VM

1. Go to [Azure Portal](https://portal.azure.com)
2. In the top search bar, type and open **Virtual Machines**
3. Click **+ Create** → **Azure Virtual Machine**
4. Fill in the basic details:
   - **Subscription**: Free Trial  
   - **Resource Group**: `startup-lab-rg` (or create one)
   - **Virtual Machine Name**: `linux-webserver`
   - **Region**: Choose closest to you (note this for later)
   - **Image**: Ubuntu 20.04 LTS  
   - **Size**: B1s (Free Tier eligible)
   - **Authentication type**: Password or SSH (choose SSH for better security)
   - **Username**: `azureuser`
   - **Password/SSH Key**: Your choice  
5. Allow **HTTP (port 80)** and **SSH (port 22)** under **Inbound Ports**
6. Click **Review + Create** → **Create**

---

## Step 2: Connect and Create a Test File

Once VM is running:

1. Click **Connect** → choose **SSH**  
2. Use the SSH command to connect from your terminal:

```bash
ssh azureuser@<VM_PUBLIC_IP>
```

3. Inside the Linux VM, run:

```bash
mkdir ~/important-data
echo "Confidential: Project X secrets" > ~/important-data/secret.txt
```

4. Confirm it's there:

```bash
cat ~/important-data/secret.txt
```

Now we have a file to recover later!

---

## Step 3: Create a Recovery Services Vault

1. Go to the [Azure Portal](https://portal.azure.com)
2. Search for **Recovery Services Vaults**
3. Click **+ Create**
4. Fill the form:
   - **Subscription**: Free Trial
   - **Resource Group**: `startup-lab-rg`
   - **Vault Name**: `vm-backup-vault`
   - **Region**: Must match your VM’s region
5. Click **Review + Create** → **Create**

---

## Step 4: Configure Backup for Linux VM (with Daily Automation)

1. Go to **vm-backup-vault**
2. On left menu → **+ Backup**
3. **Where is your workload running?** → Select **Azure**
4. **What do you want to back up?** → Select **Virtual Machine**
5. Click **Continue**

6. Click **+ Add** → Select your **Linux VM** → Click **OK**

7. On **Backup Policy**:
   - Click **Create New**
     - Name: `linux-daily-policy`
     - Frequency: **Daily**
     - Time: 2:00 AM UTC
     - Time Zone: IST (or your time zone)
     - Retention: 30 days
     - Click **OK**

8. Click **Enable Backup**

Backups will now run **daily automatically**!

---

## Step 5: Trigger a Manual Backup (Optional for Testing)

1. Go to Recovery Vault → **Backup Items** → **Azure Virtual Machine**
2. Click on your **Linux VM**
3. Click **Backup Now**
4. Set **Retain Backup Till** date → Click **OK**

Wait for "Backup in progress" to complete.

---

## Step 6: Delete File & Recover It

### Simulate File Loss

1. SSH into your VM:

```bash
ssh azureuser@<VM_PUBLIC_IP>
```

2. Delete the file:

```bash
rm ~/important-data/secret.txt
```

3. Verify it’s gone:

```bash
cat ~/important-data/secret.txt  # Should give error
```

---

### Recover File from Backup

1. Go to Recovery Vault → **Backup Items** → **Azure Virtual Machine**
2. Click your Linux VM → **File Recovery**
3. Choose latest **Restore Point**
4. Click **Download Script**

### On your local terminal:

1. Upload script to your Linux VM:

```bash
scp ./recoveryScript.sh azureuser@<VM_PUBLIC_IP>:/home/azureuser/
```

2. SSH into VM and run the script:

```bash
chmod +x recoveryScript.sh
sudo ./recoveryScript.sh
```

3. The backup will mount at `/mnt/RecoveryDisk1` (or similar)

4. Recover your file:

```bash
cp /mnt/RecoveryDisk1/home/azureuser/important-data/secret.txt ~/important-data/
```

5. Confirm:

```bash
cat ~/important-data/secret.txt
```

File restored!

---

## Summary

| Step | Action |
|------|--------|
| 1️⃣ | Created a Linux VM on Azure |
| 2️⃣ | Created a test file inside the VM |
| 3️⃣ | Created Recovery Services Vault |
| 4️⃣ | Enabled automated daily backups |
| 5️⃣ | Triggered a manual backup |
| 6️⃣ | Recovered a deleted file from backup |

---

