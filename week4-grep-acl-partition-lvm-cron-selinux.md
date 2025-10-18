# 🐧 Week 4: Advanced Linux Administration — grep, ACL, Partitioning, LVM, Job Scheduling & SELinux  

Welcome to **Week 4** of my 6-week Linux learning journey!  
This week I explored some core Linux system administration topics that form the foundation of server and DevOps management.  

---

## 🔍 grep — Searching Made Easy  

- `grep root /etc/passwd` → search for the word *root*  
- `grep -c root /etc/passwd` → count matching lines  
- `grep -o root /etc/passwd` → show only matched parts  
- `grep ^root /etc/passwd` → match *root* at the beginning of line  
- `grep bash$ /etc/passwd` → match *bash* at end of line  
- `grep -v bash /etc/passwd` → exclude lines with *bash*  
- `grep -n root /etc/passwd` → show line numbers  
- `grep -i devops /etc/passwd` → case-insensitive search  
- `grep -w dev /etc/passwd` → match only whole word  

---

## 🔐 ACL (Access Control List)

ACL allows giving **fine-grained permissions** beyond traditional user/group/other.  

- `setfacl -m u:meeta:rwx /test` → give special rights to user  
- `getfacl /test` → view ACLs  
- `setfacl -m d:u:meeta:rwx /test` → default ACL inheritance  
- `setfacl -m g:sales:--- /test` → set ACL for a group  
- `setfacl -x u:student /test` → remove user ACL  
- `setfacl -k /test` → remove default ACL  
- `setfacl -b /test` → remove all ACLs  

---

## 💾 Partition Management  

- `fdisk -l` → list partitions  
### MBR (Master Boot Record)
- Older scheme, supports **4 primary partitions** (or 3 primary + 1 extended)  
- MBR is **512 bytes** — 446 bytes boot code, 64 bytes partition table, 2 bytes signature.  

### GPT (GUID Partition Table)
- Modern scheme, supports many partitions.  
- Uses a special **EFI partition** for booting OS.  

### Example: Create a 600MB Partition and Mount Persistently  
```bash
fdisk /dev/vdb
n
+600M
partprobe
mkfs -t ext4 /dev/vdb1
mkdir /data
mount /dev/vdb1 /data
vim /etc/fstab
/dev/vdb1 /data ext4 defaults 0 0
mount -a
systemctl daemon-reload

📦 LVM (Logical Volume Management)

Why LVM? - It provides resizing capability, snapshots, and flexible storage management.

Steps:
lsblk
fdisk /dev/vdb
n +700M
t 8e
w
partprobe
pvcreate /dev/vdb2
vgcreate vg0 /dev/vdb2
lvcreate -L 100M -n lv0 vg0
mkfs -t ext4 /dev/vg0/lv0
mkdir /database
vim /etc/fstab
/dev/vg0/lv0 /database ext4 defaults 0 0
mount -a
systemctl daemon-reload

Resize LVM
lvextend -L 300M /dev/vg0/lv0
resize2fs /dev/vg0/lv0

Snapshot
lvcreate -s /dev/vg0/lv0 -L 10M -n lvsnap

Create Swap Partition (512M)
fdisk /dev/vdb
n +512M
t swap
w
partprobe
mkswap /dev/vdb3
vim /etc/fstab
/dev/vdb3 swap swap defaults 0 0
mount -a
swapon -a
free -m

🕒 Scheduling Tasks (cron)
Cron fields:
* * * * *
→ minute, hour, day of month, month, day of week

Example:
Backup /root every Sunday of Jan & Mar at 11 PM

crontab -e
0 23 * 1,3 sun tar -cvzf /tmp/root.tar.gz /root
crontab -l

🔒 SELinux (Security-Enhanced Linux)
SELinux enforces strict access control via MAC (Mandatory Access Control).

Goals:- Protect user data from services like httpd, sshd, crond.

Policy Types:
Targeted → confines key services
Strict → confines everything
MLS → multi-level (gov/military-grade)

Modes:
Enforcing → blocks and logs
Permissive → logs only (debug)
Disabled → turns SELinux off

Commands:
sestatus
setenforce 0   # permissive
setenforce 1   # enforcing
getenforce
ls -ldZ /etc
ls -Z file.txt
ps -eZ | grep sshd
vim /etc/selinux/config

⚙️ Challenges I Faced
Remembering grep options for complex searches
Understanding difference between MBR and GPT layouts
Troubleshooting mounting errors in /etc/fstab
Configuring SELinux modes correctly for troubleshooting

💡 Resources
Red Hat — Understanding ACLs
Linux Handbook — LVM Explained
Cron Job Basics (TutorialsPoint)
Red Hat — SELinux Guide
Linux Handbook — LVM Explained

TutorialsPoint — Cron Job Basics

Red Hat — SELinux Guide

Red Hat — SELinux Guide
