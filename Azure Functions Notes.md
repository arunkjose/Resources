
---

## **Key Files in Azure Functions Project**

| File Name         | Purpose                                                                                          | Required |
|-------------------|--------------------------------------------------------------------------------------------------|----------|
| `index.js`        | Contains the **main logic** of your Azure Function. This is the file that Azure executes.        | ✅ Yes    |
| `function.json`   | Defines the **trigger type**, direction (input/output), parameter names, and script to run.      | ✅ Yes    |
| `host.json`       | Contains **global settings** for all functions in the project. Controls behavior like logging.   | ✅ Yes    |
| `package.json`    | Describes your **Node.js project**, dependencies, and scripts to run your function locally.       | ✅ Yes (for JavaScript/Node) |

---

## **Detailed Explanation of Each File**

---

### `index.js`
> **This is the entry point for your Azure Function.**

- Azure runs the code inside this file whenever the function is triggered.
- You must export a function using `module.exports`.
- It receives `context` and `req`/`myTimer` (based on the trigger).

#### Example (HTTP Trigger):
```javascript
module.exports = async function (context, req) {
    context.log('HTTP trigger executed.');
    const name = req.query.name || (req.body && req.body.name);
    context.res = {
        status: 200,
        body: name ? `Hello, ${name}!` : 'Hello, world!'
    };
};
```

#### Example (Timer Trigger):
```javascript
module.exports = async function (context, myTimer) {
    const currentTime = new Date().toISOString();
    context.log(`Timer ran at: ${currentTime}`);
    if (myTimer.isPastDue) {
        context.log('Timer is late!');
    }
};
```

---

### `function.json`
> **This file defines how the function is triggered and what bindings are used.**

- Each function has its **own `function.json`** inside its own folder.
- Maps input/output bindings like `req`, `res`, `myTimer`, etc.
- Links the trigger to `index.js` using `"scriptFile"`.

#### HTTP Trigger Example:
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

#### Timer Trigger Example:
```json
{
  "bindings": [
    {
      "name": "myTimer",
      "type": "timerTrigger",
      "direction": "in",
      "schedule": "*/5 * * * * *"
    }
  ],
  "scriptFile": "index.js"
}
```

---

### `host.json`
> **Global configuration for your function app.**

- Applies to **all functions** in the same project.
- Can control logging, retries, extension bundles, and more.

#### Minimal required version:
```json
{
  "version": "2.0"
}
```

> You can later extend this to control host behaviors like:
```json
{
  "version": "2.0",
  "logging": {
    "applicationInsights": {
      "samplingSettings": {
        "isEnabled": true
      }
    }
  }
}
```

---

### `package.json`
> **Defines your Node.js project.** Required to run locally.

- Lists project metadata, scripts, and dependencies.
- Helps run the function using `npm start` or `func start`.

#### Example:
```json
{
  "name": "httptriggerproject",
  "version": "1.0.0",
  "scripts": {
    "start": "func start"
  },
  "dependencies": {}
}
```

---

## ✅ Summary

| File           | What It Does                                          | Scope             |
|----------------|-------------------------------------------------------|-------------------|
| `index.js`     | Function logic/code                                   | Per function      |
| `function.json`| Describes trigger/bindings and links to `index.js`   | Per function      |
| `host.json`    | Global host config for the function app               | Project-wide      |
| `package.json` | Node.js metadata, scripts, and dependencies           | Project-wide      |

---

