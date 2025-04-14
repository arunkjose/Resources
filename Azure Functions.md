## Setting Up and Testing Azure Functions with HTTP Trigger and Timer Trigger

This lab will guide you through setting up the environment for running Azure Functions locally with **Visual Studio Code (VS Code)**, **Azure Functions Extension**, **Azure Functions Core Tools**, and **Azure Storage Account**. You will then create and test two types of Azure Functions: **HTTP Trigger** and **Timer Trigger**.

---

### **Part 1: Set Up the Development Environment**

#### **Step 1: Install Visual Studio Code (VS Code)**

1. **Download VS Code**:
   - Go to the [Visual Studio Code Downloads page](https://code.visualstudio.com/download).
   - Choose the version for your operating system (Windows, macOS, or Linux) and install it.

2. **Launch VS Code**:
   - After installation, open Visual Studio Code.
3. Create two new folders on the Desktop
   **HttpTriggerProject** & **TimerTriggerProject**
---

#### **Step 2: Install the Azure Functions Extension for VS Code**

1. **Open Extensions Panel**:
   - In VS Code, click the **Extensions** icon on the left sidebar or press `Ctrl+Shift+X` (Windows/Linux) or `Cmd+Shift+X` (macOS).

2. **Search for Azure Functions Extension**:
   - In the search bar, type **Azure Functions**.

3. **Install the Azure Functions Extension**:
   - Click on the **Azure Functions** extension by **Microsoft** and click **Install**.
![image](https://github.com/user-attachments/assets/1fa55589-dbca-4d9b-af4a-8b3890c035cd)

---

#### **Step 3: Install Azure Functions Core Tools Locally**

**Azure Functions Core Tools** allow you to run and test Azure Functions on your local machine before deploying them to Azure.

1. **Install Node.js** (required for Azure Functions Core Tools):
   - Visit the [Node.js Downloads page](https://nodejs.org/en/download/) and download the **LTS version**.
   - Install Node.js on your system.

2. **Install Azure Functions Core Tools**:
   - Open your **Command Prompt** (Windows) or **Terminal** (macOS/Linux).
   - Run the following command to install **Azure Functions Core Tools** globally:

     ```bash
    npm install -g azure-functions-core-tools@4 --unsafe-perm true
     ```

3. **Verify the Installation**:
   - Run the following command to verify the installation:

     ```bash
     func --version
     ```

   - You should see the installed version of **Azure Functions Core Tools**.
![image](https://github.com/user-attachments/assets/34a06a21-3854-4cad-be4c-739d0c120a7c)

4. **Install and Run Azurite (Recommended for Local Dev)**
```
npm install -g azurite
```
```
azurite --version
```
```
azurite
```
![image](https://github.com/user-attachments/assets/e6653c95-b432-4e70-ac2f-2d2022903915)

---

### **Part 2: Create and Test Azure Functions**

#### **Step 1: Create an HTTP Trigger Function**

1. **Create a New Azure Functions Project**:
   - In VS Code, open the **Command Palette** (`Ctrl+Shift+P`).
   - Type **Azure Functions: Create New Project**.
   - Choose the folder where you want to store the function app :**HttpTriggerProject**
   - Select **JavaScript** as the language.
   - Select **HTTP Trigger** for the trigger type.
   - Set the function name as `HttpTriggerFunction`.

2. **Modify the HTTP Trigger Code**:
   Update the code in `HttpTriggerFunction.js` to the following:

   ```javascript
   module.exports = async function (context, req) {
       context.log('JavaScript HTTP trigger function processed a request.');

       const name = req.query.name || (req.body && req.body.name);
       context.res = {
           // status: 200, /* Defaults to 200 */
           body: name ? `Hello, ${name}!` : 'Hello, world!'
       };
   };
   ```
   Create a new file called function.json
   'The function.json file is a crucial configuration file in an Azure Functions app. It defines the bindings and trigger settings for the function.'
   
   Update the code:
   ```
   {
    "bindings": [
      {
        "authLevel": "anonymous",
        "type": "httpTrigger",
        "direction": "in",
        "name": "request",
        "methods": ["get", "post"]
      },
      {
        "type": "http",
        "direction": "out",
        "name": "$return"
      }
    ]
  }
  ```
HTTP Trigger: The function will be triggered by an HTTP request (GET/POST), and the input is represented by the request parameter.

HTTP Output: The function returns a response that will be captured as $return.

**Note: If you see any file called index.js delete it.**

Modify the contents of file host.json:
```
{
  "version": "2.0"
}
```

4. **Test the Function Locally**:
   - Press **F5** to run the function locally.
   - Open your browser and go to `http://localhost:7071/api/HttpTriggerFunction?name=John`.
   - You should see the response:
     ```
     Hello, World!
     ```

---

#### **Step 2: Create a Timer Trigger Function**

1. **Create a New Timer Trigger Function**:
   - In VS Code, open the **Command Palette** (`Ctrl+Shift+P`).
   - Choose the folder where you want to store the function app:**TimerTriggerProject**
   - Type **Azure Functions: Create New Function** and select **Timer Trigger** as the template.
   - Set the function name as `TimerFunction`.
   - Set the **Schedule** to `"0 * * * * *"` (this cron expression triggers the function every minute).

2. **Modify the Timer Trigger Code** 
   Rename timerTrigger.js to index.js and add the below code

   ```javascript
  module.exports = async function (context, myTimer) {
    const currentTime = new Date().toISOString();
    context.log(`Timer triggered at: ${currentTime}`);
    if (myTimer.isPastDue) {
        context.log('Timer is running late!');
    }
};
   ```
Modify the contents of the file host.json:
```
{
  "version": "2.0"
}
```
**Note: If you see any file called index.js, delete it.**

Make sure .fucignore contents match the below contents:
```
__azurite_db*__.json
__blobstorage__
__queuestorage__
local.settings.json
test
tsconfig.json
.gitignore
.vscode
```
If not, update and save.
.funcignore is used to specify files and directories to be ignored when deploying or running your Azure Functions app locally.

Create the function.json file with the below contents:
```
{
  "bindings": [
    {
      "name": "myTimer",
      "type": "timerTrigger",
      "direction": "in",
      "schedule": "*/5 * * * * *"
    }
  ]
}
```
![image](https://github.com/user-attachments/assets/63e32024-b8b5-4983-8e20-faa380b6b9e0)

package.json
```
{
  "name": "timerapp",
  "version": "1.0.0",
  "scripts": {
    "start": "func start"
  },
  "dependencies": {}
}
```
Verify the folder structure
![image](https://github.com/user-attachments/assets/227b8e59-48ea-44cc-a943-ee6abfeb10d8)
Any differences, modify it accordingly.


3. **Test the Timer Function Locally**:
   - Press **F5** to run the function locally.
   - Every minute, check the **Terminal** for the log output with the timestamp.
   - Example log:
     ```
     The timer trigger function ran! 2025-04-12T10:10:00.000Z
     ```
![image](https://github.com/user-attachments/assets/cb074148-50bb-4594-8e75-fdd45b593689)

---

To include the steps for creating a Function App on Azure before deploying the Timer Trigger Function, here's how the process would look, including the necessary code updates and actions in Azure:

---

### **Part 3: Deploy to Azure**

### Step 1: Create an Azure Storage Account

1. **Go to the Azure Portal**:
   - Visit [Azure Portal](https://portal.azure.com/).

2. **Create a New Storage Account**:
   - In the left sidebar, click **Create a resource**.
   - In the search box, type **Storage account** and select it from the options.
   - Click **Create**.

3. **Configure Storage Account**:
   Fill in the necessary details:
   - **Subscription**: Choose your Azure subscription.
   - **Resource Group**: Select an existing resource group or create a new one.
   - **Storage Account Name**: Provide a globally unique name for your storage account (e.g., `mystorageaccount123`).
   - **Region**: Select the region closest to your function app (e.g., **East US**).
   - **Performance**: Choose **Standard**.
   - **Replication**: Choose **Locally redundant storage (LRS)**.
   - Click **Next** through the remaining tabs, reviewing the settings, and then click **Create**.

4. **Wait for Deployment**:
   - The storage account will be created. This may take a few minutes.
   - Once the deployment is complete, go to the **Storage Account** resource in the portal.

---

### Step 2: Retrieve the Connection String for the Storage Account

1. **Access Storage Account Keys**:
   - In the Azure Portal, go to your **Storage Account**.
   - Under the **Settings** section, click **Access keys**.
   - Copy **Key1** (or **Key2** if you prefer).

2. **Get the Connection String**:
   - Below the key details, you'll see the **Connection string**. Copy this connection string.

---

### Step 3: Configure `AzureWebJobsStorage` in Your Function App
Without the AzureWebJobsStorage setting, Azure Functions wouldn't have access to essential storage resources, leading to failures in logging, state management, and other runtime operations. This setting is a fundamental requirement to ensure proper function app behavior.

1. **Go to Your Function App**:
   - In the **Azure Portal**, navigate to your **Function App**.
   - Under the **Settings** section, click on **Configuration**.

2. **Add `AzureWebJobsStorage` Setting**:
   - Click **+ New application setting**.
   - Set the **Name** to `AzureWebJobsStorage`.
   - Paste the **Connection String** you copied from the Storage Account.
   - Click **OK**.

3. **Save the Configuration**:
   - Click **Save** at the top to apply the changes.

---

#### **Step 4: Deploy the Function to Azure**

Once your Function App is created and you're signed in to Azure, you can deploy the function:

1. In VS Code, go to the **Azure** tab on the left sidebar.
2. Find your **Function App** under the **Functions** section.
   ![image](https://github.com/user-attachments/assets/67d44427-82ac-4dd5-81d9-1d80f4a83ff8)

4. Right-click the Function App and select **Deploy to Function App**.
   ![image](https://github.com/user-attachments/assets/b3419eb6-49de-4e82-a985-76686d85f37e)

6. VS Code will prompt you to select the folder containing your function app (`TimerTriggerProject`).
7. Choose the correct Function App you created in Azure (e.g., `my-timer-function-app`).
8. Confirm the deployment.

   VS Code will deploy your function to Azure. During the deployment process, you'll see logs and progress in the **Output** window.

---

#### **Step 5: Test the Deployed Functions**

Once the function is deployed to Azure, you'll need to test both the HTTP Trigger and the Timer Trigger.

1. **Test the HTTP Trigger**:
   - After deployment, Azure will provide you with a **URL** for the HTTP trigger.
   - Use browser to make a request to the HTTP trigger endpoint.
   - You should get a response, such as a `200 OK` with any additional output defined in your function.

2. **Monitor the Timer Trigger**:
   - For the **Timer Trigger**, since it runs based on a cron expression, it will trigger according to the schedule you defined.
   - Go to the **Azure Portal** and navigate to your Function App.
   - Under **Functions**, find your `TimerFunction`.
   - Go to **Monitor** or **Logs** to check when the function is being triggered. You should see logs corresponding to the timestamps for each trigger.
---

### **Summary**

In this lab, you have:
- Set up **Visual Studio Code** with the **Azure Functions Extension**.
- Installed **Azure Functions Core Tools**.
- Created and tested two types of Azure Functions using **HTTP Trigger** and **Timer Trigger**.
- Optionally, deployed the functions to **Azure** for remote testing.

