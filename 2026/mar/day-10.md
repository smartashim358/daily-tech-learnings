# Linux Permissions - Structured Notes

## 1. Introduction
Linux file permissions define access control for files and directories. They determine who can read, write, or execute files, ensuring system security.

---

## 2. Basic Permissions

| Symbol | Meaning | Description |
|--------|--------|------------|
| r | Read | View file contents or list directory |
| w | Write | Modify file or add/remove files in directory |
| x | Execute | Run file or enter directory |

---

## 3. Permission Groups

Permissions are divided into three categories:

| Group | Description |
|------|------------|
| User (u) | Owner of the file |
| Group (g) | Users in the same group |
| Others (o) | All other users |

Structure:
rwx  rwx  rwx
 u    g    o

---

## 4. Viewing File Permissions

### ls -l
Displays file details and permissions

Example:
-rw-r--r-- 1 user group 46 Apr 14 16:37 file.txt

Breakdown:
- First character: file type (- = file, d = directory)
- Next 9 characters: permissions
- Owner and group
- File size
- Last modified date

### stat
Shows detailed file information

Command:
stat file.txt

### namei
Shows permission along path

Command:
namei -l /path/to/file

---

## 5. chmod Command (Change Permissions)

### Symbolic Method

Format:
chmod [who][operator][permission] file

Operators:
+ : add permission  
- : remove permission  
= : set exact permission  

Examples:
chmod +x file.txt
chmod o+x file.txt
chmod ugo-rwx file.txt
chmod ug+rw,o-x file.txt

---

## 6. Octal Notation

| Permission | Value |
|-----------|------|
| Read (r) | 4 |
| Write (w) | 2 |
| Execute (x) | 1 |

Combine values:

| Octal | Meaning |
|------|--------|
| 7 | rwx |
| 6 | rw- |
| 5 | r-x |
| 4 | r-- |
| 0 | --- |

Example:
chmod 755 file.txt

Meaning:
- User: rwx (7)
- Group: r-x (5)
- Others: r-x (5)

---

## 7. Permission Example

rw- r-x r--

Explanation:
- User: read, write
- Group: read, execute
- Others: read only

---

## 8. Special Permissions

### setuid
Runs file with owner's privileges
chmod u+s file

### setgid
Files inherit group or run with group permissions
chmod g+s directory

### sticky bit
Only owner can delete files in directory
chmod +t directory

---

## 9. Ownership Management

### chown
Change file owner and group

Command:
chown user:group file.txt

---

## 10. Key Commands Summary

| Command | Purpose |
|--------|--------|
| ls -l | View permissions |
| chmod | Change permissions |
| chown | Change ownership |
| stat | Detailed file info |
| namei | Check path permissions |

---

## 11. Important Notes

- Avoid giving full permissions (777) unless necessary
- Be careful with "others" permissions for security
- Use groups to manage multiple users efficiently
- Prefer least privilege principle

---

## End of Notes
