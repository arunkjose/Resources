
---

## **Setting Up and Testing Azure Functions with HTTP Trigger and Timer Trigger**

This lab guides you through setting up Azure Functions locally using **Visual Studio Code**, installing required extensions and tools, creating **HTTP** and **Timer** trigger functions, and deploying them to **Azure**.

---

## **Part 1: Set Up the Development Environment**

### Step 1: Install Visual Studio Code (VS Code)

1. Download from: [https://code.visualstudio.com/download](https://code.visualstudio.com/download)  
2. Install and launch VS Code.
3. Create two folders on your desktop:
   - `HttpTriggerProject`
   - `TimerTriggerProject`

---

### Step 2: Install Azure Functions Extension in VS Code

1. Open **Extensions**:  
   `Ctrl+Shift+X` (Windows/Linux) or `Cmd+Shift+X` (macOS)
2. Search for **Azure Functions**.
3. Install the extension by **Microsoft**.

![Azure Functions Extension](https://github.com/user-attachments/assets/1fa55589-dbca-4d9b-af4a-8b3890c035cd)

---

### Step 3: Install Azure Functions Core Tools

1. **Install Node.js (LTS Version)**:  
   [https://nodejs.org/en/download](https://nodejs.org/en/download)

2. **Install Core Tools** (in terminal or command prompt):  
   ```bash
   npm install -g azure-functions-core-tools@4 --unsafe-perm true
   ```

3. **Verify Installation**:  
   ```bash
   func --version
   ```

![Core Tools Version](https://github.com/user-attachments/assets/34a06a21-3854-4cad-be4c-739d0c120a7c)

---

### Step 4: Install Azurite (for Local Development)

```bash
npm install -g azurite
azurite --version
azurite
```

![Azurite Running](https://github.com/user-attachments/assets/e6653c95-b432-4e70-ac2f-2d2022903915)

---

## **Part 2: Create and Test Azure Functions**

### Step 1: Create an HTTP Trigger Function

1. Open VS Code → `HttpTriggerProject` folder.
2. Open Command Palette (`Ctrl+Shift+P`) → **Azure Functions: Create New Project**
3. Choose:
   - **Language**: JavaScript  
   - **Trigger**: HTTP Trigger  
   - **Function Name**: `HttpTriggerFunction`
- Note: Rename the httptrigger1.js to index.js because Azure functions looks for a file with the same name.
#### Replace Code in `index.js`:

```javascript
module.exports = async function (context, req) {
    context.log('JavaScript HTTP trigger function processed a request.');

    const name = req.query.name || (req.body && req.body.name);
    context.res = {
        status: 200,
        body: name ? `Hello, ${name}!` : 'Hello, world!'
    };
};
```

#### Rename the main folder: httptriggerproject, under which index.js and function.json should be present.

#### Create and update `function.json`:

```json
{
    "bindings": [
      {
        "authLevel": "anonymous",
        "type": "httpTrigger",
        "direction": "in",
        "name": "req",
        "methods": ["get", "post"]
      },
      {
        "type": "http",
        "direction": "out",
        "name": "res"
      }
    ],
    "scriptFile": "index.js"  
  }
```

#### Modify or create `host.json`:

```json
{
  "version": "2.0"
}
```

#### Modify or create `package.json`:

```json
{
  "name": "httptriggerproject",
  "version": "1.0.0",
  "scripts": {
    "start": "func start",
    "test": "echo \"No tests yet...\""
  },
  "dependencies": {}
}
```

**Note**: Delete any `index.js` file that gets created automatically.

---

### Test HTTP Function Locally

- Press **F5** to start local server.
- Visit: `http://localhost:7071/api/HttpTriggerFunction?name=John`
- Expected Output:
  ```
  Hello, John!
  ```

---

### Part 3: Create a Timer Trigger Function

1. Open VS Code → `TimerTriggerProject` folder.
2. Open Command Palette → **Azure Functions: Create New Function**
3. Choose:
   - **Trigger Type**: Timer Trigger  
   - **Function Name**: `TimerFunction`  
   - **Schedule**: `"0 * * * * *"` (Every minute)

#### Replace `timerTrigger.js` with `index.js`:

```javascript
module.exports = async function (context, myTimer) {
    const currentTime = new Date().toISOString();
    context.log(`Timer triggered at: ${currentTime}`);
    if (myTimer.isPastDue) {
        context.log('Timer is running late!');
    }
};
```

#### Create `function.json`:

```json
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

#### Create or update `.funcignore`:

```txt
__azurite_db*__.json
__blobstorage__
__queuestorage__
local.settings.json
test
tsconfig.json
.gitignore
.vscode
```

#### Create or update `host.json`:

```json
{
  "version": "2.0"
}
```

#### Create `package.json`:

```json
{
  "name": "timerapp",
  "version": "1.0.0",
  "scripts": {
    "start": "func start"
  },
  "dependencies": {}
}
```

**Verify Folder Structure**  
![Timer Project Structure](https://github.com/user-attachments/assets/227b8e59-48ea-44cc-a943-ee6abfeb10d8)
Rename the main folder: timertriggerproject under which index.js and function.json should be present.
---

### Test Timer Function Locally

- Press **F5** to run.
- Check Terminal log every 5 seconds for:
  ```
  Timer triggered at: <timestamp>
  ```

![Timer Log Output](https://github.com/user-attachments/assets/cb074148-50bb-4594-8e75-fdd45b593689)

---

## **Part 3: Deploy to Azure**

### Step 1: Create Azure Storage Account

1. Go to: [https://portal.azure.com/](https://portal.azure.com/)
2. Search and select **Storage Account** → **Create**.
3. Fill in:
   - **Subscription**, **Resource Group**, **Unique Name**
   - **Region**: Closest to you
   - **Performance**: Standard  
   - **Replication**: LRS  
4. Click **Review + Create**, then **Create**.

---

### Step 2: Get Connection String

1. Go to your Storage Account → **Access Keys**
2. Copy **Connection String** under **key1**

---

### Step 3: Configure `AzureWebJobsStorage`

1. Go to your **Function App** in Azure.
2. Navigate to: **Configuration** → **Application Settings**
3. Click **+ Add**:
   - **Name**: `AzureWebJobsStorage`
   - **Value**: Paste the connection string
4. Click **Save**.

![Environment Variables](https://github.com/user-attachments/assets/2213351c-4a09-42a5-996e-29600e8eb5f7)

---

### Step 4: Deploy Function App from VS Code

1. In VS Code → **Azure Tab**  
2. Find your Function App  
3. Right-click → **Deploy to Function App**

![Deploy to Azure](https://github.com/user-attachments/assets/b3419eb6-49de-4e82-a985-76686d85f37e)

4. Choose the correct local folder (`TimerTriggerProject`)  
5. Confirm and watch the Output window

---

### Step 5: Test Deployed Function

- **HTTP Trigger**:
  - Use provided URL → Test in browser/Postman

- **Timer Trigger**:
  - Logs appear automatically in **Azure Portal** > **Monitor** > **Logs**

---

