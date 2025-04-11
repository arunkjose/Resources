---

## **LAB: Backup a VM using Recovery Services Vault**

### Scenario:
You're managing a web server VM in Azure. The company wants **daily backups** of this VM for disaster recovery.

We'll:
1. Create a Recovery Services Vault  
2. Register the VM for backup  
3. Set up the backup policy  
4. Trigger a backup  
5. Explore restore options  

---

### **Pre-requisites:**
- A running **Linux or Windows VM** in Azure  
- A **Resource Group**  
- A **Free Tier subscription**

---

### 🛠Step 1: Create a Recovery Services Vault

1. Go to the [Azure Portal](https://portal.azure.com)
2. In the top search bar, search for **"Recovery Services Vaults"**
3. Click **+ Create**
4. Fill the form:
   - **Subscription**: Your Free Trial
   - **Resource Group**: Use an existing one (e.g., `startup-lab-rg`) or create a new one
   - **Vault Name**: `vm-backup-vault`
   - **Region**: Same as your VM’s location
5. Click **Review + Create** → **Create**

---

### Step 2: Configure Backup for the VM

1. After deployment, go to the newly created **Recovery Services Vault**
2. In the left menu, under **Getting Started**, click **+ Backup**
3. On the **Where is your workload running?** page:
   - **Select**: Azure
   - **What do you want to back up?**: Virtual Machine
   - Click **Continue**
4. Under **Select items to backup**:
   - Click **+ Add**
   - Select your VM → Click **OK**
5. **Backup Policy**:
   - You can keep the default policy (daily backup with 30-day retention) or click **Create New** to customize
6. Click **Enable Backup**

---

### Step 3: Trigger a Manual Backup

1. In the Recovery Services Vault → Left menu → **Backup Items**
2. Click **Azure Virtual Machine**
3. Select your VM name
4. In the toolbar at the top → Click **Backup Now**
5. Select the **Retain Backup Till** date → Click **OK**

It’ll show “Backup in progress.” Wait a few minutes.

---

### Step 4: Explore Restore Options

Once backup completes:

1. Go to **Backup Items** → **Azure Virtual Machine**
2. Click on your VM
3. Click **Restore VM**
4. You can choose:
   - **Create new VM** (from the backup)
   - **Replace existing VM** (be careful!)
   - Select **Restore Point**
   - Choose storage and settings
5. Click **Restore** (Only try this if you want to simulate it—no extra charges if free-tier used carefully)

---

---

## Summary

| Step | Action |
|------|--------|
| 1️⃣ | Created a Recovery Services Vault |
| 2️⃣ | Linked a VM to it for backup |
| 3️⃣ | Triggered a manual backup |
| 4️⃣ | Explored restore options (VM or file-level) |

---

