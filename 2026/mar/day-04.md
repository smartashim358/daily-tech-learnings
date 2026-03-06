# Linux File System Structure (Deep Guide)

## 1. Introduction

Linux follows the **Filesystem Hierarchy Standard (FHS)**. All files and
directories start from the **root directory (`/`)**.

Unlike Windows where storage is divided into drives like `C:\` or `D:\`,
Linux organizes everything under one directory tree starting from `/`.

Example structure:

/ ├── bin ├── boot ├── dev ├── etc ├── home ├── lib ├── proc ├── root
├── tmp ├── usr └── var

Understanding this structure is important for: - Operating system
fundamentals - Cybersecurity - System administration - Malware
analysis - Digital forensics

------------------------------------------------------------------------

# 2. Root Directory (/)

The root directory is the **top level of the entire filesystem**.

Every directory exists under `/`.

Example:

``` bash
cd /
ls
```

Typical output:

    bin  boot  dev  etc  home  lib  proc  root  tmp  usr  var

------------------------------------------------------------------------

# 3. /bin (Essential User Binaries)

`/bin` contains **essential command line programs** used by all users.

Examples:

    /bin/ls
    /bin/cp
    /bin/mv
    /bin/bash
    /bin/cat

Example command:

``` bash
ls /bin
```

Purpose: - Core utilities required for system operation - Commands
available even during system recovery

Security relevance: Attackers sometimes replace binaries here to create
backdoors.

------------------------------------------------------------------------

# 4. /sbin (System Binaries)

Contains **administrative commands** mainly used by the root user.

Examples:

    /sbin/reboot
    /sbin/fsck
    /sbin/shutdown
    /sbin/iptables

Example:

``` bash
ls /sbin
```

Purpose: - System repair - Disk management - Boot operations

------------------------------------------------------------------------

# 5. /etc (Configuration Files)

Stores **system configuration files**.

Important files:

    /etc/passwd
    /etc/shadow
    /etc/hosts
    /etc/hostname
    /etc/fstab
    /etc/ssh/sshd_config

Example:

``` bash
cat /etc/passwd
```

Example output:

    root:x:0:0:root:/root:/bin/bash

Cybersecurity importance: - User accounts - Password storage - Service
configuration

------------------------------------------------------------------------

# 6. /home (User Directories)

Contains personal directories for normal users.

Example:

    /home/alice
    /home/bob
    /home/john

Example command:

``` bash
ls /home
```

Typical user files:

    Documents
    Downloads
    Desktop
    Projects

------------------------------------------------------------------------

# 7. /root (Root User Home)

Home directory of the **root administrator**.

Example:

    /root

Difference:

    /home/user  → normal user
    /root       → administrator

Only root can access it.

------------------------------------------------------------------------

# 8. /boot (Boot Files)

Contains files required to start the system.

Examples:

    /boot/vmlinuz
    /boot/initrd
    /boot/grub

Bootloader configuration:

    /boot/grub/grub.cfg

Example:

``` bash
ls /boot
```

------------------------------------------------------------------------

# 9. /dev (Device Files)

Linux treats **hardware devices as files**.

Examples:

    /dev/sda
    /dev/sda1
    /dev/null
    /dev/random
    /dev/tty

Example:

``` bash
ls /dev
```

Important device files:

    /dev/null   → discards output
    /dev/random → random number generator
    /dev/sda    → disk device

------------------------------------------------------------------------

# 10. /proc (Process Information)

`/proc` is a **virtual filesystem created by the kernel**.

It contains runtime system information.

Examples:

    /proc/cpuinfo
    /proc/meminfo
    /proc/uptime

Example command:

``` bash
cat /proc/cpuinfo
```

Process directories:

    /proc/1
    /proc/234
    /proc/1024

Example:

``` bash
ls /proc/$$
```

Security use: - Process investigation - Malware detection - Memory
analysis

------------------------------------------------------------------------

# 11. /tmp (Temporary Files)

Stores temporary files created by programs.

Examples:

    /tmp/file1
    /tmp/install_temp

Example:

``` bash
ls /tmp
```

Files here may be deleted after reboot.

Security risk: Attackers sometimes hide malicious scripts here.

------------------------------------------------------------------------

# 12. /usr (User Programs)

Contains most installed applications and libraries.

Structure:

    /usr/bin
    /usr/lib
    /usr/share
    /usr/local

Examples:

    /usr/bin/python
    /usr/bin/git
    /usr/bin/firefox

Example:

``` bash
ls /usr/bin
```

------------------------------------------------------------------------

# 13. /var (Variable Data)

Stores data that changes frequently.

Examples:

    /var/log
    /var/cache
    /var/spool
    /var/tmp

Important logs:

    /var/log/auth.log
    /var/log/syslog

Example:

``` bash
ls /var/log
```

Cybersecurity importance: Logs are critical for **incident investigation
and monitoring**.

------------------------------------------------------------------------

# 14. /lib (Shared Libraries)

Contains shared libraries used by programs.

Similar to **DLL files in Windows**.

Examples:

    /lib/libc.so
    /lib/libm.so

Example:

``` bash
ls /lib
```

Programs in `/bin` and `/sbin` rely on these libraries.

------------------------------------------------------------------------

# 15. /opt (Optional Software)

Used for installing **third‑party software packages**.

Example:

    /opt/google
    /opt/discord

------------------------------------------------------------------------

# 16. /mnt (Temporary Mount Point)

Used for manually mounting filesystems.

Example:

``` bash
mount /dev/sdb1 /mnt
```

Example structure:

    /mnt/usb
    /mnt/disk

------------------------------------------------------------------------

# 17. /media (Removable Devices)

Automatically used for removable storage.

Examples:

    /media/usb
    /media/cdrom
    /media/external_drive

------------------------------------------------------------------------

# 18. Summary Table

  Directory   Purpose
  ----------- ----------------------
  /           Root directory
  /bin        Essential commands
  /sbin       System commands
  /etc        Configuration files
  /home       User directories
  /root       Root home
  /boot       Bootloader & kernel
  /dev        Device files
  /proc       Process information
  /tmp        Temporary files
  /usr        User programs
  /var        Logs & variable data
  /lib        Shared libraries
  /opt        Optional software
  /mnt        Manual mount point
  /media      Removable devices

------------------------------------------------------------------------

# 19. Why Cybersecurity Students Must Know This

Understanding the Linux filesystem helps with:

-   Malware analysis
-   Digital forensics
-   Privilege escalation investigation
-   Log analysis
-   Rootkit detection

Example investigations:

Check running processes:

``` bash
ls /proc
```

Check authentication logs:

``` bash
cat /var/log/auth.log
```

Check system users:

``` bash
cat /etc/passwd
```

------------------------------------------------------------------------

# 20. Key Concept

Linux follows a design principle:

**Everything is treated as a file.**

That includes: - Devices - Processes - Configuration - Hardware
interfaces

This design provides powerful transparency and control for system
administrators and cybersecurity professionals.
