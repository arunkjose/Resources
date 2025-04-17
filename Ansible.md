
---

## **PART 1 – Provision the Target VM Using Azure Portal**

1. Login to [https://portal.azure.com](https://portal.azure.com)
2. Navigate to **Virtual Machines > + Create**
3. Use these settings:
   - **Name**: `target-vm`
   - **Region**: canada central
   - **Image**: Ubuntu 20.04 LTS
   - **Size**: Standard B1s or larger
   - **Authentication**: SSH Public Key (use the same key as control VM)
   - **Inbound ports**: Allow SSH (22) and HTTP (80)
4. Click **Review + Create > Create**

**Important:** Make sure both VMs are in the same region/resource group.

---

## **PART 2 – SSH into the Control VM**

'From your local machine CMD or git bash'
---

## **PART 3 – Prepare the Control VM**

### Update the system:

```bash
sudo apt update && sudo apt upgrade -y
```

### Install Python, pip, and Ansible:

```bash
sudo apt install -y python3 python3-pip ansible
```

### Install Azure CLI:
Note: If done already ignore and move to next step
```bash
curl -sL https://aka.ms/InstallAzureCLIDeb | sudo bash
```

### Verify Az login
```
az group list --output table
```

### Install Boto3 (for Azure integrations):

```bash
pip3 install boto3
```

---

## **PART 4 – Create Ansible Project Directory**

```bash
mkdir ~/azure-ansible-lab && cd ~/azure-ansible-lab
```

---

## **PART 5 – Create the Inventory File**

```bash
nano hosts.ini
```

Paste this (replace IP):

```ini
[target_vm]
<target-vm-public-ip> ansible_user=azureuser ansible_ssh_private_key_file=~/.ssh/id_rsa
```

> Replace `<target-vm-public-ip>` with the actual public IP of the new target VM.  
> Make sure `.ssh/id_rsa` is the private key matches the public key used during VM creation.

---

## **PART 6 – Create the Playbook**

```bash
vi setup_webserver.yml
```

Paste this:

```yaml
---
- name: Setup web server on Azure VM
  hosts: target_vm
  become: true

  tasks:
    - name: Update APT cache
      apt:
        update_cache: yes

    - name: Install NGINX
      apt:
        name: nginx
        state: present

    - name: Start and enable NGINX
      service:
        name: nginx
        state: started
        enabled: yes

    - name: Create custom index page
      copy:
        dest: /var/www/html/index.html
        content: |
          <html>
            <head><title>Welcome</title></head>
            <body>
              <h1>This VM is managed by Ansible!</h1>
            </body>
          </html>
```

---

##  **PART 7 – Run the Playbook**

```bash
ansible-playbook -i hosts.ini setup_webserver.yml
```

Expected output:
- Ansible connects via SSH
- Installs NGINX
- Deploys a custom HTML page

---

## **PART 8 – Test Your Web Server**

Open the public IP of the **target VM** in a browser:

```text
http://<target-vm-public-ip>
```

You should see:

> **"This VM is managed by Ansible!"**
---

## **Cleanup**

To delete the VM when done:

```bash
az vm delete --resource-group <your-resource-group> --name target-vm --yes
```

---
