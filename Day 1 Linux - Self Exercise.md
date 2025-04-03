## **Part 1: Working with Directories**  

### **Objective:**  
Practice creating, moving, and copying files and directories in Linux.  

### **Tasks:**  
1. **Create the following directory structure:**  
   ```
   ~/lab/
   ├── dir1/
   ├── dir2/
   │   └── dir3/
   └── dir4/
   ```
   - Use the `mkdir` command to create the directories.  

2. **Create the following files inside the directories:**  
   - `file1.txt` inside `dir1`  
   - `file2.txt` inside `dir2`  
   - `file3.txt` inside `dir2/dir3`  
   - `file4.txt` inside `dir4`  
   - Use the `touch` command to create empty files.  

3. **Move `file1.txt` from `dir1` to `dir2`.**  
   - Use the `mv` command.  

4. **Copy `file2.txt` from `dir2` to `dir4`.**  
   - Use the `cp` command.  

---

## **Part 2: Managing Users and Groups**  

### **Objective:**  
Practice creating users, groups, and managing group memberships.  

### **Tasks:**  
1. **Create two new users: `user1` and `user2`.**  
   - Use the `useradd` command.  

2. **Create a group named `group1` and add `user1` to it.**  
   - Use the `groupadd` and `usermod` commands.  

3. **Add `user2` to `group1`.**  
   - Use the `usermod` command.  

---

## **Part 3: File and Directory Permissions**  

### **Objective:**  
Practice modifying file permissions and ownership.  

### **Tasks:**  
1. **Change the permissions of `file3.txt` so that:**  
   - Owner: Read and write  
   - Group: Read-only  
   - Others: No access  
   - Use the `chmod` command.  

2. **Change the ownership of `file4.txt` to `user1` and its group to `group1`.**  
   - Use the `chown` command.  

---

## **Part 4: Monitoring and Logging**  

### **Objective:**  
Learn how to monitor system processes and view logs.  

### **Tasks:**  
1. **List all currently running processes.**  
   - Use the `ps aux` command.  

2. **Find and terminate a process.**  
   - Use the `ps aux | grep <process>` and `kill <PID>` commands.  

3. **Start, stop, restart, enable, and disable a web server (Apache/Nginx).**  
   - Use the `systemctl` command.  

---

## **Part 5: Basic Commands**  

### **Objective:**  
Practice using fundamental Linux commands for navigation and file operations.  

### **Tasks:**  

1. **Display the current directory path.**  
   - Use the `pwd` command.  

2. **List all files in `~/lab` and its subdirectories in a tree structure.**  
   - Use the `tree ~/lab` command (install `tree` if needed).  

3. **Display detailed information about all files in `dir2`.**  
   - Use the `ls -l ~/lab/dir2` command.  

4. **Search for the word "test" in `file3.txt`.**  
   - First, add text to the file using `echo "This is a test" >> file3.txt`.  
   - Then, use the `grep "test" file3.txt` command.  

5. **Create a new file using Vi and Nano.**  
   - Open Vi and create `testfile.txt` using `vi testfile.txt`.  
   - Add text and save it (`i` to insert, `Esc` to exit insert mode, `:wq` to save and exit).  
   - Open Nano and create `testfile.txt` using `nano testfile.txt`.  
   - Add text and save it (`Ctrl + X`, then `Y`, then `Enter`).  

---
### **Bonus Challenges (Optional)**  
* Verify the changes using `ls -l` after each step.
* Use `cat`, `nano`, or `echo` to add content to the files.  
* Try logging in as `user1` and `user2` to test their access permissions.  

---
