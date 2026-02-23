# PowerShell & Network Management for Ethical Hacking

**Date:** 2026-02-22  
**Topic:** Network Management & PowerShell in Ethical Hacking

---

## 1. Checking Network Interfaces

Command to view all network interfaces:
```powershell
netsh interface show interface
```

**Output Meaning:**
| Admin State | State       | Interface Name |
|-------------|------------|----------------|
| Enabled     | Connected  | Ethernet 2     |
| Enabled     | Disconnected | Wi-Fi 2      |
| Enabled     | Connected  | VMware VMnet1  |
| Enabled     | Connected  | VMware VMnet8  |

- **Connected** → currently active network
- **Disconnected** → not connected
- VMware adapters → virtual networks, used by VMs only

**Key Takeaway:** The main internet connection is usually **Ethernet 2** if connected.

---

## 2. Enabling / Disabling Network Adapters

### Using PowerShell
**Enable Network Adapter:**
```powershell
netsh interface set interface "Interface Name" admin=enabled
```
**Disable Network Adapter:**
```powershell
netsh interface set interface "Interface Name" admin=disabled
```

**Example:**
```powershell
netsh interface set interface "Wi-Fi 2" admin=enabled
netsh interface set interface "VMware Network Adapter VMnet1" admin=disabled
```

### Using GUI
1. Press **Win + R** → type `ncpa.cpl` → Enter
2. Right-click adapter → **Enable / Disable**

**Tip:** Do not disable your main internet adapter accidentally.

---

## 3. Viewing Saved Wi-Fi Passwords (Legal)

Only works for networks previously connected:
```powershell
# List saved Wi-Fi profiles
netsh wlan show profiles

# Show password of a profile
netsh wlan show profile name="WiFi_Name" key=clear
```
- Look for **Key Content** → this is the password

**Important:** If the password has changed and was never entered on the PC, it cannot be retrieved.

---

## 4. PowerShell in Ethical Hacking

**Legal Uses:**
1. **Network Reconnaissance**
   ```powershell
ipconfig /all        # View IPs
netstat -ano         # Active connections
Test-NetConnection google.com -Port 443 # Port test
```
2. **System Enumeration**
   ```powershell
Get-Process          # Running processes
Get-LocalUser        # Users
Get-ItemProperty HKLM:\Software\Microsoft\Windows\CurrentVersion\Uninstall\* # Installed programs
```
3. **Active Directory / Enterprise Auditing**
   - List users, groups, permissions (legal, for pentesting environments)
4. **Log Analysis**
   ```powershell
Get-EventLog -LogName Security
```
   - Detect failed logins, suspicious activity
5. **Automation & Scripting**
   - Automate scans, reports, monitoring

**Key Point:** PowerShell is powerful for Windows environments; attackers and defenders both use it.

**Tools That Use PowerShell:**
- PowerSploit
- Empire
- Metasploit (Windows modules)

**Future-Proof Tip:** Always practice on **your own network / lab / legal CTF platforms**.

---

## 5. Wi-Fi Password Changes

- If the router password changes, **old password no longer works**
- Devices previously connected may stay connected until reboot or disconnect
- To reconnect, enter the **new password**
- Windows only knows passwords previously entered and saved

**Router Recovery (Legal):**
- Log in to router admin panel (192.168.x.x)
- Check Wireless Settings or reset router physically

---

**Summary / Takeaways:**
- Use `netsh` and PowerShell to manage and check networks
- Enable/Disable adapters safely
- View only **your saved Wi-Fi passwords**, never crack unknown networks
- PowerShell is powerful for ethical hacking when used for reconnaissance, enumeration, and automation
- Always practice in **legal environments**

---

**End of Notes**

