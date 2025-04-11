
---

# Steps to Create Azure App Service Plan & Web App

---

## Step 1: Sign In to Azure Portal

- Go to [https://portal.azure.com](https://portal.azure.com)
- Sign in with your Azure credentials

---

## Step 2: Create an App Service Plan

1. **Search** for **"App Service plans"** in the top search bar
2. Click **+ Create** (or **+ Add**)

### Fill in the Basics:
- **Subscription**: Select your subscription
- **Resource Group**: Create new :paas-demo
- **Name**: 'webserver-plan'
- **Operating System**: Choose **Linux** 
- **Region**: Central Us
- **SKU and Size**:
  - Click **Change size**
  - Select a **Pricing Tier** : Premium v3
  - Click **Apply**

3. Click **Review + Create**
4. Click **Create**

**App Service Plan is now created.**

---

## Step 3: Create an Azure App Service (Web App)

1. **Search** for **"App Services"**
2. Click **+ Create**

### Fill in the Basics:
- **Subscription**: Choose your subscription
- **Resource Group**: Select the same as used for App Service Plan
- **Name**: `my-linux-webapp-123` *(must be globally unique)*
- **Publish**: **Code**
- **Runtime Stack**: Choose according to your application (PHP)
- **Operating System**: **Linux** 
- **Region**: Must be same as the App Service Plan (e.g., **Central US**)

### App Service Plan:
- Click **"App Service Plan" > "Browse"** 
- Select the plan you created earlier 

3. Click **Review + Create**
4. Click **Create**

**Web App is now deployed.**

---
## Step 4: Connect App Service to GitHub via Deployment Center

1. In the Azure Portal, go to **App Services**
2. Select your web app
3. In the left-hand menu, scroll down and click **Deployment Center**

### Configure GitHub Integration:

4. Under **Source**, select **GitHub**
5. Click **Authorize AzureAppService** if prompted (log into GitHub and allow permissions)
6. Choose:
   - **Organization**: Your GitHub username/org
   - **Repository**: Select your repo
   - **Branch**: `main` or your working branch

7. Click **Save**

Azure will now automatically pull code from GitHub and deploy it.

---

## Step 5: Verify Deployment

1. Go back to the **Deployement Center**  tab
2. Click on browser

3. Your GitHub-hosted site should now be live!

---
