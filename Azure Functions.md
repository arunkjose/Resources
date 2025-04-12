
---
## **Lab: Deploy and Test Azure Function on Azure Portal**

---

### **Prerequisites**
- An active Azure subscription.
- A web browser to access the Azure Portal.

---

### **Step 1: Create a Function App in Azure Portal**
1. **Log into the Azure Portal**: Navigate to [https://portal.azure.com/](https://portal.azure.com/).
   
2. **Create a Function App**:
   - In the left sidebar, click **Create a resource**.
   - In the **Search the Marketplace** box, type **Function App** and click on **Function App** from the results.
   - Click **Create**.
   
3. **Configure the Function App**:
   - **Subscription**: Choose your Azure subscription.
   - **Resource Group**: Either select an existing resource group or create a new one.
   - **Function App Name**: Enter a globally unique name (e.g., `my-first-function-app`).
   - **Publish**: Select **Code**.
   - **Runtime Stack**: Choose **Node.js** for JavaScript or **Python**, based on your preference.
   - **Region**: Choose the region closest to you.
   
4. **Review and Create**:
   - Click **Next** through the tabs until you reach the **Review + Create** section.
   - Review the details, and then click **Create**.

   Wait for the deployment to complete.

---

### **Step 2: Create a Function in the Function App**
1. Once the **Function App** is created, navigate to it in the **Azure Portal**.
   
2. In the left sidebar, under **Functions**, click **+ Add** to create a new function.
   
3. Select **In-portal** and click **Continue**.
   
4. Choose the **HTTP trigger** template.
   
5. **Name your Function** (e.g., `HttpExample`).
   
6. Set the **Authentication Level** to **Anonymous**.
   
7. Click **Create**.

---

### **Step 3: Add Code to Your HTTP Trigger**
1. After the function is created, you'll be taken to the **Function Editor**.
   
2. For **JavaScript (Node.js)**, the default code should be:

   ```javascript
   module.exports = async function (context, req) {
       context.log('JavaScript HTTP trigger function processed a request.');
       
       const name = req.query.name || (req.body && req.body.name);
       context.res = {
           body: name ? `Hello, ${name}!` : 'Hello, world!'
       };
   };
   ```

3. For **Python**, the default code should be:

   ```python
   import logging
   import azure.functions as func

   def main(req: func.HttpRequest) -> func.HttpResponse:
       logging.info('Python HTTP trigger function processed a request.')

       name = req.params.get('name')
       if not name:
           try:
               req_body = req.get_json()
           except ValueError:
               pass
           else:
               name = req_body.get('name')

       return func.HttpResponse(f"Hello, {name}!", status_code=200)
   ```

4. **Save** the code by clicking on **Save** at the top of the editor.

---

### **Step 4: Test Your Function**
1. In the **Azure Portal**, navigate back to your **Function App**.
   
2. Under **Functions**, click on your function (`HttpExample`).
   
3. At the top of the function’s page, click **Copy URL** to copy the **Function URL**.

---

### **Step 5: Test the Function Using a Browser or Postman**
#### **Test in Browser**:
1. Open your browser and paste the copied URL into the address bar. 
   Example URL format:
   ```
   https://<your-function-app-name>.azurewebsites.net/api/HttpExample?name=John
   ```
   
2. The response should be:
   ```
   Hello, John!
   ```

---

### **Step 6: Monitor the Function**
1. In the **Azure Portal**, go to your **Function App**.
   
2. Under **Monitoring**, click **Application Insights**.
   
3. If you haven't enabled **Application Insights** yet, you'll be prompted to enable it. Follow the on-screen prompts.
   
4. Once enabled, you can view detailed logs, execution times, success/failure rates, and more.

---

---

### **Summary of the Lab**
- You created a **Function App** in the **Azure Portal**.
- You deployed an **HTTP-triggered function** and tested it by passing query parameters via a browser or Postman.
- You enabled **Application Insights** to monitor your function’s performance.

---
