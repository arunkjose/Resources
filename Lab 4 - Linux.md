# **Linux Storage Management Cheat Sheet**  

---

## **Lab 3: Linux Storage**  

### **Task 1: Create an Additional Primary Partition on Linux**  

#### **1. Create a New Partition**  
- Run `fdisk` with the target hard drive  
  ```bash
  lsblk  
  fdisk /dev/xvdb  
  ```
- Inside `fdisk`, follow these steps:  
  - Press **`n`** → Create a new partition  
  - Press **`p`** → Select primary partition  
  - Press **`1`** → Assign partition number 1  
  - Set start & end sectors (default: press Enter)  
  - Define partition size (e.g., `+5G` for 5GB)  
  - Press **`w`** to write changes  

#### **2. Verify the New Partition**
- Check if the partition was created  
  ```bash
  fdisk -l /dev/xvdb  
  ```

#### **3. Notify the OS of Partition Changes**
- Use `partprobe` to detect the partition table  
  ```bash
  partprobe  
  ```

#### **4. Format the Partition**
- Format as `ext4`  
  ```bash
  mkfs.ext4 /dev/xvdb1  
  ```

#### **5. Mount the Partition**
- Create a mount point and mount the partition  
  ```bash
  mkdir /mnt/ext4  
  mount /dev/xvdb1 /mnt/ext4  
  ```

#### **6. Verify the Mounted Partition**
- Check mounted partitions  
  ```bash
  df -h  
  lsblk  
  ```

#### **7. Make Mounting Permanent**
- Add an entry to `/etc/fstab`  
  ```bash
  echo "/dev/xvdb1 /mnt/ext4 ext4 defaults 0 0" >> /etc/fstab  
  cat /etc/fstab  
  ```

---

### **Delete the Partition**  

#### **1. Remove Auto-Mount Entry**  
- Edit `/etc/fstab` and remove the last line  
  ```bash
  vi /etc/fstab  
  ```
  *(Press `i` to edit, delete the line, then `ESC`, `:wq` to save.)*

#### **2. Unmount the Partition**
- Unmount the partition  
  ```bash
  umount /dev/xvdb1  
  ```

#### **3. Delete the Partition**
- Open `fdisk`  
  ```bash
  fdisk /dev/xvdb  
  ```
- Inside `fdisk`:  
  - Press **`d`** → Delete partition  
  - Select partition number (e.g., `1`)  
  - Press **`w`** to write changes  

#### **4. Verify Deletion**
- Check if the partition is deleted  
  ```bash
  lsblk  
  fdisk -l /dev/xvdb  
  ```

---


## **Task 2: Archive & Compression**  

#### **1. Create and Enter Archive Directory**
```bash
mkdir archive  
cd archive  
```

#### **2. Copy Files for Archiving**
```bash
cp /etc/passwd testfile  
cp /etc/passwd file1  
cp /etc/passwd file2  
cp /etc/passwd file3  
ls -l  
```

#### **3. Create an Archive with `tar`**
- Create an archive  
  ```bash
  tar -cf archive.tar testfile  
  ```
- List files inside the archive  
  ```bash
  tar -tvf archive.tar  
  ```

#### **4. Extract an Archive**
- Delete original file  
  ```bash
  rm -rf testfile  
  ```
- Extract from `tar` archive  
  ```bash
  tar -xf archive.tar  
  ls -l  
  ```

#### **5. Compress Files with Different Algorithms**
```bash
gzip file1  
bzip2 file2  
xz file3  
```

#### **6. Compare File Sizes**
```bash
ls -lk  
```

#### **7. Decompress Files**
```bash
gzip -d file1.gz  
bzip2 -d file2.bz2  
xz -d file3.xz  
ls -lk  
```

---

## **Quick Reference Commands**  

| Command | Description |
|---------|-------------|
| `lsblk` | List block devices |
| `fdisk -l /dev/xvdb` | Show partition table |
| `fdisk /dev/xvdb` | Modify partitions |
| `partprobe` | Reload partition table |
| `mkfs.ext4 /dev/xvdb1` | Format as ext4 |
| `mkdir /mnt/ext4` | Create mount directory |
| `mount /dev/xvdb1 /mnt/ext4` | Mount partition |
| `df -h` | Check disk usage |
| `tar -cf archive.tar file` | Create archive |
| `tar -xf archive.tar` | Extract archive |
| `gzip file` | Compress file |
| `gzip -d file.gz` | Decompress file |
| `bzip2 file` | Compress file |
| `bzip2 -d file.bz2` | Decompress file |
| `xz file` | Compress file |
| `xz -d file.xz` | Decompress file |

---
