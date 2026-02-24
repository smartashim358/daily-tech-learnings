# Blue Team Learning Notes -- Day 1 (Process Monitoring & PowerShell Basics)

## 1. Enabling Process Creation Auditing

To log every new process creation (Event ID 4688):

``` powershell
auditpol /set /subcategory:"Process Creation" /success:enable
```

Purpose: - Enables logging of newly created processes. - Critical for
detecting malware execution.

------------------------------------------------------------------------

## 2. Viewing Security Logs

### View Latest Security Events

``` powershell
Get-WinEvent -LogName Security -MaxEvents 5
```

### Filter Only Process Creation Events (4688)

``` powershell
Get-WinEvent -LogName Security | Where-Object { $_.Id -eq 4688 } | Select -First 5
```

Concepts: - `$_` = Current object in pipeline - `.Id` = Event ID
property - `-eq` = Equal comparison

------------------------------------------------------------------------

## 3. Inspecting Event Object Structure

Store one event:

``` powershell
$event = Get-WinEvent -LogName Security | Where-Object { $_.Id -eq 4688 } | Select -First 1
```

View object structure:

``` powershell
$event | Get-Member
```

View event properties:

``` powershell
$event.Properties
```

Important Indexes (Event ID 4688):

  Index   Meaning
  ------- -------------------
  1       SubjectUserName
  5       NewProcessName
  13      ParentProcessName

Extract values:

``` powershell
$event.Properties[5].Value
$event.Properties[13].Value
```

------------------------------------------------------------------------

## 4. Writing a Basic PowerShell Script

Example script to extract parent-child processes:

``` powershell
$events = Get-WinEvent -LogName Security |
Where-Object { $_.Id -eq 4688 } |
Select-Object -First 5

foreach ($event in $events) {
    $newProcess = $event.Properties[5].Value
    $parentProcess = $event.Properties[13].Value

    Write-Output "New Process: $newProcess"
    Write-Output "Parent Process: $parentProcess"
    Write-Output "---------------------------"
}
```

Key Concepts: - Variables: `$events`, `$event` - Loop: `foreach` -
Object property access: `.Properties[index].Value`

------------------------------------------------------------------------

## 5. Running PowerShell Scripts

Save file as:

    process_check.ps1

Run:

``` powershell
.\process_check.ps1
```

If execution policy blocks:

``` powershell
Set-ExecutionPolicy RemoteSigned -Scope CurrentUser
```

------------------------------------------------------------------------

## 6. Administrator Mode

Open elevated PowerShell:

-   Press `Win`
-   Type `powershell`
-   Press `Ctrl + Shift + Enter`

Or from current shell:

``` powershell
Start-Process powershell -Verb runAs
```

Verify:

``` powershell
whoami
```

------------------------------------------------------------------------

## Core Concepts Learned Today

-   Process creation auditing (4688)
-   Event log filtering
-   Understanding PowerShell objects
-   Extracting structured event data
-   Writing and running PowerShell scripts
-   Administrator privilege basics

------------------------------------------------------------------------

End of Day 1 Notes
