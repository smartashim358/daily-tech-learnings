
# SOC Engineering notes:

# Windows Event ID 4624 -- Successful Logon

------------------------------------------------------------------------

# 1. Definition

Event ID 4624 is generated when a logon session is successfully created
on a Windows system.

Log Location: - Log Name: Security - Source:
Microsoft-Windows-Security-Auditing

Core Meaning: Event 4624 represents successful authentication and access
token creation.

------------------------------------------------------------------------

# 2. Internal Authentication Architecture

Authentication Flow:

User Input → Winlogon → LSASS → Authentication Package (Kerberos / NTLM)
→ Access Token Created → Logon Session Established → Event 4624 Logged

## Core Components

  Component         Role
  ----------------- ----------------------------------
  Winlogon.exe      Handles interactive login
  LSASS.exe         Validates credentials
  Kerberos / NTLM   Authentication protocol
  Access Token      Contains identity and privileges
  Logon Session     Security context container

Important Concept: No access token = No system access.

------------------------------------------------------------------------

# 3. Event Structure Breakdown

## 3.1 Subject Section

Indicates which account initiated the logon process.

Common Value: SYSTEM (LSASS context)

Key Fields: - SubjectUserSid - SubjectUserName - SubjectLogonId

------------------------------------------------------------------------

## 3.2 New Logon Section (Critical Section)

Represents the actual logged-in user.

  Field            Description
  ---------------- ---------------------------
  Security ID      SID of user
  Account Name     Username
  Account Domain   Domain or local system
  Logon ID         Unique session identifier

Logon ID is used to correlate: - 4624 (Logon) - 4634 (Logoff) - 4672
(Privilege assignment) - 4688 (Process creation)

------------------------------------------------------------------------

## 3.3 Logon Type (Detection Critical)

  Logon Type   Meaning
  ------------ ------------------------------
  2            Interactive (keyboard login)
  3            Network (SMB, file share)
  4            Batch (Scheduled task)
  5            Service
  7            Unlock
  8            NetworkCleartext
  9            NewCredentials
  10           RemoteInteractive (RDP)
  11           CachedInteractive

Security Notes:

-   Type 3 at unusual hours → Possible lateral movement
-   Type 9 → Credential abuse
-   Type 10 → Remote access monitoring required
-   Service accounts using Type 2 → Suspicious

------------------------------------------------------------------------

# 4. Authentication Package

Indicates which protocol handled authentication.

  Value                                   Meaning
  --------------------------------------- -----------------------
  Kerberos                                Domain authentication
  NTLM                                    Legacy authentication
  Negotiate                               Automatic selection
  MICROSOFT_AUTHENTICATION_PACKAGE_V1_0   Local login

Detection Insight: Unexpected NTLM usage in domain environments should
be reviewed.

------------------------------------------------------------------------

# 5. Network Information Section

Key Fields: - Workstation Name - Source Network Address - Source Port

Indicators:

-   Source IP not equal to 127.0.0.1 → Remote login
-   Blank Source IP → Local login

------------------------------------------------------------------------

# 6. Process Information

Identifies the process that initiated the logon.

Legitimate Example:
C:`\Windows`{=tex}`\System32`{=tex}`\winlogon`{=tex}.exe

High-Risk Examples: cmd.exe powershell.exe

Unexpected initiating processes require investigation.

------------------------------------------------------------------------

# 7. Investigation Workflow

Standard Correlation Model:

1.  Identify Event 4624
2.  Extract Logon ID
3.  Search Event 4672 (Privilege Assignment)
4.  Search Event 4688 (Process Creation)
5.  Confirm Event 4634 (Logoff)

This builds a full authentication timeline.

------------------------------------------------------------------------

# 8. PowerShell Investigation Commands

## Retrieve 4624 Events

``` powershell
Get-WinEvent -FilterHashtable @{
    LogName='Security'
    Id=4624
}
```

## Filter Remote Desktop Logins (Type 10)

``` powershell
Get-WinEvent -FilterHashtable @{
    LogName='Security'
    Id=4624
} | Where-Object {
    $_.Message -match "Logon Type:\s+10"
}
```

## Identify Events with Source Network Address

``` powershell
Get-WinEvent -FilterHashtable @{
    LogName='Security'
    Id=4624
} | Where-Object {
    $_.Message -match "Source Network Address"
}
```

------------------------------------------------------------------------

# 9. Example Compromise Pattern

-   4624 (Type 10 - RDP)
-   4672 (Special privileges assigned)
-   4688 (cmd.exe or powershell.exe execution)

This sequence may indicate remote compromise.

------------------------------------------------------------------------

# 10. Key Takeaways

-   Event 4624 confirms successful authentication.
-   Logon Type defines access method.
-   Logon ID enables event correlation.
-   Authentication Package reveals protocol used.
-   Network fields help detect lateral movement.
-   Always correlate with related security events.

------------------------------------------------------------------------

End of Study Notes
