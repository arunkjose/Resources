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
| Region               | Canada Central |
| Image                | Windows Server 2022 Datacenter        |
| Size                 | Standard_D4s_v3       |
| Username             | `azureuser`                            |
| Password             | Set a strong password                  |
| Inbound ports        | **Allow RDP (3389)**                   |



4. In the **Disks** tab:
   - OS Disk Type: Standard HDD 

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

1. In Azure Portal → Go to your VM → **Settings** -> **Disks**
2. Click **+ Add data disk**
3. Under **Name**, click **Create disk**:
   - Name: `DataDisk01`
   - Size: 32 GiB
   - Performance: Standard
   - Click **Create**
4. Attach this disk and click **Save**

Wait a few seconds. The disk is now available in your VM!
![image](https://github.com/user-attachments/assets/e73e76ac-8afb-4f18-b71e-0fdf1c8d57e5)

---

## SECTION 3: Partition and Format the Data Disk

### Inside the VM:

1. Press `Windows + X` → Choose **Disk Management**
   ![image](https://github.com/user-attachments/assets/87080639-4aa7-4900-92ee-b9cc473118de)
2. New disk shows as **Unallocated**
   ![image](https://github.com/user-attachments/assets/b768bae5-c67e-47f4-ba84-d526e1a5e154)

3. Right-click on the new disk → **Initialize Disk**
   - Select **GPT**
![image](https://github.com/user-attachments/assets/d2a44d17-d4d7-4bdc-8884-2b5fba774b3f)

4. Right-click **Unallocated Space** → **New Simple Volume**
   - File System: **NTFS**
   - Volume Label: `NTFSData`
![image](https://github.com/user-attachments/assets/8cae9234-af24-45f8-9873-097073e3d729)

![image](https://github.com/user-attachments/assets/a162cb4a-550d-4562-b2c5-29d42d3062ea)


Disk is ready with NTFS format.
---

## SECTION 4: Explore NTFS Features
---

### 4.1 Enable File Compression

1. Go to **File Explorer** -> **This pc** -> **Drive F:**
 ![image](https://github.com/user-attachments/assets/3b064323-ba17-4524-b0f3-cfe083d2e056)
2. Create a folder → Name: `CompressedFolder`
3. ![image](https://github.com/user-attachments/assets/76ad4a91-bf88-4b56-808a-59af238db91c)

4. Right-click the folder → Properties → Click **Advanced**
5. Check **"Compress contents to save disk space"** → Click OK

Files in this folder will now be stored compressed.
![image](https://github.com/user-attachments/assets/6ad9e2b2-485e-470b-9ad0-eb8194ff3e32)

---

### 4.2 Set NTFS Permissions

1. Right-click on `CompressedFolder` → **Properties**
2. Go to **Security** tab
3. Click **Edit** → Add or modify permissions
   - You can allow/deny **Read**, **Write**, **Modify**, etc.
4. Add custom users (if needed) or test with `azureuser`

Permissions control who can do what with the folder.
![image](https://github.com/user-attachments/assets/b0ae97c1-0fe3-4624-a68d-71a09639d366)

---

### 4.3 Enable Disk Quotas

1. Right-click `F:` drive → Properties → **Quota** tab
2. Click **"Show Quota Settings"**
3. Enable:
   - [✓] Enable quota management
   - [✓] Deny disk space to users exceeding limit
4. Set limit (e.g., 5 GB warning, 7 GB hard limit)
![image](https://github.com/user-attachments/assets/ea8780fb-4b34-4b47-9dc8-b78ad1573d39)

Quotas are now enforced per user.

### 4.4 File Encryption

1. Right-click CompressedFolder → **Properties**
2. Click Advanced
3. Check the box: “Encrypt contents to secure data”
4. Click OK → Apply → Choose:
5. Apply changes to this folder only OR Apply to folder, subfolders, and files (if you plan to add files later)
6. Click OK to finish.
---
![image](https://github.com/user-attachments/assets/21ad405d-5df2-4e72-a437-52b5b58cc70d)

### Cleanup
---

### Steps to Delete Resource Group

1. Go to [https://portal.azure.com](https://portal.azure.com)

2. In the search bar, type **“Resource groups”** and open it

3. Locate the Resource Group you created  
   > e.g., `RG-FileSystemLab`

4. Click on it to open details

5. At the top, click **"Delete resource group"**

6. Azure will prompt:  
   > “Type the resource group name to confirm”

7. Type the exact name (e.g., `RG-FileSystemLab`)

8. Click **Delete**

---



