# Windows Management Instrumentation (WMI) -- Deep Study Notes

Focus: Blue Team / System Internals Author: Ashim Nepali

------------------------------------------------------------------------

# 1. What is WMI?

Windows Management Instrumentation (WMI) is a Windows infrastructure
that allows structured querying of:

-   Processes
-   Services
-   Operating System
-   Hardware
-   Network
-   Security information

WMI is built on CIM (Common Information Model). It returns OBJECTS, not
plain text.

------------------------------------------------------------------------

# 2. WMI Architecture (Concept Flow)

PowerShell Command ↓ Get-CimInstance ↓ WMI Provider ↓ CIM Repository ↓
Windows Kernel / System Data

Meaning: PowerShell asks → WMI processes → System responds → Object
returned.

------------------------------------------------------------------------

# 3. Understanding WMI Objects

Example:

Get-CimInstance Win32_Process

This returns objects containing: - Properties - Methods - Metadata

Check structure:

Get-CimInstance Win32_Process \| Get-Member

------------------------------------------------------------------------

# 4. Win32_Process (Deep Study)

Represents every running process.

Important Properties: - Name - ProcessId - ParentProcessId -
ExecutablePath - HandleCount - WorkingSetSize - KernelModeTime -
UserModeTime

Example:

Get-CimInstance Win32_Process \| Select Name,ProcessId,WorkingSetSize

Blue Team Use: - Detect suspicious processes - Check abnormal memory
usage - Identify parent-child chains - Detect malware behavior

------------------------------------------------------------------------

# 5. Win32_Service (Deep Study)

Represents Windows services.

Important Properties: - Name - DisplayName - State (Running/Stopped) -
StartMode (Auto/Manual/Disabled) - PathName - StartName

Example:

Get-CimInstance Win32_Service \| Select Name,State,StartMode

Blue Team Use: - Detect persistence - Identify auto-start services -
Check unusual execution paths - Detect SYSTEM-level services

------------------------------------------------------------------------

# 6. Win32_OperatingSystem (Deep Study)

Represents OS-level information.

Important Properties: - Caption - Version - BuildNumber -
OSArchitecture - TotalVisibleMemorySize - FreePhysicalMemory -
LastBootUpTime

Example:

Get-CimInstance Win32_OperatingSystem \| Select
Caption,Version,LastBootUpTime

Blue Team Use: - Detect outdated systems - Monitor uptime - Monitor
memory state - Verify architecture

------------------------------------------------------------------------

# 7. Blue Team Investigation Flow

Step 1 → Inspect process (Win32_Process) Step 2 → Check parent process
Step 3 → Inspect related service (Win32_Service) Step 4 → Check OS state
(Win32_OperatingSystem) Step 5 → Validate path and startup configuration

------------------------------------------------------------------------

# 8. Core Commands Summary

List class details: Get-CimClass Win32_Process

Filter example: Get-CimInstance Win32_Service -Filter "State='Running'"

Full object view: Get-CimInstance Win32_Process \| Format-List \*

------------------------------------------------------------------------

# Final Understanding

WMI allows structured system interrogation.

If you master WMI: You understand Windows internal behavior.
