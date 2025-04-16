---

## **Solution: Step-by-Step Instructions**

### Step 1: Create the App Service

1. Log in to [https://portal.azure.com](https://portal.azure.com).
2. Search for **App Services** → Click **+ Create**.
3. In the **Basics** tab:
   - **Subscription**: Free Tier or your active subscription
   - **Resource Group**: `appservice-demo-rg` (create if needed)
   - **Name**: `myhtmlwebapp123`
   - **Publish**: Code
   - **Runtime Stack**: .NET Core (you can leave it default since you're serving static HTML)
   - **OS**: Windows
   - **Region**: Closest to your location
4. Under **App Service Plan**, click **Create new**:
   - Name: `FreePlan`
   - Choose **F1 - Free Tier**
5. Click **Review + Create** → **Create**

---

### Step 2: Deploy the HTML Page

#### Option A: App Service Editor (Quick Edit in Portal)

1. Go to your newly created App Service.
2. In the left menu → Go to **Development Tools** → Click **App Service Editor (Preview)** → Click **Go**.
3. In the editor, go to `site/wwwroot`.
4. Create a new file: `index.html`.
5. Paste the provided HTML content into the file and **Save**.

#### Option B: Zip Deploy (Local Upload)

1. On your local system:
   - Create a folder (e.g., `webapp`)
   - Save the provided `index.html` inside that folder
   - Compress the folder into `webapp.zip`
2. In the Azure Portal:
   - Go to your App Service → Click **Deployment Center**
   - Choose **Zip Deploy** → Upload the `webapp.zip`

---

### Step 3: Verify the Deployment

1. Go back to your App Service → Click **Overview**
2. Find the **Default Domain**, e.g., `https://myhtmlwebapp123.azurewebsites.net`
3. Click the URL or open it in your browser

You should see the HTML page with the "Hello from Azure App Service!" heading.

---

