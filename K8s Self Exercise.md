
---

### Lab: Deploy NGINX and Expose via NodePort

#### **Step 1: Create the Deployment YAML**

Create a file named `nginx-deployment.yaml`:

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment
spec:
  replicas: 1
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx
        image: nginx:latest
        ports:
        - containerPort: 80
```

#### **Step 2: Create the NodePort Service YAML**

Create another file named `nginx-service.yaml`:

```yaml
apiVersion: v1
kind: Service
metadata:
  name: nginx-service
spec:
  type: NodePort
  selector:
    app: nginx
  ports:
    - protocol: TCP
      port: 80
      targetPort: 80
      nodePort: 30080  # You can change this to any port between 30000–32767
```

#### **Step 3: Apply the YAML files**

Run these commands to deploy:

```bash
kubectl apply -f nginx-deployment.yaml
kubectl apply -f nginx-service.yaml
```

#### **Step 4: Access NGINX via Browser or curl**

In killerkoda
Go to traffic ports -> add the custom port: 30080

Note: Killerkoda doesn't provide any IP address
---

### Check Everything

```bash
kubectl get pods
kubectl get svc
```

You should see a pod running and the NodePort service exposing port 30080.

---
### Cleanup
```
kubectl delete deploy nginx-deployment
```
```
kubectl delete svc nginx-service
```
