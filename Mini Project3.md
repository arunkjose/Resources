Setting Up and Testing Azure Functions with HTTP Trigger and Timer Trigger

This lab will guide you through setting up the environment for running Azure Functions locally with **Visual Studio Code (VS Code)**, **Azure Functions Extension**, **Azure Functions Core Tools**, and **Azure Storage Account**. You will then create and test two types of Azure Functions: **HTTP Trigger** and **Timer Trigger**.

---

### **Part 1: Set Up the Development Environment**

#### **Step 1: Install Visual Studio Code (VS Code)**

1. **Download VS Code**:
   - Go to the [Visual Studio Code Downloads page](https://code.visualstudio.com/download).
   - Choose the version for your operating system (Windows, macOS, or Linux) and install it.

2. **Launch VS Code**:
   - After installation, open Visual Studio Code.

---

#### **Step 2: Install the Azure Functions Extension for VS Code**

1. **Open Extensions Panel**:
   - In VS Code, click the **Extensions** icon on the left sidebar or press `Ctrl+Shift+X` (Windows/Linux) or `Cmd+Shift+X` (macOS).

2. **Search for Azure Functions Extension**:
   - In the search bar, type **Azure Functions**.

3. **Install the Azure Functions Extension**:
   - Click on the **Azure Functions** extension by **Microsoft** and click **Install**.

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
     npm install -g azure-functions-core-tools@3 --unsafe-perm true
     ```

3. **Verify the Installation**:
   - Run the following command to verify the installation:

     ```bash
     func --version
     ```

   - You should see the installed version of **Azure Functions Core Tools**.

---

### **Part 2: Create and Test Azure Functions**

#### **Step 1: Create an HTTP Trigger Function**

1. **Create a New Azure Functions Project**:
   - In VS Code, open the **Command Palette** (`Ctrl+Shift+P`).
   - Type **Azure Functions: Create New Project**.
   - Choose the folder where you want to store the function app.
   - Select **JavaScript** as the language.
   - Select **Function** as the template and **HTTP Trigger** for the trigger type.
   - Set the function name as `HttpTriggerFunction`.
   - Set the **Authorization Level** to **Anonymous**.

2. **Modify the HTTP Trigger Code**:
   Update the code in `index.js` to the following:

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

3. **Test the Function Locally**:
   - Press **F5** to run the function locally.
   - Open your browser and go to `http://localhost:7071/api/HttpTriggerFunction?name=John`.
   - You should see the response:
     ```
     Hello, John!
     ```

---

#### **Step 2: Create a Timer Trigger Function**

1. **Create a New Timer Trigger Function**:
   - In VS Code, open the **Command Palette** (`Ctrl+Shift+P`).
   - Type **Azure Functions: Create New Function** and select **Timer Trigger** as the template.
   - Set the function name as `TimerFunction`.
   - Set the **Schedule** to `"0 * * * * *"` (this cron expression triggers the function every minute).

2. **Modify the Timer Trigger Code**:
   Update the code in `index.js` to the following:

   ```javascript
   module.exports = async function (context, myTimer) {
       const currentTime = new Date().toISOString();
       context.log('Timer trigger function ran!', currentTime);
   };
   ```

3. **Test the Timer Function Locally**:
   - Press **F5** to run the function locally.
   - Every minute, check the **Terminal** for the log output with the timestamp.
   - Example log:
     ```
     Timer trigger function ran! 2025-04-12T10:10:00.000Z
     ```

---

### **Part 3: Deploy to Azure (Optional)**

1. **Sign In to Azure**:
   - In VS Code, open the **Command Palette** (`Ctrl+Shift+P`).
   - Type **Azure Functions: Sign In to Azure** and follow the prompts to authenticate.

2. **Deploy the Functions**:
   - Right-click the **Function App** in the **Azure** tab on the left sidebar.
   - Select **Deploy to Function App** and follow the prompts to deploy your local function to Azure.

3. **Test the Deployed Functions**:
   - After deployment, you’ll get a URL for each function (HTTP and Timer Trigger).
   - Test the **HTTP Trigger** using Postman or a browser.
   - For the **Timer Trigger**, monitor the logs in the Azure portal to see when it runs.

---

### **Summary**

In this lab, you have:
- Set up **Visual Studio Code** with the **Azure Functions Extension**.
- Installed **Azure Functions Core Tools**.
- Created and tested two types of Azure Functions using **HTTP Trigger** and **Timer Trigger**.
- Optionally, deployed the functions to **Azure** for remote testing.

You now have a local development environment for Azure Functions, and you can test and deploy your functions to the cloud.
