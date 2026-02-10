# Linux Commands Cheat Sheet for Cybersecurity

Author: Ashim Nepali  
Purpose: Master Linux commands for cybersecurity, server management, and penetration testing.

---

## 1. File & Directory Commands

### `ls`
**Definition:** Lists files and directories.  
**Explanation:** Show files, permissions, hidden files, sizes, etc.  
**Example:**
```bash
ls -la
```

### `cd`
**Definition:** Change directory.  
**Explanation:** Navigate between folders.  
**Example:**
```bash
cd /home/kali/Documents
```

### `pwd`
**Definition:** Print working directory.  
**Explanation:** Shows current directory path.  
**Example:**
```bash
pwd
# Output: /home/kali/Documents
```

### `mkdir`
**Definition:** Make a new directory.  
**Explanation:** Create folders for organization.  
**Example:**
```bash
mkdir lab
```

### `rm -r`
**Definition:** Remove a directory and its contents.  
**Explanation:** Deletes folder recursively.  
**Example:**
```bash
rm -r GhostTrack
```

---

## 2. File Viewing Commands

### `cat`
**Definition:** Concatenate and display file contents.  
**Example:**
```bash
cat file1.txt
```

### `less`
**Definition:** Scroll through long files.  
**Example:**
```bash
less /var/log/syslog
```

### `tail -f`
**Definition:** Follow live updates to a file.  
**Example:**
```bash
tail -f /var/log/auth.log
```

---

## 3. Searching & Filtering

### `grep`
**Definition:** Search text inside files.  
**Example:**
```bash
grep "error" /var/log/syslog
```

### `find`
**Definition:** Search for files/directories based on criteria.  
**Example:**
```bash
find . -type f
find / -perm -4000 2>/dev/null  # Find all SUID files
```

### `awk`, `sed`, `cut`
**Definition:** Text processing tools for extracting and modifying data.  
**Example:**
```bash
awk '{print $1}' file.txt
sed 's/old/new/g' file.txt
cut -d':' -f1 /etc/passwd
```

---

## 4. User & Permission Management

### `whoami` / `id` / `groups`
**Definition:** Show current user info.  
**Example:**
```bash
whoami
id
groups
```

### `chmod`
**Definition:** Change file permissions.  
**Example:**
```bash
chmod 755 script.sh
```

### `chown`
**Definition:** Change file owner.  
**Example:**
```bash
chown kali:kali file.txt
```

### `sudo` / `su`
**Definition:** Run commands as root / switch user.  
**Example:**
```bash
sudo apt update
su -
```

---

## 5. Networking

### `ip a`
**Definition:** Show network interfaces and IP addresses.  
**Example:**
```bash
ip a
```

### `ping`
**Definition:** Test connectivity to another host.  
**Example:**
```bash
ping 192.168.1.20
```

### `ssh`
**Definition:** Secure shell connection to a remote Linux system.  
**Example:**
```bash
ssh kali@192.168.1.20
ssh root@192.168.1.20
```

### `nmcli` / `rfkill`
**Definition:** Control Wi-Fi interfaces.  
**Example:**
```bash
nmcli radio wifi off
nmcli radio wifi on
rfkill block wifi
rfkill unblock wifi
```

---

## 6. Process & System Control

### `ps aux`
**Definition:** Show running processes.  
**Example:**
```bash
ps aux | grep ssh
```

### `top` / `htop`
**Definition:** Interactive process monitoring.  
**Example:**
```bash
top
```

### `kill` / `kill -9`
**Definition:** Terminate processes by PID.  
**Example:**
```bash
kill 1234
kill -9 1234
```

---

## 7. System Power & Services

### `shutdown` / `reboot`
**Definition:** Shutdown or restart the system.  
**Example:**
```bash
shutdown -h now   # halt
shutdown -r now   # restart
reboot
```

### `systemctl`
**Definition:** Manage services on Linux.  
**Example:**
```bash
systemctl status ssh
systemctl restart nginx
systemctl stop apache2
```

---

## 8. Archiving & File Transfer

### `tar`
**Definition:** Archive or extract files.  
**Example:**
```bash
tar -czvf backup.tar.gz /home/kali/Documents
tar -xzvf backup.tar.gz
```

### `scp`
**Definition:** Securely copy files over SSH.  
**Example:**
```bash
scp file.txt kali@192.168.1.20:/home/kali/
```

### `wget` / `curl`
**Definition:** Download files from internet.  
**Example:**
```bash
wget http://example.com/file.zip
curl -O http://example.com/file.zip
```

---

## 9. Cybersecurity-Focused Commands

### `find / -perm -4000 2>/dev/null`
**Definition:** Find all SUID files (privilege escalation check).  
**Explanation:** Searches entire system for files with SUID permissions, ignoring errors.  
**Example:**
```bash
find / -perm -4000 2>/dev/null
```

### `tail -f /var/log/auth.log`
**Definition:** Monitor authentication logs in real-time.  
**Example:** Detect login attempts or sudo usage.
```bash
tail -f /var/log/auth.log
```

---

# ⚡ Cheat Sheet Tips

- Always **check IP with `ip a`**, not loopback  
- Use `rm -ri` for safe deletes  
- SSH keys > password for secure remote login  
- `ip a` > `ifconfig` for modern systems  
- `tail -f` is your **live log monitoring superpower**  

---

**End of File**

