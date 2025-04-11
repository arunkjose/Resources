---
# **Azure Storage Lab**
### **Scenario: Startup Product Catalog System**
---
You're working at a small startup that sells handmade items online.You’re tasked with setting up cloud storage for:
---
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
   - **Name**: `storagelabaccountxyz` (must be unique)  
   - **Region**: *Central US*  
   - **Primary Service**: Others  
   - **Performance**: **Standard**  
   - **Redundancy**: **LRS**  
   - **Access Tier (default)**: **Hot**  
3. Click **Review + Create** → **Create**

---

### Enable Blob Anonymous Access (Optional for Public URLs)**

> Only do this if you want to allow unauthenticated access to blobs (like static images).

1. Go to your **storage account** → Left menu → **Configuration**  
2. Find **Allow blob public access**  
3. Set it to **Enabled**  
4. Click **Save**
![image](https://github.com/user-attachments/assets/860c45f4-3f64-4315-87b8-3164350164d7)

Then:

- Go to your **container** (after creating it in Step 3)  
- Click **Change access level** → Set to:
  - **Blob (public read access for blobs only)**

---

### **Step 3: Upload Product Images to Blob Storage**

1. Go to your **storage account** → Left menu → **Containers**  
2. Click **+ Container**
   - Name: `product-images`
   - Public access: **Private** (unless testing public URLs)
3. Click the container → **Upload**
   - Upload 1–2 small JPG or PNG files
4. Click a file → **Download** to test
5. *(Optional)* Click **Change tier** to move one file to **Cool**

---

### **Step 4: Upload Order Reports to File Share**

1. In your storage account → Left menu → **File shares**  
2. Click **+ File share**
   - Name: `order-reports`
3. Click the file share → Upload a `.csv` file (e.g., `orders.csv`)
4. Click the file → Download it to test

---

### **Step 5: Add Lifecycle Management Rule (Auto-Tiering)**

1. In your storage account → Left menu → **Data Management ** -> **Lifecycle Management**
2. Click **+ Add rule**
3. Rule name: `move-old-to-cool`
4. Scope: Apply to all blobs
5. Define rule:
   - Move blobs to **Cool** after **30 days**
   - (Optional) Move to **Archive** after **90 days**
6. Click **Add**

---

### **Step 7: Clean Up (Optional)**

1. Go to **Resource Groups**
2. Click `storage-lab-rg` → Click **Delete Resource Group**

---

### **Learning Outcome Recap**

- Created a **free-tier storage account**
- Used **Blob** for unstructured images
- Used **File Share** for structured CSV logs
- Configured **lifecycle management**
- Managed **public access settings**

---

