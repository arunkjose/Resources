### Script1: Reading a file line by line
```
echo -e "Line 1\nLine 2\nLine 3" > file.txt
```
```
vi script1.sh
```
```
#!/bin/bash

while IFS= read -r line; do
  echo "$line"
done < file.txt

if [ $? -eq 0 ]; then
  echo "Success"
else
  echo "Fail"
fi
```
```
chmod +x script1.sh
```
```
./script1.sh
```

### Script2:Backup Script
```
mkdir -p /tmp/data
echo "Sample file" > /tmp/data/file1.txt
```
```
vi script2.sh
```
```
#!/bin/bash
# Simple backup script

src="/tmp/data"
dest="/tmp/backup"
date=$(date +%F-%H-%M)

mkdir -p "$dest"
cp -r "$src" "$dest/data-backup-$date"
echo "Backup completed at $date" >> "$dest/backup.log"
```
```
chmod +x script2.sh
```
```
./script2.sh
```
### Script3: User creation
```
vi script3.sh
```
```
#!/bin/bash
# Script to create a new user safely

username="devopsuser"
password="DevOps@123"

# Check if the user already exists
if id "$username" &>/dev/null; then
  echo "User $username already exists."
else
  sudo useradd -m -s /bin/bash "$username"
  echo "$username:$password" | sudo chpasswd
  sudo usermod -aG sudo "$username"
  echo "User $username created and added to sudo group."
fi
```
```
chmod +x script3.sh
```
```
sudo ./ script3.sh
```

### Script4: Update system & Install packages
```
vi script4.sh
```
```
#!/bin/bash
# setup_server.sh

echo "Updating system..."
sudo apt update -y && sudo apt upgrade -y

echo "Installing essential packages..."
sudo apt install -y git curl wget unzip net-tools

echo "Setup complete!"
```
```
chmod +x script4.sh
```
```
./script4.sh
```

### Script5: Log Cleanup
```
vi script5.sh
```
```
#!/bin/bash
# log_cleanup.sh

log_dir="/var/log"
days_old=7

echo "Cleaning up .log files older than $days_old days in $log_dir..."

sudo find "$log_dir" -type f -name "*.log" -mtime +$days_old -exec rm -f {} \;

echo "Old logs cleaned from $log_dir"
```
```
chmod +x script5.sh
```
First try without deleting, to see what it will find:
```
sudo find /var/log -type f -name "*.log" -mtime +7
```
```
./script5.sh
```

### Script6: Check system health
```
vi script6.sh
```
```
#!/bin/bash
# health_check.sh

echo "----- System Health Report -----"

echo "Hostname     : $(hostname)"
echo "Uptime       : $(uptime -p)"
echo "CPU Load     : $(top -bn1 | grep 'load average' | awk '{print $(NF-2), $(NF-1), $NF}')"

echo "Memory Usage :"
free -h

echo "Disk Usage   :"
df -h

echo "--------------------------------"
```
```
chmod +x script6.sh
```
```
./script6.sh
```

### Script7: Auto Restart Failed System Services
```
vi script7.sh
```
```
#!/bin/bash
# restart_failed_services.sh

echo "Checking for failed services..."

# Get a list of failed services
failed_services=$(systemctl list-units --type=service --state=failed | awk '/.service/ {print $1}')

# Loop through each service and restart it
for service in $failed_services; do
  echo "Restarting $service"
  sudo systemctl restart "$service"
done

echo "Done."
```
```
chmod +x script7.sh
```
```
sudo ./script7.sh
```
