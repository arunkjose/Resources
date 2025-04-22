
---

## Task: Create a Linux VM on Azure and Install Docker on Ubuntu

---

## Part 1: Create Ubuntu 18.04 VM on Azure

### Step 1: Log in to Azure
- Go to [https://portal.azure.com](https://portal.azure.com)
- Sign in with your Azure credentials

---

### Step 2: Create the VM
1. Go to **Virtual Machines** → Click **Create** → **Azure virtual machine**
2. Fill in the following:
   - **Subscription**: (your subscription)
   - **Resource Group**: docker-rg
   - **Name**: e.g., `ubuntu-docker-vm`
   - **Region**: Cannada Central
   - **Image**: Select **Ubuntu Server 18.04 LTS**
   - **Size**: Choose B1s (small and fits Free Tier)
   - **Authentication**:
     - Type: SSH or Password
     - Username: `ubuntu`
     - Password or upload SSH key
   - **Public Inbound Ports**: Select `Allow selected ports` → check **SSH (22)**

3. Click **Review + Create** → then **Create**

---

## Part 2: Connect to Your VM

Once the deployment is complete:

### Step 3: SSH into VM

- Get the **public IP** from the VM overview
- Open terminal and run:

```bash
ssh ubuntu@<Your_Public_IP>
```

Or use PuTTY on Windows if you're using a password.

---

## Part 3: Install Docker on Ubuntu 18.04

### Step 4: Set Hostname (optional)
```bash
sudo hostnamectl set-hostname docker
```

---

### Step 5: Switch to root (optional)
```bash
sudo su
```

---

### Step 6: Update packages
```bash
apt update -y
```

---

### Step 7: Install curl
```bash
apt install curl -y
```

---

### Step 8: Install Docker using official script
```bash
curl -fsSL https://get.docker.com | sh
```

---

### Step 9: Check Docker status
```bash
systemctl status docker
```

> If it’s **not active**, run:
```bash
systemctl start docker
```

---

### Step 10: Add `ubuntu` user to `docker` group
```bash
sudo usermod -aG docker ubuntu
```

> Then log out and log back in (or run `newgrp docker`)

---

### Step 11: Verify Docker version
```bash
docker --version
```
---
