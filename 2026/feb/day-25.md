# Blue Team Day 2 -- Service Investigation & Process Analysis (Windows)

## 1. Understanding Process Metrics

When investigating a process, we analyzed:

-   **WS (Working Set)** → Actual RAM currently used by the process
-   **PM (Private Memory)** → Memory used only by that process
-   **NPM (Non-Paged Memory)** → Kernel memory that cannot be swapped to
    disk
-   **Handles** → References to system resources (files, registry,
    threads)
-   **CPU(s)** → Total CPU time (in seconds) used since process start

### Normal Ranges (8GB RAM System)

-   Browser WS: 200--800 MB\
-   Explorer WS: 100--250 MB\
-   Handles (normal app): 100--2000\
-   Antivirus Handles: 2000--4000\
-   Idle CPU: 1%--10%

Key Lesson:\
Do not judge by number alone. Always compare with: - Process name -
Process path - Behavior trend (increasing or stable)

------------------------------------------------------------------------

## 2. Service Investigation Using PowerShell

### Core Command

``` powershell
Get-CimInstance Win32_Service |
Where-Object {$_.Name -eq "rsEngineSvc"} |
Select Name,State,StartMode,PathName
```

### Command Breakdown

#### Get-CimInstance Win32_Service

-   Queries Windows Management Instrumentation (WMI)
-   Retrieves all Windows service objects

#### Pipe (\|)

-   Sends output of one command to the next

#### Where-Object

-   Filters objects based on condition

`$_` = Current object being processed

Example:

``` powershell
$_.Name
```

Means: Name property of the current service.

#### Select

-   Displays only chosen properties

------------------------------------------------------------------------

## 3. What We Discovered

Service Name: rsEngineSvc\
State: Running\
StartMode: Auto\
Path:
C:`\Program `{=tex}Files`\ReasonLabs`{=tex}`\EPP`{=tex}`\rsEngineSvc`{=tex}.exe

Conclusion: - Installed in legitimate directory - Auto-start service -
Likely bundled antivirus (Potentially Unwanted Program) - Not stealth
malware

------------------------------------------------------------------------

## 4. Blue Team Investigation Flow

1.  Identify unknown process
2.  Check memory usage
3.  Check executable path
4.  Check service configuration
5.  Verify startup behavior
6.  Decide: Monitor / Remove / Escalate

------------------------------------------------------------------------

## 5. Important Blue Team Concepts Learned

-   Baseline creation
-   Service enumeration
-   Process-to-service correlation
-   Path validation
-   Understanding WMI & CIM queries
-   PowerShell pipeline logic

------------------------------------------------------------------------

End of Day 2 Notes Focus: Understanding Windows Services & Investigation
Methodology
