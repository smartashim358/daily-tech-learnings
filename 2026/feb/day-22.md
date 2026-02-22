#  PowerShell & Windows File System –  Notes (2026-02-22)

Author: Ashim Nepali  
Level: Foundation Phase  
Focus: Files, Directories, Disk Clustering, Permissions, NTFS ACL

---

# 1️. Files

## Definition
- A **file** is a named container that stores data.
- Examples: `.txt`, `.exe`, `.jpg`

## Components
- **Data**: Actual content
- **Metadata**: File name, size, timestamps, owner, permissions, location

## Disk Storage
- Stored in **sectors** (smallest physical unit) on HDD/SSD
- Managed via **clusters** (group of sectors, e.g., 4KB default)
- NTFS keeps file records in **MFT (Master File Table)**

## File Operations
- **Create**: Allocates cluster(s), sets metadata, inherits parent permissions
```powershell
New-Item test.txt
```
- **Open**: OS creates a handle, loads data into RAM, may lock file
- **Delete**: Removes MFT entry, marks disk space free; actual data remains until overwritten

## Cluster Example
- Cluster = 4KB
- File1 = 1KB → uses 1 cluster (3KB slack)
- File2 = 3KB → uses 1 cluster (1KB slack)
- File3 = 5KB → uses 2 clusters (8KB total, 3KB slack)
- **Rule**: Each cluster belongs to only 1 file

---

# 2️. Directories (Folders)

## Definition
- Container for files and/or other directories
- Stores names and pointers to file locations

## Operations
- Create folder:
```powershell
New-Item WarriorLab -ItemType Directory
```
- Delete folder recursively:
```powershell
Remove-Item WarriorLab -Recurse -Force
```
- List contents:
```powershell
Get-ChildItem -Force -Recurse
```

---

# 3️. Windows File Permissions (NTFS)

## Concepts
- Permissions define **who can do what** to a file/folder
- Managed via **ACL (Access Control List)** containing **ACE (Access Control Entries)**
- Users can belong to **groups**, inheriting permissions

## Basic Permissions
| Permission | Meaning |
|------------|--------|
| Read (R) | View file |
| Write (W) | Modify file |
| Execute (X) | Run program |
| Modify (M) | Read + Write + Delete |
| Full Control (F) | Everything |

## Priority
1. Explicit Deny
2. Explicit Allow
3. Inherited Deny
4. Inherited Allow
>  Deny always overrides Allow

## Inheritance
- Child files/folders inherit permissions from parent
- Shown as `(I)` in icacls
- Object Inherit `(OI)` → applies to files
- Container Inherit `(CI)` → applies to folders

## Ownership
- Owner can modify permissions
- Taking ownership is key when access is denied

---

# 4️. Commands for Analysis & Modification

### Check Permissions
```powershell
icacls hacker
Get-Acl hacker
```

### Grant Permissions
```powershell
icacls hacker /grant DELL:F
```

### Deny Permissions
```powershell
icacls hacker /deny DELL:F
```

### Remove Permissions
```powershell
icacls hacker /remove DELL
```

### Take Ownership
```powershell
takeown /f hacker /r /d y
```

---

# 5️. Key Concepts Learned Today

- **File** = data + metadata, stored in clusters on disk
- **Cluster** = minimum allocation unit; cannot be shared between files
- **Slack space** = unused space inside cluster
- **Directory** = container for files/folders
- **NTFS Permissions** = ACL rules defining access
- **Effective Permissions** = calculated by OS from all groups and ACEs
- **Ownership** = gives control to modify ACL even when denied

---

# 6️. Practice/Revision Steps

1. Create files of different sizes and check disk usage vs cluster allocation
2. Open file in Notepad and try deleting folder → observe lock behavior
3. Use `icacls` to read and modify permissions
4. Take ownership of a folder and modify ACL
5. Analyze effective permissions when a user belongs to multiple groups


