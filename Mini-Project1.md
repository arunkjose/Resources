---
# Lab Guide: Hosting a Website on Azure Windows Server using IIS
---

## Lab Setup Steps

---

### **Step 1: Create a Windows Server VM in Azure**

1. **Login to Azure Portal**: [https://portal.azure.com](https://portal.azure.com)
2. Go to **Virtual Machines** > Click **+ Create** > **Azure Virtual Machine**
3. Fill in the **Basics** tab:
   - **Subscription**: Your active subscription
   - **Resource Group**: Create or select an existing one
   - **Virtual machine name**: `MyIISWebServer`
   - **Region**: Choose nearest region
   - **Image**: Select `Windows Server 2019 Datacenter` (or 2022)
   - **Size**: Choose a basic size (e.g., B1s for demo)
   - **Administrator account**: Enter username and password (note these for RDP)
   - **Public inbound ports**: Allow selected ports → Check **RDP (3389) + Http (80)**
4. Click **Next** through other tabs, then click **Review + Create**
5. Wait for deployment to complete and click **Go to Resource**

---

### **Step 2: Connect to the VM via RDP**

1. In the VM Overview page, click **Connect > RDP**
2. Download the RDP file and open it
3. Enter the credentials you set earlier
4. You’re now inside the Windows Server VM

---

### **Step 3: Install IIS on Windows Server**

1. Open **Server Manager** from the Start Menu
2. Click **Add roles and features**
3. On the wizard:
   - **Installation Type**: Role-based
   - **Server Selection**: Local server
   - **Server Roles**: Check **Web Server (IIS)**
   - Add features if prompted, then click **Next**
4. Click **Install**, wait for the installation to finish
5. After installation, open browser inside VM and go to:  
   **http://localhost**  
   You should see the **default IIS web page**

---

### **Step 4: Create and Host a Simple Website**

1. Open **File Explorer** and go to:
   ```
   C:\inetpub\wwwroot
   ```
2. Backup and delete `iisstart.htm` (optional)
3. Create a new file called `index.html` with the following content:
   ```html
   <html>
   <head><title>My Azure IIS Website</title></head>
   <body>
       <h1>Hello from Azure IIS Server!</h1>
   </body>
   </html>
   ```
4. Save the file

---

### **Step 5: Allow HTTP (Port 80) in Network Security Group**

1. Go to Azure Portal → Your VM → **Networking**
2. Under **Inbound Port Rules**, click **Add Inbound Port Rule**
3. Set:
   - **Source**: Any
   - **Source Port Ranges**: *
   - **Destination**: Any
   - **Destination Port Ranges**: `80`
   - **Protocol**: TCP
   - **Action**: Allow
   - **Priority**: Leave default
   - **Name**: `Allow-HTTP`
4. Click **Add**

---

### **Step 6: Access Your Website Publicly**

1. Go to VM **Overview** → Copy **Public IP Address**
2. Paste it in a browser like this:
   ```
   http://<your-public-ip>
   ```
3. You should see your **custom HTML page**!

---

## Clean Up Resources 

If you're done, delete the resource group to avoid charges:
1. Go to **Resource Groups** in Azure
2. Select the group you created
3. Click **Delete Resource Group**

---
