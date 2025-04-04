---

# **Linux Command Cheatsheet**

##  **Exercise 1: Basic Commands**
1. **Create a new directory**  
   ```bash
   mkdir my_directory
   ```
2. **List files in the current directory**  
   ```bash
   ls
   ```
3. **Change into the directory**  
   ```bash
   cd my_directory
   ```
4. **Create a new file**  
   ```bash
   touch my_file.txt
   ```
5. **Copy file to another directory**  
   ```bash
   cp my_file.txt backup/
   ```
6. **Remove a file**  
   ```bash
   rm my_file.txt
   ```
7. **Find all `.txt` files recursively**  
   ```bash
   find . -name "*.txt"
   ```

---

## **Exercise 2: Files and Directories**
1. **Create a file**  
   ```bash
   touch my_notes.txt
   ```
2. **Rename a file**  
   ```bash
   mv my_notes.txt new_notes.txt
   ```
3. **Move file to another directory**  
   ```bash
   mv new_notes.txt backup/
   ```
4. **Display directory permissions**  
   ```bash
   ls -l backup
   ```
5. **Change permissions (Owner: RWX, Others: Read-only)**  
   ```bash
   chmod 755 backup
   ```
6. **Check file ownership**  
   ```bash
   ls -l new_notes.txt
   ```
7. **Change ownership of a file**  
   ```bash
   chown john:users new_notes.txt
   ```

---

## **Exercise 3: Users and Groups**
1. **Create a user**  
   ```bash
   sudo useradd john
   ```
2. **Set a password**  
   ```bash
   sudo passwd john
   ```
3. **Add user to sudo group**  
   ```bash
   sudo usermod -aG sudo john
   ```
4. **Switch to another user**  
   ```bash
   su john
   ```
5. **Check user info**  
   ```bash
   id
   ```
6. **Delete a user**  
   ```bash
   sudo userdel john
   ```

---

##  **Exercise 4: Permissions**
1. **Create a script file**  
   ```bash
   touch my_script.sh
   ```
2. **Set script permissions (Owner: RWX, Others: Read-only)**  
   ```bash
   chmod 755 my_script.sh
   ```
3. **Change ownership of a file**  
   ```bash
   chown john:users my_script.sh
   ```

---

## **Exercise 5: Storage**
1. **Check available disk space**  
   ```bash
   df -h
   ```
2. **Create a new partition (Interactive Mode)**  
   ```bash
   sudo fdisk /dev/sdX
   ```
3. **Format the partition to ext4**  
   ```bash
   sudo mkfs.ext4 /dev/sdX1
   ```
4. **Mount the partition**  
   ```bash
   sudo mount /dev/sdX1 /mnt/my_partition
   ```
5. **Unmount the partition**  
   ```bash
   sudo umount /mnt/my_partition
   ```

---

## **Exercise 6: Archive and Compression**
1. **Create a compressed `.tar.gz` archive**  
   ```bash
   tar -czvf my_directory.tar.gz my_directory
   ```
2. **Extract `.tar.gz` to a new directory**  
   ```bash
   tar -xzvf my_directory.tar.gz -C extracted
   ```
3. **Create a zip archive**  
   ```bash
   zip -r my_directory.zip my_directory
   ```
4. **Extract a zip archive**  
   ```bash
   unzip my_directory.zip -d extracted
   ```

---

## **Exercise 12: crontab Command**
1. **Schedule a script to run daily at 2 AM**  
   ```bash
   crontab -e
   0 2 * * * /path/to/cleanup.sh
   ```
2. **List current user's crontab jobs**  
   ```bash
   crontab -l
   ```
3. **Remove all crontab jobs**  
   ```bash
   crontab -r
   ```

---

## **Exercise 13: Package Manager**
1. **Update and upgrade packages**  
   ```bash
   sudo apt update && sudo apt upgrade
   ```
2. **Install `htop`**  
   ```bash
   sudo apt install htop
   ```
3. **Search for a package**  
   ```bash
   apt search nginx
   ```
4. **Remove a package**  
   ```bash
   sudo apt remove htop
   ```

---

## **Exercise 14: Networking**
1. **Display network interfaces & IPs**  
   ```bash
   ip addr
   ```
2. **Ping an IP to check connectivity**  
   ```bash
   ping 8.8.8.8
   ```
---

## **Additional: cron Command Examples**
1. **Edit crontab**  
   ```bash
   crontab -e
   ```
2. **Schedule a task every minute**  
   ```bash
   * * * * * echo "Cron task executed at $(date)" >> ~/cron_log.txt
   ```
3. **Verify crontab jobs**  
   ```bash
   crontab -l
   ```
4. **Schedule a script daily at 8:00 AM**  
   ```bash
   0 8 * * * ~/my_script.sh
   ```

---
