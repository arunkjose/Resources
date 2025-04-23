Lab 3 : Deployment
=============================================================

----------------------------------------------------------------------
# Task 1: Write a Deployment yaml and Apply it
----------------------------------------------------------------------
## Create a file named dep-nginx.yaml using content given below
```
vi dep-nginx.yaml
```
## Paste the following content into the file:
```
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-dep
  labels:
    app: nginx-dep
spec:
  replicas: 3
  strategy:
    type: Recreate
  selector:
    matchLabels:
      app: nginx-app
  template:
    metadata:
      labels:
        app: nginx-app
    spec:
      containers:
      - name: nginx-ctr
        image: nginx:1.12.2
        ports:
        - containerPort: 80

```
## Save and exit the editor
## Apply the Deployment yaml created in the previous step
```
kubectl apply -f dep-nginx.yaml
```
## View the objects created by Kubernetes Deployment and ReplicaSet 
```
kubectl get deployments
```
------------------------------------------------------------------------------
# Task 2: Scaling of Deployments
------------------------------------------------------------------------------
## View the number of Pod replicas created by the Deployment
```
kubectl get deployments
```
```
kubectl get pods
```
## Scale up the deployment to have 8 Pod replicas
```
kubectl scale deployment nginx-dep --replicas=8
```
## Check the Pods and deployment to and verify that the number of Pod replicas are 8
```
kubectl get deployments
```
```
kubectl get pods
```
## Scale down the deployments to 2 Pod replicas
```
kubectl scale deployment nginx-dep --replicas=2
```
## Check the Pods and deployment to and verify that the number of Pod replicas are down to 2
```
kubectl get deployments
```
```
kubectl get pods
```

-----------------------------------------------------------------------------
# Task 3 Cleanup the resources using command below
-----------------------------------------------------------------------------
## Delete the resources created during the lab:
```
kubectl delete -f dep-nginx.yaml
```
