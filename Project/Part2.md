
---

## Phase 5: Install Docker on Ansible VM (Azure Ubuntu)

### Step 1: SSH into Your Ansible VM

Connect to your Azure VM using the SSH key.

```bash
ssh -i mykey.pem azureuser@<Azure_VM_Public_IP>
```

> **Why?** You're accessing the Ansible machine where you'll install Docker and perform all Docker-related tasks.

---

### Step 2: Install Docker using the Official Convenience Script

```bash
# Download Docker's official install script
curl -fsSL https://get.docker.com -o get-docker.sh

# Run the script with root privileges
sudo sh get-docker.sh
```

> **Why?** This is the fastest and safest way to get the latest Docker version on Ubuntu from official sources.

---

### Step 3: Add Your User to the Docker Group

```bash
# Add current user to 'docker' group so we can run Docker without sudo
sudo usermod -aG docker $USER

# Apply changes immediately
newgrp docker
```

> **Why?** Without this, you'll have to type `sudo` before every Docker command. This makes development smoother.

---

### Step 4: Test Docker Installation

```bash
docker --version          # Check Docker version
docker run hello-world    # Verify Docker is working
```

> **Why?** Confirms Docker was installed correctly and can pull/run containers.

---

## Phase 6: Clone Repo and Build Docker Image

---

### Step 1: Clone the GitHub Repository

```bash
git clone https://github.com/comal15/Resources.git
cd Resources/Docker
```

> **Why?** You're pulling the source code and Dockerfile from the right folder in the repo, so you can build the containerized app.

---

### Step 2: Build the Docker Image

```bash
docker build -t quickkart-app:v1 .
```

> **Why?** This command looks for the `Dockerfile` in the current directory and builds a Docker image named `quickkart-app` with tag `v1`.

---

### Step 3: Run the Docker Image Locally (Optional)

```bash
docker run -d -p 8080:80 quickkart-app:v1
```

> **Why?** This lets you verify the app works before pushing it to DockerHub. It maps port `8080` on your machine to port `80` inside the container.

Access it at:

```bash
http://<Azure_VM_Public_IP>:8080
```

---

## Phase 7: Push Image to DockerHub

---
Create a DockerHub Account
Visit https://hub.docker.com/

Click Sign Up

Choose a Docker ID (this will be used in your image names, e.g., docker.io/your-docker-id/imagename)

Verify your email

### Step 1: Log in to DockerHub

```bash
docker login
```

> **Why?** You need to authenticate with DockerHub before pushing images.

---

### Step 2: Tag the Docker Image

```bash
docker tag quickkart-app:v1 <your-dockerhub-username>/quickkart-app:v1
```

> **Why?** DockerHub requires images to be tagged with your username for uploading.

---

### Step 3: Push the Image to DockerHub

```bash
docker push <your-dockerhub-username>/quickkart-app:v1
```

> **Why?** Now your app image is public and ready to be pulled from any Kubernetes environment.

---

## Phase 8: Deploy on KillerKoda CKAD Playground

---

### Step 1: Open [KillerKoda CKAD](https://killercoda.com/playgrounds) and launch the CKAD Playground.

---

### Step 2: Create a Pod YAML File

Save this as `quickkart-pod.yaml`:

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: quickkart
  labels:
    app: quickkart
spec:
  containers:
  - name: quickkart-container
    image: <your-dockerhub-username>/quickkart-app:v1
    ports:
    - containerPort: 80
```

> **Why?** This defines your pod using the custom Docker image you pushed.

---

### Step 3: Create a NodePort Service

Save this as `quickkart-svc.yaml`:

```yaml
apiVersion: v1
kind: Service
metadata:
  name: quickkart-svc
spec:
  type: NodePort
  selector:
    app: quickkart
  ports:
  - protocol: TCP
    port: 80
    targetPort: 80
    nodePort: 30080
```

> **Why?** This service exposes your pod on port `30080`, so you can access it via browser.

---

### Step 4: Deploy to Kubernetes

```bash
kubectl apply -f quickkart-pod.yaml
kubectl apply -f quickkart-svc.yaml
```

> **Why?** These commands apply your Kubernetes configurations.

---

### Step 5: Access the App

Use the browser URL provided by KillerKoda:

```
http://localhost:30080
```

You should now see your **Quickkart App** live and running!

---
