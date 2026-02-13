# 🛡️ Linux File Permissions -- Complete Mastery Guide

Author: Ashim Nepali\
Level: Beginner → Advanced (Cybersecurity Focus)

------------------------------------------------------------------------

## 1. Introduction to Linux File Permissions

Linux is a multi-user operating system designed with strong security
boundaries.\
Every file and directory has an owner and a defined permission
structure.\
These permissions determine who can read, modify, or execute a file.\
Understanding this system is foundational for system administration and
cybersecurity.

------------------------------------------------------------------------

## 2. Viewing File Permissions

### Command:

``` bash
ls -l
```

### Explanation:

The `ls -l` command lists files in long format, displaying permission
bits, ownership, size, and timestamps.\
The first column represents file type and permission structure.\
It allows developers and security professionals to quickly audit access
control settings.\
This is the first step in diagnosing permission-related errors.

------------------------------------------------------------------------

## 3. Permission Structure Breakdown

Example Output:

    -rwxr-xr--

### Explanation:

The first character defines the file type (`-` for file, `d` for
directory).\
The next three characters represent owner permissions.\
The following three represent group permissions.\
The final three define access for others (everyone else on the system).

------------------------------------------------------------------------

## 4. Permission Values (Numeric System)

  Symbol   Value
  -------- -------
  r        4
  w        2
  x        1

### Explanation:

Linux uses binary-based arithmetic to define permissions numerically.\
Each permission group is calculated by adding values of r, w, and x.\
For example, `rwx` equals 7 (4+2+1).\
This numeric model simplifies bulk permission configuration in scripting
and automation.

------------------------------------------------------------------------

## 5. Changing Permissions

### Command:

``` bash
chmod 755 filename
```

### Explanation:

The `chmod` command modifies file permission bits.\
In `755`, the owner receives full control (7), while group and others
receive read and execute access (5).\
This configuration is commonly used for executable scripts and web
files.\
Improper usage may introduce security vulnerabilities.

------------------------------------------------------------------------

## 6. Symbolic Mode Permission Changes

### Command:

``` bash
chmod u+x filename
```

### Explanation:

Symbolic mode allows granular modification without recalculating numeric
values.\
`u+x` adds execute permission to the file owner only.\
This is useful when adjusting specific access bits incrementally.\
It prevents accidental overwriting of existing permissions.

------------------------------------------------------------------------

## 7. Ownership Management

### Change Owner:

``` bash
sudo chown user:group filename
```

### Explanation:

The `chown` command changes file ownership.\
This is necessary when files are created under root privileges but need
normal user control.\
Ownership misconfiguration is a common cause of permission errors.\
In secure environments, ownership must align with least-privilege
principles.

------------------------------------------------------------------------

## 8. Directory Permission Behavior

Directory permissions function differently from file permissions.

  Permission   Meaning in Directory
  ------------ ----------------------
  r            List files
  w            Create/Delete files
  x            Enter directory

### Explanation:

Without execute permission on a directory, users cannot access its
contents---even if they can read it.\
Write permission allows file creation and deletion inside the
directory.\
Execute permission enables traversal.\
This distinction is critical when securing application folders.

------------------------------------------------------------------------

## 9. Special Permissions

### SUID (Set User ID)

``` bash
chmod 4755 filename
```

This allows a file to execute with the owner's privileges.\
Often used for system utilities requiring elevated rights.\
Improper SUID configuration can lead to privilege escalation.\
Security professionals frequently audit SUID binaries.

------------------------------------------------------------------------

### Sticky Bit

``` bash
chmod 1777 directory
```

Commonly used in shared directories like `/tmp`.\
Users can create files, but only the file owner can delete them.\
This prevents users from removing other users' files.\
It enhances multi-user system stability.

------------------------------------------------------------------------

## 10. Security Auditing Commands

### Find World-Writable Files

``` bash
find / -type f -perm -0002 2>/dev/null
```

### Find SUID Files

``` bash
find / -perm -4000 2>/dev/null
```

### Explanation:

These commands help identify potential security risks.\
World-writable files can be modified by any user, increasing attack
surface.\
SUID files may allow privilege escalation if vulnerable.\
Routine auditing is a key practice in defensive security.

------------------------------------------------------------------------

# Conclusion

Mastering Linux file permissions is essential for developers, system
administrators, and cybersecurity professionals.\
It enforces access control, protects sensitive data, and prevents
unauthorized actions.\
A strong understanding of ownership, permission bits, and special modes
reduces misconfiguration risks.\
True Linux expertise begins with mastering permissions at a deep level.

------------------------------------------------------------------------

End of Document.
