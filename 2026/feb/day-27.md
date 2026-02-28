# Blue Team Investigation Model -- Deep Study Notes

Author: Ashim Nepali\
Topic: Process & System Investigation using PowerShell + WMI

------------------------------------------------------------------------

# Overview

Today we learned how to investigate a Windows system step-by-step using:

1.  Process inspection
2.  Parent process analysis
3.  Service verification
4.  Executable path validation
5.  Operating system state review

This document is clean, structured, and GitHub-ready.

------------------------------------------------------------------------

# 1. Inspect Process (Win32_Process)

Purpose: Determine if a process is normal or suspicious.

Command:

Get-CimInstance Win32_Process -Filter "Name='process.exe'" \|
Format-List \*

Key Properties:

-   Name
-   ProcessId
-   ParentProcessId
-   ExecutablePath
-   CommandLine
-   HandleCount
-   WorkingSetSize
-   KernelModeTime
-   UserModeTime

What to Check:

-   Unusual command line arguments
-   High memory usage without reason
-   Very high handle count
-   Missing executable path
-   Unknown process name

------------------------------------------------------------------------

# 2. Identify Parent Process

Purpose: Understand who launched the process.

Command:

$proc = Get-CimInstance Win32_Process -Filter "ProcessId=PID" Get-CimInstance Win32_Process -Filter "ProcessId=$(\$proc.ParentProcessId)"

Normal Examples:

explorer.exe → browser.exe\
services.exe → svchost.exe

Suspicious Examples:

winword.exe → powershell.exe\
explorer.exe → cmd.exe → unknown.exe

Parent-child relationships help detect malicious spawning behavior.

------------------------------------------------------------------------

# 3. Check Related Service (Win32_Service)

Purpose: Detect persistence or auto-start behavior.

Command:

Get-CimInstance Win32_Service \| Where-Object {\$\_.ProcessId -eq PID}

Key Properties:

-   Name
-   State
-   StartMode
-   PathName
-   StartName

Red Flags:

-   StartMode = Auto
-   Executable in AppData or Temp
-   Running as LocalSystem
-   Unknown vendor

Services are commonly abused for persistence.

------------------------------------------------------------------------

# 4. Verify Executable Path

Purpose: Confirm the file is legitimate.

Example:

C:`\Windows`{=tex}`\System32`{=tex}`\svchost`{=tex}.exe (Normal)\
C:`\Users`{=tex}`\Public`{=tex}`\svchost`{=tex}.exe (Suspicious)

Command:

Get-Item "C:`\Path`{=tex}`\file`{=tex}.exe" \| Format-List \*

Check:

-   CreationTime
-   LastWriteTime
-   File size
-   File location

Process name can be fake. Path is critical.

------------------------------------------------------------------------

# 5. Analyze OS State (Win32_OperatingSystem)

Purpose: Understand overall system condition.

Command:

Get-CimInstance Win32_OperatingSystem

Important Properties:

-   Caption
-   Version
-   BuildNumber
-   OSArchitecture
-   FreePhysicalMemory
-   LastBootUpTime

Why It Matters:

-   Detect long uptime
-   Identify outdated systems
-   Check memory pressure
-   Correlate suspicious activity with reboot time

------------------------------------------------------------------------

# Investigation Flow Model

Step 1 → Inspect Process\
Step 2 → Identify Parent\
Step 3 → Check Service\
Step 4 → Verify Path\
Step 5 → Analyze OS State

This layered approach builds a full system understanding.

------------------------------------------------------------------------

# Final Understanding

PowerShell + WMI provide structured visibility into:

-   Running processes
-   Services
-   System state
-   Persistence mechanisms

Mastering these steps builds strong Blue Team investigation skills.

------------------------------------------------------------------------

End of Notes
