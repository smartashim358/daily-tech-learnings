#  PowerShell Foundations 

Author: Ashim Nepali\
Level: Foundation Phase\
Focus: Disk • Memory • Files • Directories • Processes • Network • Users

------------------------------------------------------------------------

# 1️⃣ Understanding PowerShell

PowerShell is an object-oriented command-line shell built on .NET.
Unlike CMD, it works with structured objects instead of plain text.

Key Concept: - Command = Cmdlet - Format: Verb-Noun (Example:
Get-Process)

------------------------------------------------------------------------

# 2️⃣ File System & Directory Control

## Check Current Location

``` powershell
Get-Location
```

## List Files & Folders

``` powershell
Get-ChildItem
Get-ChildItem -Force
Get-ChildItem -Recurse
```

## Create Directory

``` powershell
New-Item -ItemType Directory -Name WarriorLab
```

## Create File

``` powershell
New-Item -ItemType File -Name test.txt
```

## Delete File/Folder

``` powershell
Remove-Item test.txt
Remove-Item WarriorLab -Recurse
```

## Copy & Move

``` powershell
Copy-Item file.txt C:\Destination
Move-Item file.txt C:\Destination
```

Concept: - Files are stored in hierarchical structure. - -Recurse
removes or lists subdirectories. - -Force reveals hidden/system files.

------------------------------------------------------------------------

# 3️⃣ Disk & Storage Management

## View Drives

``` powershell
Get-PSDrive -PSProvider FileSystem
```

## Disk Space Overview

``` powershell
Get-Volume | Select DriveLetter, SizeRemaining, Size
```

## Folder Size Measurement

``` powershell
Get-ChildItem C:\Path -Recurse | Measure-Object -Property Length -Sum
```

## Pagefile Information

``` powershell
Get-CimInstance Win32_PageFileUsage
```

Concept: - Pagefile (pagefile.sys) = Virtual memory backup for RAM. -
Windows combines RAM + Pagefile = Virtual Memory System.

------------------------------------------------------------------------

# 4️⃣ Memory Management Concepts

Key Columns from Get-Process:

-   WS (Working Set) → Physical RAM currently used
-   PM → Paged memory allocated
-   NPM → Non-paged kernel memory
-   Handles → System object references

## Top Memory Processes

``` powershell
Get-Process | Sort-Object WS -Descending | Select -First 5 Name, WS, PM
```

## System Memory Overview

``` powershell
Get-CimInstance Win32_OperatingSystem | Select TotalVisibleMemorySize, FreePhysicalMemory
```

Concept: - Windows manages paging automatically. - Users cannot manually
swap specific processes. - Kernel controls memory balancing.

------------------------------------------------------------------------

# 5️⃣ Process Management

## List Processes

``` powershell
Get-Process
```

## Kill Process by Name

``` powershell
Stop-Process -Name notepad
```

## Kill by PID

``` powershell
Stop-Process -Id 1234
```

## Restart Explorer Safely

``` powershell
Get-Process explorer | Stop-Process -Force; Start-Process explorer
```

Concept: - PID (Process ID) uniquely identifies a process. - Force
killing may cause data loss. - Critical system processes should not be
terminated.

------------------------------------------------------------------------

# 6️⃣ Services Control

## List Services

``` powershell
Get-Service
```

## Stop/Start Service

``` powershell
Stop-Service -Name wuauserv
Start-Service -Name wuauserv
```

## Change Startup Type

``` powershell
Set-Service -Name wuauserv -StartupType Automatic
```

Concept: - Services run in background. - Not all services are safe to
disable.

------------------------------------------------------------------------

# 7️⃣ Networking Fundamentals

## Check IP Address

``` powershell
Get-NetIPAddress
```

## Ping Test

``` powershell
Test-Connection google.com
```

## Check Open Ports

``` powershell
netstat -ano
```

## Test Specific Port

``` powershell
Test-NetConnection -ComputerName 192.168.1.1 -Port 80
```

Concept: - IP Address identifies device on network. - Ports represent
services. - netstat shows active connections and PIDs.

------------------------------------------------------------------------

# 8️⃣ Users & Privileges

## List Local Users

``` powershell
Get-LocalUser
```

## List Administrators Group

``` powershell
Get-LocalGroupMember -Group Administrators
```

## Change Password (Admin Required)

``` powershell
Set-LocalUser -Name Username -Password (Read-Host -AsSecureString)
```

Concept: - Windows uses role-based privilege system. - Administrator
access required for system-level changes.

------------------------------------------------------------------------

#  Core Principles Learned

1.  Windows memory is kernel-managed.
2.  Processes are identified by PID.
3.  File system follows hierarchical structure.
4.  Disk + RAM combine into virtual memory.
5.  PowerShell uses object-based pipeline.
6.  Networking uses IP + Port architecture.
7.  Services and users require privilege control.

------------------------------------------------------------------------

#  Foundation Status

You now understand:

✔ File system control\
✔ Disk monitoring\
✔ Memory concepts\
✔ Process management\
✔ Service handling\
✔ Networking basics\
✔ User privilege system

Next Phase: Automation & Controlled Lab Emulation.

------------------------------------------------------------------------

End of Revision Document
