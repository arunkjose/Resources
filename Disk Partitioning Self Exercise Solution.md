---
## **Solution: Step-by-Step Instructions**
---
### Step 1: Attach a New Data Disk to the Windows Server VM

1. Go to the [Azure Portal](https://portal.azure.com) and sign in.
2. In the left-hand menu, select **Virtual Machines**.
3. Choose the **Windows Server VM** to which you want to attach the disk.
4. Under **Settings**, click **Disks**.
5. Click **+ Add data disk**:
   - **Name**: `NewDataDisk`
   - **Source Type**: **Empty**
   - **Size**: 50 GB (or according to your requirement)
   - **Disk type**: Choose **Standard HDD** or **Standard SSD** based on your preference.
6. Click **Save** to attach the disk.

---

### Step 2: Initialize and Partition the New Disk in Windows Server VM

1. **Connect** to your Windows Server VM using **RDP** (Remote Desktop Protocol).
2. Once logged in, press **Windows + X** and choose **Disk Management**.
3. In **Disk Management**, you should see the new disk listed as **Unallocated** (e.g., `Disk 1`).
4. Right-click on the **Unallocated space** → Select **Initialize Disk**:
   - Choose **GPT** (GUID Partition Table) if it's a large disk (over 2TB) or **MBR** (Master Boot Record) if it's smaller.
5. After initializing, right-click the **Unallocated space** → Select **New Simple Volume**:
   - Follow the wizard to:
     - Assign a drive letter (e.g., **D:**)
     - Format the disk with **NTFS** and provide a volume label (e.g., `DataDisk`).
6. Click **Next** and then **Finish** to complete the partitioning and formatting.

---

### Step 3: Verify the New Disk in Windows Server VM

1. Open **File Explorer** on the Windows Server VM.
2. Navigate to **This PC**.
3. You should now see the new disk (e.g., **D:**) listed with the volume label you provided.
4. You can now use the disk for storage, install applications, or store data.

---
