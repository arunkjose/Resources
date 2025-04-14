---

## **Lab: Azure Data Lake Storage Gen2**

### **Scenario: Marketing Analytics for a Startup**
---
You're part of a marketing team that collects:
- **Website traffic logs** (`.csv`)
- **Social media campaign images** (`.jpg`, `.png`)

Your job is to create a **centralized data lake** to store this structured and unstructured data **securely**, using **Azure Free Tier** resources. You’ll learn how to:

- Create a Data Lake Gen2-enabled Storage Account  
- Create containers/folders  
- Upload and access files  
- Access endpoints and tools  
- Clean up to avoid charges

---

## **Pre-Requisites**

- Azure Free Trial account
- Internet browser
- Sample files (like `.csv`, `.jpg`, `.png`)

---

## **Step-by-Step Lab Instructions**

---

### **Step 1: Create a Resource Group**

1. Log in to [https://portal.azure.com](https://portal.azure.com)
2. Search for **"Resource groups"** → Click **Create**
3. Fill in:
   - **Subscription**: Free Trial
   - **Resource Group Name**: `datalake-lab-rg`
   - **Region**: Central US *(Free Tier supported region)*
4. Click **Review + Create** → **Create**

---

### **Step 2: Create a Data Lake Gen2-Enabled Storage Account**

1. Search for **"Storage accounts"** → Click **Create**
2. Fill in **Basics**:
   - **Subscription**: Free Trial
   - **Resource Group**: `datalake-lab-rg`
   - **Storage Account Name**: `datalakemarketingx1z` *(must be globally unique)*
   - **Region**: Central US
   - **Performance**: Standard
   - **Primary Service**: Others
   - **Redundancy**: Locally Redundant Storage (LRS)
3. Click on the **Advanced** tab:
   - Scroll to **Hierarchical namespace**
   - Enable **Hierarchical namespace** → set to **Yes**
4. Click **Review + Create** → **Create**

---

### **Step 3: Create a Container for Raw Data**

1. After the storage account is deployed, → Open it
2. From the left-hand menu → Click **Settings** -> **Configuration** -> Enable 'Allow Blob anonymous access' -> Save
3. From the left-hand menu → Click **Containers**
4. Click **+ Container**
   - Name: `raw-marketing-data`
   - Public Access: **Private (no anonymous access)**
5. Click **Create**

---

### **Step 4: Upload Files (CSV and JPG)**

1. Click into the `raw-marketing-data` container
2. Click **Upload**
   - Select:
     - `web-traffic.csv` *(sample traffic log)*
     - `ad-banner.jpg` *(sample image)*
3. Click **Upload**
4. After upload:
   - Click any file → **Download** to verify access

---

### **Step 5: Access File URLs (Endpoints)**

1. In the container, click any uploaded file
2. Click on **Properties**
3. Copy the **URL** of the file  
   Example:  
   ```
   https://datalakemarketingxyz.blob.core.windows.net/raw-marketing-data/web-traffic.csv
   ```
> Access is private, so unless access is changed  the URL won’t work for public access

---

### **Step 6: (Optional) Enable Lifecycle Management**

If you want to simulate auto-tiering of older data:

1. In your Storage Account → Left menu → **Lifecycle Management**
2. Click **+ Add a rule**
3. Name: `auto-tier-old-data`
4. Scope: All blobs
5. Rule:
   - Move blob to **Cool** after 30 days
   - (Optional) Move to **Archive** after 90 days
6. Click **Add**

> These rules simulate long-term cost savings.

---

### **Step 7: Clean Up to Avoid Charges**

1. Go to **Resource Groups** from the portal home
2. Search for `datalake-lab-rg`
3. Click → **Delete Resource Group**

---

## **Learning Outcome**

By the end of this lab, you now understand:

| Concept | What You Did |
|--------|---------------|
| **Data Lake Gen2** | Enabled Hierarchical Namespace for folder-like structure |
| **Blob Storage** | Used for both structured (CSV) and unstructured (JPG) data |
| **Containers** | Created to logically separate raw marketing data |
| **Accessing Data** | Viewed properties and tested download |
| **Endpoint URLs** | Learned how apps/tools can use file URLs |
| **Azure Storage Explorer** | Optional tool for interacting visually |
| **Lifecycle Management** | Set auto-move to cooler tiers for cost optimization |

---
