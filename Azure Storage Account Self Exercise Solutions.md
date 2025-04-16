
---

## **Solution**

### Step 1: Create a Storage Account

1. Go to [https://portal.azure.com](https://portal.azure.com).
2. Search for **Storage accounts** → Click **+ Create**.
3. Configure the account:
   - **Subscription**: Free Trial
   - **Resource Group**: `storage-demo-rg`
   - **Storage Account Name**: `youruniquestorage123`
   - **Region**: Select closest region
   - **Performance**: Standard
   - **Redundancy**: Locally-redundant storage (LRS)
4. Click **Review + Create** → **Create**

---

### Step 2: Upload a File to Blob Storage

1. Go to your created **Storage Account** → Click **Containers** under **Data storage**
2. Click **+ Container**
   - Name: `myblobcontainer`
   - Access Level: Private
   - Click **Create**
3. Open the container → Click **Upload**
   - Browse and select any small file (e.g., `notes.txt`)
   - Click **Upload**
4. Click the file to view:
   - Properties
   - URL (will be inaccessible unless public access is enabled)

---

### Step 3: Create and Upload to File Share

1. In the same Storage Account → Click **File shares**
2. Click **+ File Share**
   - Name: `myfileshare`
   - Click **Create**
3. Open the file share → Click **Upload** to add a file

---

