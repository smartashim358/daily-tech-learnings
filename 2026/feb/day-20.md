# Remote Desktop & Network Setup Guide for Windows

This guide explains how to **rename your PC, set a static IP, and manage Remote Desktop Connection** in Windows. It is designed for beginners, students, and IT learners. All steps are professional and ready for GitHub notes.

---

## 1. Rename Your PC
Renaming your PC helps you identify it easily on networks.

**Steps:**
1. Press **Windows + I** to open **Settings**.
2. Go to **System** → **About**.
3. Click **Rename this PC**.
4. Enter a new name (e.g., `ASHIM-PC`).
   - Use letters and numbers only
   - No spaces or special characters
5. Click **Next**.
6. Restart your PC for changes to take effect.

**Tip:** Choose meaningful names if you manage multiple PCs (e.g., `OFFICE-PC01`, `HOME-LAPTOP`).

---

## 2. Change to a Static IP
Static IP ensures your PC always uses the same IP, which is useful for **Remote Desktop** and network management.

### Steps to Set Static IP:

1. Press **Windows + R**, type `ncpa.cpl`, press **Enter**.
2. Right-click your active network adapter (Wi-Fi/Ethernet) → **Properties**.
3. Double-click **Internet Protocol Version 4 (TCP/IPv4)**.
4. Select **Use the following IP address**.
5. Enter the following example values:

| Field | Example |
|-------|---------|
| IP Address | 192.168.1.50 |
| Subnet Mask | 255.255.255.0 |
| Default Gateway | 192.168.1.1 |
| Preferred DNS | 8.8.8.8 |
| Alternate DNS | 8.8.4.4 |

6. Click **OK** → Close.

**Tips:**
- Make sure the static IP is in the same network range as your router.
- Avoid IP conflicts by choosing an unused number.
- To check current IP and gateway: `Windows + R` → `cmd` → `ipconfig`.

---

## 3. Enable Remote Desktop Connection (RDC)
RDC allows you to **access and control your PC remotely**.

### Steps to Enable RDC:

1. Press **Windows + I** → **System** → **Remote Desktop**.
2. Turn **On** **Enable Remote Desktop**.
3. Note the **PC Name** or **Static IP** to connect.
4. Ensure your **Firewall allows Remote Desktop**.

### Connect from Another PC:
1. Open **Remote Desktop Connection** on another Windows PC.
2. Enter the **PC Name or Static IP**.
3. Enter **username and password**.
4. You are now connected and can control the PC remotely.

### Remote Power Options:
| Action | How |
|--------|-----|
| Shutdown / Restart | Start → Power → Shut down / Restart (while connected) |
| Log off | Start → Sign out |
| Turn on PC remotely | Requires **Wake-on-LAN** setup in BIOS and adapter, then send WoL packet |

**Tip:** For low RAM PCs (like 4GB), use **lightweight browsers and sleeping tabs** during RDC to keep system fast.

---

## 4. Best Practices
- Always assign **Static IP** for PCs you want to access via RDC.
- Use meaningful **PC names** for easy identification.
- Limit unnecessary apps during remote sessions to save memory.
- Enable **Firewall** and strong passwords for security.
- Combine with **Brave Memory Saver** or **Edge Sleeping Tabs** on your local PC to reduce memory usage.

