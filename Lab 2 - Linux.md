# **Linux User & Group Management Cheat Sheet**

---
Switch to root user
```
sudo su
```
## **Task 1: Managing Users**  

### **1. Add Users**
- Create two users: `user1` and `user2`  
  ```bash
  useradd user1  
  useradd user2  
  ```

### **2. Set Passwords for Users**
- Assign passwords to the users  
  ```bash
  passwd user1  
  passwd user2  
  ```

### **3. Check User IDs and Group IDs**
- Fetch UID and GID for the users  
  ```bash
  id user1  
  id user2  
  ```

### **4. Switch Between Users**
- Switch to `user1` and verify  
  ```bash
  su user1  
  whoami  
  exit  
  ```
- Switch to `user2` and verify  
  ```bash
  su user2  
  whoami  
  exit  
  ```

### **5. Search for Specific Users**
- Use `grep` to filter user details  
  ```bash
  cat /etc/passwd | grep user1  
  cat /etc/passwd | grep user2  
  ```

### **6. Modify User Properties**
- Modify the shell and add a comment for `user2`  
  ```bash
  usermod -c "IT Admin" user2  
  usermod -s /bin/sh user2  
  cat /etc/passwd | grep user2  
  ```

### **7. Create a User with Custom UID, GID & Home Directory**
- Add `user3` with specific properties  
  ```bash
  useradd user3 -c "HR Admin" -d /mnt/user3 -u 30003 -g 40004  
  ```
- Verify creation  
  ```bash
  cat /etc/passwd | grep user3  
  ```

### **8. Delete Users**
- Delete `user1` and `user2` along with their home directories  
  ```bash
  userdel -r user1  
  userdel -r user2  
  ```
- Verify deletion  
  ```bash
  tail /etc/passwd  
  ```

---

## **Task 2: Managing Groups**  

### **1. Create Users and Verify**
- Create `testuser1` and `testuser2`  
  ```bash
  useradd testuser1  
  useradd testuser2  
  tail /etc/passwd  
  ```

### **2. View Group Information**
- Display contents of `/etc/group`  
  ```bash
  cat /etc/group  
  tail /etc/group  
  ```

### **3. Create a New Group**
- Create a new group named `IT-group`  
  ```bash
  groupadd IT-group  
  ```

### **4. Add Users to a Group**
- Add `testuser1` and `testuser2` to `IT-group`  
  ```bash
  usermod -G IT-group testuser1  
  usermod -G IT-group testuser2  
  ```

### **5. Verify Users in Group**
- Check `/etc/group` to confirm  
  ```bash
  tail /etc/group  
  ```

### **6. Create a Group with Custom GID**
- Create `HR-group` with a specific GID  
  ```bash
  groupadd HR-group -g 40055  
  ```
- Verify creation  
  ```bash
  tail /etc/group  
  ```

### **7. Create a User and Add to a Group**
- Create `testuser3` and add to `IT-group`  
  ```bash
  useradd testuser3  
  gpasswd -a testuser3 IT-group  
  ```
- Verify  
  ```bash
  tail /etc/group  
  ```

### **8. Remove Users from a Group**
- Remove `testuser1` and `testuser2` from `IT-group`  
  ```bash
  gpasswd -d testuser2 IT-group  
  gpasswd -d testuser1 IT-group  
  ```
- Verify  
  ```bash
  tail /etc/group  
  ```

### **9. Delete Groups**
- Delete `IT-group`  
  ```bash
  groupdel IT-group  
  ```
- Verify  
  ```bash
  tail /etc/group  
  ```

---

## **Task 3: File Permissions**

### **1. Create a Directory and a File**
- Create `testfolder` and `testfile`  
  ```bash
  mkdir testfolder  
  touch testfile  
  ```

### **2. Modify Directory Permissions**
- Allow group members to create and delete files  
  ```bash
  ls -ld testfolder/  
  chmod g+w testfolder/  
  ls -ld testfolder/  
  chmod o-rwx testfolder/  
  ls -ld testfolder/  
  ```

### **3. Remove All Permissions**
- Remove all permissions for group and others  
  ```bash
  chmod go-rwx testfolder  
  ls -ld testfolder  
  ```

### **4. Change File Permissions**
- Check and modify `testfile` permissions  
  ```bash
  ls -ld testfile  
  chmod a-rwx testfile  
  ls -ld testfile  
  ```

### **5. Grant Full Access**
- Grant full access to all users  
  ```bash
  chmod a+rwx testfile  
  ls -ld testfile  
  ```

### **6. Set Specific Permissions Using Numeric Values**
- Change permissions using numeric mode  
  ```bash
  chmod 644 testfile  
  ls -ld testfile  
  chmod 755 testfolder  
  ls -ld testfolder  
  ```

### **7. Change Ownership & Group**
- Assign a new owner and group to `testfolder`  
  ```bash
  ls -ld testfolder/  
  chown new-user3 testfolder/  
  ls -ld testfolder/  
  chgrp test-group testfolder/  
  ls -ld testfolder/  
  ```

---

## **Summary of Important Commands**
| Command | Description |
|---------|-------------|
| `useradd username` | Create a new user |
| `passwd username` | Set password for a user |
| `id username` | Display user and group ID |
| `su username` | Switch to another user |
| `usermod -c "Comment" username` | Modify user details |
| `userdel -r username` | Delete a user |
| `groupadd groupname` | Create a new group |
| `usermod -G groupname username` | Add user to a group |
| `gpasswd -d username groupname` | Remove user from a group |
| `groupdel groupname` | Delete a group |
| `ls -ld filename` | View file permissions |
| `chmod permissions filename` | Change file permissions |
| `chown new-owner filename` | Change file owner |
| `chgrp new-group filename` | Change file group |

