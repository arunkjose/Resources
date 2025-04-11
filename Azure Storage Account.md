
---
# **Azure Storage Lab**

### **Scenario: Startup Product Catalog System**

You're working at a small startup that sells handmade items online.  
You’re tasked with setting up cloud storage for:

- **Product images (JPGs)**
- **Order reports (CSVs)** 
The system should:
- Stay within the Free Tier
- Automatically manage old files
- Allow developers to access files when needed

---

### **Step 1: Create Resource Group**

1. **Go to** Azure Portal
2. In the top search bar, type **"Resource Groups"** → Click **Create**
3. Fill:
   - **Name**: `storage-lab-rg`
   - **Region**: *Central US*
4. Click **Review + Create** → **Create**

---

### **Step 2: Create a Storage Account**

1. In the top search bar, type **"Storage Accounts"** → Click **Create**
2. Fill:
   - **Subscription**: Free Trial
   - **Resource group**: `storage-lab-rg`
   - **Name**: `storage-lab-account-xyz` (unique)
   - **Region**: *Central US*
   - **Performance**: **Standard**
   - **Redundancy**: **LRS**
   - **Access Tier (default)**: **Hot**
3. Click **Review + Create** → **Create**

---

### **Step 3: Upload Product Images to Blob Storage**

1. Go to your **storage account** → Left menu → **Containers**
2. Click **+ Container**
   - Name: `product-images`
   - Public access: **Private**
3. Click the new container → Click **Upload**
   - Upload 1–2 small JPG or PNG files (sample product images)
4. Once uploaded, click a file → **Download** to test
5. **(Optional)** Click **Change tier** to move one file to **Cool**

---

### **Step 4: Upload Order Reports to File Share**

1. In your storage account → Left menu → **File shares**
2. Click **+ File share**
   - Name: `order-reports`
3. Click the file share → Upload a `.csv` file (e.g., `orders.csv`)
4. Click the file → Download it to test access

---

### **Step 5: View Access Endpoints (URLs)**

1. In your storage account → Click **Properties**
2. You'll see URLs (endpoints) for:
   - Blob service
   - File service
   - Table service
   - Queue service

Example Blob Endpoint:  
`https://startupstoragexyz.blob.core.windows.net/product-images/sample.jpg`

> These URLs are used by apps/scripts to access the files.

---

### **Step 6: Add Lifecycle Management Rule (Auto-Tiering)**

1. In your storage account → Left menu → **Lifecycle Management**
2. Click **+ Add rule**
3. Rule name: `move-old-to-cool`
4. Rule scope: Apply to all blobs
5. Define rule:
   - Move blobs to **Cool** after **30 days**
   - (Optional) Move to **Archive** after **90 days**
6. Click **Add**

> Rules won’t take effect immediately, but setup is complete.

---

### **Step 7: Access and Download Data**

| Type | Access Method |
|------|---------------|
| Blob (Images) | Go to container → Click blob → Download |
| File Share (Reports) | Go to file share → Click file → Download |
| Endpoint | Use copied URL (only works if access is public or app is authenticated) |

> Don’t make files public unless you’re sure! Always test with private access.

---

### **Step 8: Clean Up (Optional)**

To delete and avoid charges:

1. Go to **Resource Groups**
2. Click `startup-lab-rg` → **Delete Resource Group**

---

## **Learning Outcome**

By completing this lab, you’ve learned:

- Why and how storage is grouped (RG)
- How to use blob for unstructured data (images)
- How to use file shares for structured/semi-structured data (CSV logs)
- How access tiers and lifecycle rules optimize cost
- How to view/download data securely
- Where to find URLs for integration

---

