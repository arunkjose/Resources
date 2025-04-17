
---

## **PART 1 – Prepare the Control VM**

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

## **PART 2 – Create Ansible Project Directory**

```bash
mkdir ~/azure-ansible-lab && cd ~/azure-ansible-lab
```

---

## **PART 3 – Create the Inventory File**

```bash
vi hosts.ini
```

```
localhost ansible_connection=local
```
---

## **PART 4 – Create the Playbook**

```bash
vi setup_webserver.yml
```

Paste this:

```yaml
---
- name: Setup web server on Azure VM
  hosts: all
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

##  **PART 5 – Run the Playbook**

```bash
ansible-playbook -i hosts.ini setup_webserver.yml
```

Expected output:
- Ansible connects to the localhost(Current machine)
- Installs NGINX
- Deploys a custom HTML page

---

## **PART 6 – Test Your Web Server**

Open the public IP of the **target VM** in a browser:

```text
http://<target-vm-public-ip>
```
```
curl http://localhost
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
