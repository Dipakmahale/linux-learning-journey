# 🧩 Week 3: User Management, Permissions, Processes & More  

This week, I explored some of the most powerful Linux administration concepts that are core to every DevOps engineer’s toolkit.  

---

## 👥 User Management  

- `useradd kavita` → Add a new user  
- `groupadd sales` → Create a new group  
- `usermod -G sales kavita` → Add user *kavita* to secondary group *sales*  
- `/etc/group` → Contains group information  
- `passwd kavita` → Set password for user *kavita*  
- `/etc/passwd` → Stores user account details  
- `/etc/shadow` → Stores encrypted passwords  
  - `$6` → SHA-512  
  - `$5` → SHA-256  
  - `$1` → MD5  

**Account Management:**  
- `usermod -L kavita` → Lock user password  
- `usermod -U kavita` → Unlock user password  
- `usermod -s /sbin/nologin kavita` → Assign non-interactive shell  
- `usermod -s /bin/bash kavita` → Assign interactive shell  
- `vim /etc/sudoers` → Grants sudo privileges to users  
- `/etc/login.defs` → Contains user password policy  
- `sudo deepak` → Execute command as root user  

**User ID Ranges:**  
- Root user → UID 0  
- System users → UID 1–999  
- Regular users → UID 1000+  

---

## 🔐 Permissions & Ownership  

- `ls -ld` → View directory permissions  
- Permission values:  
  - `r=4`, `w=2`, `x=1`  
- Default permissions:  
  - Directories → `755`  
  - Files → `644`  
- Default `umask = 0022`  
  - To permanently change, edit `.bashrc` and add `umask 0022`  

**Examples:**  
- `chmod 777 /test` → Full permission  
- `chmod ugo=rwx /test` → Full permission using symbolic mode  

**Permission usage:**  
- `cd` → needs *x* (execute) permission  
- `ls -l` → needs *r* (read) permission  
- *w* → allows editing or writing files  

**Special Permissions:**  
- Sticky Bit (`chmod o+t /dir`) → Prevents users from deleting others’ files in shared directories (e.g., `/tmp`)  
- SGID (`chmod g+s /dir`) → New files inherit group ownership from the directory  
- SUID (`chmod u+s /usr/bin/passwd`) → Run executables with owner’s permissions (commonly used in binaries like `passwd`)  

---

## ⚙️ Process Management  

- Process = a running program, identified by PID  
- Parent process: `systemd`  
- `top` → Dynamic view of processes  
- `ps` → Static snapshot of active processes  
- `kill -l` → List all signals  
  - `-9` (SIGKILL): Force kill  
  - `-15` (SIGTERM): Graceful termination  
  - `-19` (SIGSTOP): Suspend process  
  - `-18` (SIGCONT): Resume process  

**Process States:**  
- `R` → Running or ready  
- `S` → Sleeping (interruptible)  
- `D` → Uninterruptible sleep  
- `Z` → Zombie (terminated but not cleaned)  
- `X` → Exited  

**Commands:**  
- `ps -aux` → List all active processes  
- `nice` → Set process priority (-20 = highest, 19 = lowest)  
- Foreground process → Uses the terminal directly  
- Background process → `command &`  
- `Ctrl+Z` → Suspend process  
- `jobs` → View background jobs  
- `Ctrl+C` → Kill foreground process  

---

## 🧾 Log Management  

- Logs = recorded system or application events  
- Services involved:  
  - `systemd-journald` → Collects logs in `/run/log/journal` (binary format)  
  - `rsyslogd` → Aggregates and stores logs in `/var/log` (plaintext)  
- `/etc/logrotate.conf` → Defines log rotation policy  
  - Default: Weekly rotation, 4 backups, compression enabled (`gzip`)  
  - Force rotation: `logrotate -f /etc/logrotate.conf`  

**Commands:**  
- `journalctl` → Read binary logs  
- `tail -f /var/log/messages` → View live log updates in text format  
- `logger "Hello"` → Create a manual log entry  

---

## 🔐 SSH (Secure Shell)  

- Enables secure remote access between client and server  
- Default port: **22**  
- Command: `ssh root@servera`  
- Verify SSH service:  
  - `yum list openssh-server`  
  - `systemctl status sshd`  
  - `netstat -tulnp | grep 22`  

**SSH Key-Based Authentication:**  
- Generate key pair: `ssh-keygen`  
- Copy key to remote: `ssh-copy-id -i ~/.ssh/id_rsa.pub user@server`  
- Enables passwordless login for future sessions  

---

## 📦 Package Management (YUM & RPM)  

**RPM (Red Hat Package Manager):**  
- Manual installation, no dependency resolution  
  - Install: `rpm -ivh httpd`  
  - Info: `rpm -qi httpd`  

**YUM (Yellowdog Updater Modified):**  
- Automatically resolves dependencies  
  - Install: `yum install httpd`  
  - Update: `yum update httpd`  
  - Remove: `yum remove httpd`  

---

## 💡 Reflection  

This week was a big leap into the real world of system administration.  
From managing users and permissions to understanding processes and logs — it all started to connect.  

Every command taught me how Linux systems stay secure, organized, and efficient.  
SSH and package management were especially exciting because they bring automation closer! 🚀  

---

## 🧰 Resources  
 
- [Linuxize — User and Group Management](https://linuxize.com/post/how-to-add-user-to-group-in-linux/)  
- [TutorialsPoint — Linux Processes](https://www.tutorialspoint.com/unix/unix-processes.htm)  
- [GeeksforGeeks — Log Management Basics](https://www.geeksforgeeks.org/techtips/how-to-manage-logs-in-linux/?utm_source=chatgpt.com)  
- [SSH Key Authentication](https://www.ssh.com/academy/ssh/keygen)  
- [YUM vs RPM Explained](https://phoenixnap.com/kb/rpm-vs-yum?utm_source=chatgpt.com) 
