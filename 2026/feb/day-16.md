# 📝 Cybersecurity & Networking Learning Tracker

This document tracks structured learning in Linux, Networking, and Ethical Security Testing.
All concepts include definitions, explanations, and practical examples for long-term memorization.

---

# 1. Networking Fundamentals

## 1.1 TTL (Time To Live)

**Definition:**  
TTL is a field inside an IP packet that limits how long the packet can travel in a network.  
Each router decreases TTL by 1. When TTL becomes 0, the packet is dropped.

**Formula:**

Hops = Default TTL - Observed TTL

**Example:**  
Default TTL = 64  
Observed TTL = 59  
Hops = 64 - 59 = 5  

This means the packet passed through 5 routers.

---

## 1.2 Packet Drop & ICMP

If TTL becomes 0 before reaching destination:
- Router drops the packet
- Router sends ICMP Time Exceeded message back

If destination is exactly 8 hops away:
- TTL must be at least 8
- If TTL < 8 → packet dropped before reaching target

---

## 1.3 Ping Command

**Purpose:** Test connectivity and measure latency.

Example:

```
ping 8.8.8.8
```

Shows:
- Round trip time
- Packet loss
- TTL value

---

## 1.4 MTR Command

**Definition:** Combination of ping + traceroute.

Example:

```
mtr -s 1500 8.8.8.8
```

Used to:
- Check each hop
- Detect packet loss per router
- Test different packet sizes

---

# 2. Linux System Learning

## 2.1 Important Directories

### /etc
System configuration files.

### /var
Logs, variable data, cache.

### /usr
User-installed applications and binaries.

---

## 2.2 Important Commands

### SSH

```
ssh user@ip_address
```

Example:

```
ssh kali@192.168.56.101
```

Used for secure remote login.

---

### IP Address Check

```
ip addr
```

Displays:
- Network interfaces
- Assigned IP addresses

---

### Remove Command

```
rm -r folder_name     # Delete folder recursively
rm -ri folder_name    # Delete interactively with confirmation
```

---

# 3. Nmap – Network Scanning

Nmap is used for network discovery and security auditing.

## 3.1 Basic Scan

```
nmap <target_ip>
```

Purpose:
- Discover open ports
- Identify active services

Example:

```
nmap 192.168.1.10
```

---

## 3.2 Service Version Detection

```
nmap -sV <target_ip>
```

Purpose:
- Detect service version running on open ports

Example:

```
nmap -sV 192.168.1.10
```

---

## 3.3 Aggressive Scan

```
nmap -A <target_ip>
```

Includes:
- OS detection
- Version detection
- Script scanning
- Traceroute

Example:

```
nmap -A 192.168.1.10
```

---

## 3.4 Scan Specific Ports

```
nmap -p 80,443 192.168.1.10
```

Scans only selected ports.

---

## 3.5 Scan All Ports

```
nmap -p- 192.168.1.10
```

Scans all 65535 ports.

---

# 4. Security Lab Practice

## CCTV Lab Scenario (Controlled Environment)

- Used two virtual machines
- Performed network scanning
- Identified open ports
- Understood password protection mechanisms

Goal:
Learn attack methods legally to understand defense strategies.

---

# 5. Memorization Strategy

1. Always calculate TTL manually.
2. Practice scanning in lab environment only.
3. Document every command:
   - Definition
   - Syntax
   - Example
4. Understand both attack and defense perspective.

---

# 6. Summary of Commands

| Command | Purpose |
|----------|----------|
| ping | Test connectivity |
| mtr | Trace network path |
| ssh | Remote login |
| ip addr | Show IP information |
| rm -r | Delete directory |
| nmap | Scan network |
| nmap -sV | Detect service versions |
| nmap -A | Aggressive scan |
| nmap -p- | Scan all ports |

---

Status: Learning Ongoing – Practical + Theory Combined

