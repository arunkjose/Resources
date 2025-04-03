# **Linux Process Management & Monitoring Cheat Sheet**  

---

## **Lab 4: Process Management**  .  

#### **1. View Running Processes**  
```bash
ps  
ps all  
ps aux  
```
# **Ubuntu Nginx & Apache2 Installation Cheat Sheet**  

## **1. Update Package Lists**
```sh
sudo apt update
sudo apt upgrade -y
```

---

## **2. Install Nginx**
### Install & Start
```sh
sudo apt install nginx -y
sudo systemctl start nginx
sudo systemctl enable nginx
```
### Check Status & Reload
```sh
sudo systemctl status nginx
sudo systemctl reload nginx  # Reload config without stopping service
```
### Verify Installation
```sh
nginx -v  # Check version
```

---

## **3. Install Apache2**
### Install & Start
```sh
sudo apt install apache2 -y
sudo systemctl start apache2
sudo systemctl enable apache2
```
### Check Status & Restart
```sh
sudo systemctl status apache2
sudo systemctl restart apache2
sudo systemctl reload apache2  # Reload config without stopping service
```
### Verify Installation
```sh
apache2 -v  # Check version
```
---

## **4. Common APT & APT-GET Operations**
### **Package Management**
```sh
sudo apt update          # Update package lists
sudo apt upgrade -y      # Upgrade installed packages
sudo apt autoremove -y   # Remove unnecessary dependencies
sudo apt clean           # Clear package cache
```
### **Install & Remove Packages**
```sh
sudo apt install <package_name> -y   # Install a package
sudo apt remove <package_name> -y    # Remove a package (keeps config files)
sudo apt purge <package_name> -y     # Remove package & config files
```
### **Search & Information**
```sh
apt search <package_name>     # Search for a package
apt show <package_name>       # Show package details
```
### **Service Management**
```sh
sudo systemctl start <service_name>   # Start a service
sudo systemctl stop <service_name>    # Stop a service
sudo systemctl restart <service_name> # Restart a service
sudo systemctl enable <service_name>  # Enable auto-start
sudo systemctl disable <service_name> # Disable auto-start
```
### **Task 2: Working with System Services**  

#### **Basic `systemctl` Commands**  

| **Command** | **Alternative** | **Description** |
|------------|---------------|----------------|
| `systemctl start <service>` | `service <name> start` | Start a service |
| `systemctl stop <service>` | `service <name> stop` | Stop a service |
| `systemctl restart <service>` | `service <name> restart` | Restart a service |
| `systemctl reload <service>` | `service <name> reload` | Reload configuration |
| `systemctl status <service>` | `service <name> status` | Check service status |
| `systemctl is-active <service>` | | Check if a service is running |
| `systemctl list-units --type service --all` | `service --status-all` | List all services |

#### **1. Check the Status of the Web Server (Apache or Nginx)**  
```bash
systemctl status apache2  # For Apache  
systemctl status nginx  # For Nginx  
```

#### **2. Stop & Disable the Web Server**  
```bash
systemctl stop apache2  # For Apache  
systemctl disable apache2  

systemctl stop nginx  # For Nginx  
systemctl disable nginx  

systemctl status apache2  # Check status after stopping  
systemctl status nginx  
```

#### **3. Start & Enable the Web Server**  
```bash
systemctl start apache2  
systemctl enable apache2  

systemctl start nginx  
systemctl enable nginx  

systemctl status apache2  
systemctl status nginx  
```

---

## **Lab 5: Monitoring & Logging**  

### **Task 1: `top` Command (Process Monitoring)**  
```bash
top  
```
#### **`top` Row Details:**  
1. **Row 1:** Current time, uptime, users, load avg  
2. **Row 2:** Total processes and their states  
3. **Row 3:** CPU utilization details  
4. **Row 4:** Physical memory usage  
5. **Row 5:** Swap memory usage  

#### **Useful Shortcuts in `top`**  
| Shortcut | Action |
|----------|--------|
| `t` | Show/hide task/cpu line |
| `m` | Show/hide RAM & SWAP details |
| `R` | Sort by PID |
| `P` | Sort by CPU usage |
| `M` | Sort by RAM usage |
| `e` | Show/hide command path |
| `r` | Renice a process (change priority) |
| `k` | Kill a process (enter PID) |
| `W` | Save configuration |
| `q` | Quit `top` |
| `h` | Help |

---

### **Task 2: `htop` Command (Improved `top`)**  

#### **1. Install `htop` (if not installed)**
```bash
yum install htop -y  
```
#### **2. Run `htop`**
```bash
htop  
```
- **Features:**  
  - Better visualization of real-time data.  
  - Allows process management (increase/decrease priority, sort, etc.).  

#### **`htop` Keyboard Shortcuts**  
| Key | Action |
|-----|--------|
| `F1` | Help |
| `F2` | Setup |
| `F3` | Search |
| `F4` | Filter |
| `F5` | Tree View |
| `F6` | Sort By |
| `F7` | Increase priority |
| `F8` | Decrease priority |
| `F9` | Kill process |
| `F10` | Quit |

---

### **Task 3: Listing Running Processes**  
```bash
ps  
ps all  
ps aux  
```

---

## **System Logging & Journaling**  

### **1. System Logs Location**  
```bash
cd /var/log  
```
- Linux saves logs in `/var/log` due to default config (`/etc/rsyslog.conf`).  

#### **Common Log Files**  
| Log File | Purpose |
|----------|---------|
| `/var/log/syslog` | General system logs |
| `/var/log/messages` | General messages, startup logs |
| `/var/log/auth.log` | Authentication logs |
| `/var/log/secure` | Security-related logs |
| `/var/log/kern.log` | Kernel logs |
| `/var/log/cron` | Cron job logs |
| `/var/log/httpd/access.log` | Apache access logs |
| `/var/log/httpd/error.log` | Apache error logs |
| `/var/log/nginx/access.log` | Nginx access logs |
| `/var/log/nginx/error.log` | Nginx error logs |

---

