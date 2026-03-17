#  Linux User Management Guide

**Last Updated:** 14 Feb, 2026  

---

##  Overview
User management is a core function of Linux system administration. It controls system access, enforces security, and ensures users have appropriate privileges.

###  Importance
- Secures system from unauthorized access
- Ensures role-based access control
- Helps in auditing and tracking user activity

---

##  Understanding User IDs (UIDs)
- Linux supports up to ~60,000 users
- Each user has a unique UID
- UID identifies users internally

---

##  Types of Users

| User Type | Description |
|----------|------------|
| Root (Superuser) | Full control over system |
| Regular User | Limited access |
| Sudo User | Temporary admin privileges |
| System/Service Account | Used by services (mysql, nginx) |
| Guest User | Temporary, minimal access |

---

##  User Groups
Groups simplify permission management.

### 🔹 Primary Group
- Default group assigned to user
- Files created inherit this group
- Usually same as username

**Check Primary Group:**
```bash
id raj
```

---

### 🔹 Secondary Groups
- Provide additional permissions
- Used for team/system access

**Add user to group:**
```bash
sudo usermod -aG developers raj
```

**Check groups:**
```bash
groups raj
```

---

##  Important User Management Files

### 🔹 User Information
- `/etc/passwd` → User details (UID, GID, home, shell)
- `/etc/shadow` → Encrypted passwords

### 🔹 Group Management
- `/etc/group` → Group details
- `/etc/gshadow` → Secure group info

### 🔹 Privilege Control
- `/etc/sudoers` → Sudo permissions

### 🔹 Default User Setup
- `/etc/skel/` → Default configs (.bashrc, .profile)

### 🔹 Logs & Auditing
- `/var/log/auth.log` (Debian-based)
- `/var/log/secure` (RHEL-based)
- `journalctl` (systemd logs)

---

##  User Management Commands

### 🔹 List All Users
```bash
awk -F':' '{print $1}' /etc/passwd
```

### 🔹 Get User Info
```bash
id username
```

### 🔹 Add User
```bash
sudo useradd username
```

### 🔹 Set Password
```bash
sudo passwd username
```

### 🔹 View User File
```bash
cat /etc/passwd
```

---

##  Modify User Accounts

### 🔹 Change UID
```bash
sudo usermod -u 1982 username
```

### 🔹 Change GID
```bash
sudo usermod -g 1005 username
```

### 🔹 Change Username
```bash
sudo usermod -l new_name old_name
```

### 🔹 Change Home Directory
```bash
sudo usermod -d /new/home username
```

### 🔹 Delete User
```bash
sudo userdel -r username
```

---

##  Common Issues & Solutions

### 🔹 Forgotten Password
```bash
sudo passwd username
```

### 🔹 Account Lockout
```bash
sudo usermod -U username
```

### 🔹 Security Updates
```bash
sudo apt update && sudo apt upgrade
```

### 🔹 Permission Errors
```bash
sudo chmod 755 /path
sudo chown user:group /path
```

### 🔹 Group Membership Issues
```bash
sudo usermod -aG group username
```

### 🔹 Privilege Escalation Risk
```bash
sudo visudo
```

### 🔹 Editing Critical Files Safely
```bash
sudo vipw
sudo vigr
```

---

##  Best Practices
- Always use `sudo` carefully
- Avoid direct editing of system files
- Follow least privilege principle
- Regularly audit user accounts
- Keep system updated

---

##  Summary
Linux user management ensures secure, efficient, and organized system usage. Mastering users, groups, permissions, and system files is essential for system administration and cybersecurity.

---



