Lab 2 : Services in Kubernetes
=============================================================
``` 
vi httpd-pod1.yaml
``` 
```
apiVersion: v1
kind: Pod
metadata:
  name: httpd-pod1
  labels:
    env: prod 
    type: front-end
    app: httpd-ws
spec:
  containers:
  - name: httpd-container
    image: httpd
    ports:
       - containerPort: 80
 
 ```
# Apply the pod definition yaml
 ```
kubectl apply -f httpd-pod1.yaml
 ```
 
# Check the newly created Pod
 ```
kubectl get pods
 ```

----------------------------------------------------------------------
# Task 1  Setup ClusterIP service
----------------------------------------------------------------------

## Create a file named "httpd-svc.yaml" and add the following YAML for a ClusterIP Service
```
vi httpd-svc.yaml
```
```
apiVersion: v1
kind: Service
metadata:
  name: httpd-svc
spec:
  selector:
    env: prod
    type: front-end
    app: httpd-ws
  ports:
  - protocol: TCP
    port: 80
    targetPort: 80
  type: ClusterIP

```
## Apply above definition using below to create a ClusterIP service
```
kubectl apply -f httpd-svc.yaml
```
## Describe the service and verify it has populated the endpoints with IP address matching Pod label
```
kubectl get svc
```
```
kubectl describe svc httpd-svc
```

------------------------------------------------------------------------------
# Task 2  Setup NodePort Service
------------------------------------------------------------------------------

## Modify the service created in the previous task to type NodePort
```
vi httpd-svc.yaml
```
```
apiVersion: v1
kind: Service
metadata:
  name: httpd-svc
spec:
  selector:
    env: prod
    type: front-end
    app: httpd-ws
  ports:
  - protocol: TCP
    port: 80
    targetPort: 80
  type: NodePort
```

## Apply the changes using below command
```
kubectl apply -f httpd-svc.yaml
```
## View details of the modified service
```
kubectl describe svc httpd-svc
```
## Validate connectivity using External IP on NodePort using below or via browser
```
curl <Node-Public-IP>:NodePort
```
![image](https://github.com/user-attachments/assets/7300acf2-918e-4b96-942b-f63a0be753c4)
![image](https://github.com/user-attachments/assets/ca628839-ac17-4e36-9652-c68d8435a974)

--------------------------------------------------------------------------------
# Task 3 Cleanup the resources using below command
----------------------------------------------------------------------------------
## Delete the resources created during the lab:
```
kubectl delete -f httpd-pod.yaml
```
```
kubectl delete -f httpd-svc.yaml
```
