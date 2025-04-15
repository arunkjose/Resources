---
# Microsoft File System + Disk Management Lab on Azure Windows VM  
---

## Lab Objectives

By the end of this lab, you will be able to:

- Create a Windows Server VM in Azure
- Attach and configure a data disk
- Initialize, partition, and format the disk with NTFS
- Perform NTFS file system operations: compression, permissions, quotas

---

## SECTION 1: Create a Windows Virtual Machine in Azure

---

### Steps to Create Windows Server VM

1. Log in to [Azure Portal](https://portal.azure.com)
2. Search for **Virtual Machines** → Click **Create**
3. In the "Basics" tab:

| Field               | Value                                  |
|---------------------|----------------------------------------|
| Subscription         | Free Trial                             |
| Resource Group       | Create new → `RG-FileSystemLab`        |
| Virtual Machine Name | `WindowsFS-VM`                         |
| Region               | Select nearest region (e.g., East US) |
| Image                | Windows Server 2022 Datacenter        |
| Size                 | B1s (or DS1_v2 for Free Tier)          |
| Username             | `azureuser`                            |
| Password             | Set a strong password                  |
| Inbound ports        | **Allow RDP (3389)**                   |

4. In the **Disks** tab:
   - OS Disk Type: Standard HDD or SSD (your choice)

5. In the **Networking** tab:
   - Keep default settings

6. Click **Review + Create** → Wait for validation → Click **Create**

---

### Connect to VM

After deployment:

1. Click **Go to Resource**
2. Click **Connect** > **RDP**
3. Download the `.rdp` file
4. Login using your `azureuser` credentials

You're inside your Windows Server VM now!

---

## SECTION 2: Add a New Data Disk to Your VM

### Steps:

1. In Azure Portal → Go to your VM → **Disks**
2. Click **+ Add data disk**
3. Under **Name**, click **Create disk**:
   - Name: `DataDisk01`
   - Size: 10 GiB
   - Performance: Standard
   - Click **Create**
4. Attach this disk and click **Save**

Wait a few seconds. The disk is now available in your VM!

---

## SECTION 3: Partition and Format the Data Disk

### Inside the VM:

1. Press `Windows + X` → Choose **Disk Management**
2. New disk shows as **Unallocated**
3. Right-click on the new disk → **Initialize Disk**
   - Select **GPT**
4. Right-click **Unallocated Space** → **New Simple Volume**
   - Assign Drive Letter: `E:`
   - File System: **NTFS**
   - Volume Label: `NTFSData`

Disk is ready with NTFS format.

---

## SECTION 4: Explore NTFS Features

---

### 4.1 Enable File Compression

1. Go to **Drive E:**
2. Create a folder → Name: `CompressedFolder`
3. Right-click the folder → Properties → Click **Advanced**
4. Check **"Compress contents to save disk space"** → Click OK

Files in this folder will now be stored compressed.

---

### 4.2 Set NTFS Permissions

1. Right-click on `CompressedFolder` → **Properties**
2. Go to **Security** tab
3. Click **Edit** → Add or modify permissions
   - You can allow/deny **Read**, **Write**, **Modify**, etc.
4. Add custom users (if needed) or test with `azureuser`

Permissions control who can do what with the folder.

---

### 4.3 Enable Disk Quotas

1. Right-click `E:` drive → Properties → **Quota** tab
2. Click **"Show Quota Settings"**
3. Enable:
   - [✓] Enable quota management
   - [✓] Deny disk space to users exceeding limit
4. Set limit (e.g., 5 GB warning, 7 GB hard limit)

Quotas are now enforced per user.

---

