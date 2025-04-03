# **Linux Process Management & Monitoring Cheat Sheet**  

---

## **Lab 4: Process Management**  

### **Task 1: Working with Linux Processes**  

#### **1. Kill Background Processes**  
```bash
jobs  
kill <PID>  
```
- Find **PID** using `ps` or `jobs`.  

#### **2. View Running Processes**  
```bash
ps  
ps all  
ps aux  
```

#### **3. Search for a Specific Process & Kill It**  
```bash
ps aux | grep cat  
kill <PID>  
```
- `kill <PID>` → Terminates the process.  

---

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
systemctl status httpd  # For Apache  
systemctl status nginx  # For Nginx  
```

#### **2. Stop & Disable the Web Server**  
```bash
systemctl stop httpd  # For Apache  
systemctl disable httpd  

systemctl stop nginx  # For Nginx  
systemctl disable nginx  

systemctl status httpd  # Check status after stopping  
systemctl status nginx  
```

#### **3. Start & Enable the Web Server**  
```bash
systemctl start httpd  
systemctl enable httpd  

systemctl start nginx  
systemctl enable nginx  

systemctl status httpd  
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

### **2. Using `journalctl` (Systemd Logs)**  

#### **Basic Commands**  
```bash
journalctl        # View system logs  
journalctl -u httpd  # View logs for Apache  
journalctl -u nginx  # View logs for Nginx  
journalctl -b    # View logs since last boot  
journalctl -f    # View last 10 log entries (follow live updates)  
```

---

## **Quick Command Reference**  

| **Command** | **Description** |
|------------|----------------|
| `jobs` | View background jobs |
| `fg %1` | Bring job to foreground |
| `kill <PID>` | Kill a process |
| `ps aux | grep <process>` | Find a process |
| `systemctl status httpd` | Check Apache web server status |
| `systemctl status nginx` | Check Nginx web server status |
| `top` | Monitor system processes |
| `htop` | Visual process monitoring |
| `journalctl -b` | View logs since last boot |
| `cd /var/log && ls -l` | View system logs |

---
