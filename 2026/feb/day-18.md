# Nmap -- Deep Technical & Conceptual Notes

Author: Ashim Nepali\
Topic: Network Reconnaissance & Security Analysis

------------------------------------------------------------------------

# 1. Introduction to Nmap

Nmap (Network Mapper) is an open-source network scanning and
reconnaissance tool used for: - Network discovery - Port scanning -
Service detection - Operating system fingerprinting - Vulnerability
assessment

Nmap works by crafting raw packets and analyzing responses. It does not
"hack" systems by default; rather, it observes how systems respond to
network probes.

Understanding Nmap requires understanding TCP/IP networking
fundamentals.

------------------------------------------------------------------------

# 2. Host Discovery

## nmap -sn 192.168.1.0/24

Purpose: Determines which hosts are alive in a network.

Technical Mechanism: - Sends ICMP Echo Requests (Ping) - May use ARP
requests on local networks - Observes responses

Concept: Before analyzing services, we must identify active devices.
This is called surface mapping.

Security Perspective: - Detect unauthorized devices - Build asset
inventory

------------------------------------------------------------------------

## nmap -sL 192.168.1.0/24

Purpose: Lists IP addresses in a subnet without sending packets.

Concept: Pure enumeration without interaction.

Use Case: Planning scan strategy without generating traffic.

------------------------------------------------------------------------

# 3. TCP Port Scanning

Ports are logical communication endpoints. Each port may run a service.

Default Nmap scans only top 1000 common ports.

------------------------------------------------------------------------

## nmap -sS Target

SYN Scan (Half-Open Scan)

Technical Explanation: 1. Sends SYN packet 2. If SYN-ACK received → port
open 3. Sends RST to terminate connection

Why It Matters: Does not complete full handshake. Less likely to be
logged by basic systems.

Security Insight: Half-open connection detection should be enabled in
IDS/IPS.

------------------------------------------------------------------------

## nmap -p- Target

Scans all 65535 TCP ports.

Why Important: Some services run on non-standard ports. Backdoors often
hide on uncommon ports.

------------------------------------------------------------------------

## nmap -sU Target

UDP Scan

UDP is connectionless. No handshake mechanism.

Common UDP Services: - DNS (53) - SNMP (161) - NTP (123)

Challenge: Slower and harder to detect open ports because lack of
response may mean open or filtered.

------------------------------------------------------------------------

## nmap -sX Target

Xmas Scan

Sends FIN, PSH, URG flags simultaneously.

Purpose: Firewall evasion testing.

------------------------------------------------------------------------

## nmap -sA Target

ACK Scan

Used to determine: - Filtered vs Unfiltered ports - Firewall rule
behavior

Does not directly determine open ports.

------------------------------------------------------------------------

## nmap -sW Target

Window Scan

Variant of ACK scan. Analyzes TCP window size to infer port state.

------------------------------------------------------------------------

# 4. Service and Version Detection

## nmap -sV Target

Determines service versions by sending protocol-specific probes.

Example Output: - Apache 2.4.49 - OpenSSH 8.2

Importance: Vulnerabilities depend on version number.

------------------------------------------------------------------------

## nmap -O Target

Operating System Detection

Uses TCP/IP stack fingerprinting: - TTL values - Window sizes - Packet
behavior

Each OS has subtle networking differences.

------------------------------------------------------------------------

## nmap -A Target

Aggressive Scan

Includes: - OS detection - Version detection - Script scanning -
Traceroute

Very noisy. Should be used in authorized testing environments only.

------------------------------------------------------------------------

## nmap -Pn Target

Skips host discovery. Assumes host is alive.

Useful when ICMP is blocked by firewall.

------------------------------------------------------------------------

# 5. Nmap Scripting Engine (NSE)

NSE allows automation of: - Vulnerability detection - Misconfiguration
discovery - Service enumeration

------------------------------------------------------------------------

## --script vuln

Runs vulnerability detection scripts.

Purpose: Checks for known CVEs and insecure configurations.

------------------------------------------------------------------------

# SMB Enumeration Scripts

Used primarily against Windows or Samba servers.

## smb-enum-shares

Lists accessible shared folders.

Risk: Sensitive file exposure.

------------------------------------------------------------------------

## smb-vuln-ms17-010

Detects EternalBlue vulnerability.

Impact: Remote code execution vulnerability in older Windows systems.

------------------------------------------------------------------------

## smb-vuln-cve-2017-7494

Checks Samba remote code execution flaw.

------------------------------------------------------------------------

## smb-vuln-ms08-067

Old RPC vulnerability in Windows systems.

------------------------------------------------------------------------

## smb-vuln-ms10-061

Print Spooler vulnerability.

------------------------------------------------------------------------

## smb-vuln-regsvc-dos

Registry service denial-of-service vulnerability.

------------------------------------------------------------------------

# 6. Web Enumeration Scripts

## http-enum

Enumerates common directories: - /admin - /login - /backup

Purpose: Discover hidden administrative interfaces.

------------------------------------------------------------------------

## http-methods

Lists allowed HTTP methods: - GET - POST - PUT - DELETE

Security Concern: PUT or DELETE enabled may allow unauthorized file
upload or deletion.

------------------------------------------------------------------------

## http-title

Retrieves webpage title. Helps identify web applications.

------------------------------------------------------------------------

## http-headers

Retrieves HTTP headers. May reveal: - Server software - Technology
stack - Security configurations

------------------------------------------------------------------------

## http-auth

Identifies authentication methods. Helps determine login protection
mechanisms.

------------------------------------------------------------------------

## http-sql-injection

Tests for SQL injection vulnerabilities using scripts.

Warning: Only use on systems you own or have permission to test.

------------------------------------------------------------------------

# 7. Professional Recon Workflow

1.  Identify live hosts
2.  Scan common ports
3.  Scan all ports if necessary
4.  Identify service versions
5.  Detect operating system
6.  Run targeted vulnerability scripts
7.  Validate findings
8.  Document findings professionally

------------------------------------------------------------------------

# 8. Ethical and Legal Responsibility

Nmap must only be used in: - Personal lab environments - Authorized
penetration tests - Educational platforms - Capture The Flag
environments

Unauthorized scanning may violate laws.

------------------------------------------------------------------------

# 9. Final Conceptual Understanding

Nmap is not about attacking. It is about understanding exposure.

True expertise lies in: - Interpreting packet behavior - Understanding
networking theory - Thinking defensively

Security mastery comes from understanding how systems communicate at the
protocol level.
