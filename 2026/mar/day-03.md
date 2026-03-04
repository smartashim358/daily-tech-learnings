# Event ID 4672 – Privileged Logon Detection Engineering

## Objective

Understand how Windows logs privileged logons and how to build detection logic using Event ID 4672.

---

## 1. What is Event ID 4672

Event ID 4672 is generated when a user logs on and is assigned special privileges.

Log Location:
Event Viewer → Windows Logs → Security

Event Message:
Special privileges assigned to new logon

This event indicates that the logged-in account has high-level privileges.

---

## 2. Why It Is Important

Privileged accounts are high-value targets.

Event 4672 helps detect:
- Administrator logons
- SYSTEM account usage
- Privilege escalation
- Lateral movement
- Service abuse

Important:
Event 4672 alone is not malicious. It must be correlated with other events.

---

## 3. Common Privileges in 4672

Examples of powerful privileges:
- SeDebugPrivilege
- SeBackupPrivilege
- SeRestorePrivilege
- SeTakeOwnershipPrivilege
- SeTcbPrivilege

These privileges allow deep system-level access.

---

## 4. Key Fields to Analyze

Subject Section:

Security ID (SID)  
Unique identifier of the account

Account Name  
User who logged in

Account Domain  
Domain or local system

Logon ID  
Used to correlate with Event ID 4624

---

## 5. Required Event Correlation

Event 4672 should be analyzed with:

| Event ID | Purpose |
|-----------|----------|
| 4624 | Successful logon |
| 4688 | Process creation |
| 4648 | Explicit credential logon |
| 4697 | Service installation |

Example Detection Logic:

4624 (LogonType = 10)  
AND 4672  
AND Account not expected admin  
→ Alert

---

## 6. Important Logon Types

| Logon Type | Meaning |
|-------------|----------|
| 2 | Interactive |
| 3 | Network |
| 10 | Remote Interactive (RDP) |

High-risk combinations:
- LogonType 3 or 10 with 4672
- Service accounts logging in interactively
- Off-hours privileged logon

---

## 7. Detection Strategy

Step 1: Enable Audit Policy

Local Security Policy  
Advanced Audit Policy  
Logon/Logoff  
Audit Special Logon  
Enable Success

Step 2: Hunt for Anomalies

Basic SIEM Logic:

EventID = 4672  
AND AccountName != SYSTEM  
AND LogonType IN (3,10)

---

## 8. Normal vs Suspicious Activity

Normal:
- SYSTEM at startup
- Administrator during working hours
- Planned maintenance activity

Suspicious:
- Privileged logon at unusual time
- New admin account usage
- Service account interactive login
- Remote privileged access from unknown host

---

## 9. Attack Flow Example

1. Initial access  
2. Credential dumping  
3. Privilege escalation  
4. Event 4672 generated  
5. Malicious process execution (4688)  
6. Lateral movement or ransomware  

Missing correlation may result in missed early detection.

---

## Key Takeaways

- Event 4672 indicates privileged logon
- It is a high-value signal
- It must be correlated with 4624 and 4688
- Critical for detecting privilege escalation and lateral movement
- Important early indicator in ransomware investigations