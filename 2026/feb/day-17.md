# TCP 3-Way Handshake -- Professional Networking & Security Notes

## Overview

The TCP 3-Way Handshake is the foundational mechanism used by the
Transmission Control Protocol (TCP) to establish a reliable,
connection-oriented communication session between a client and a server.

Understanding this process is critical for: - Network engineering -
Cybersecurity analysis - Firewall configuration - Intrusion detection -
Advanced attack detection (e.g., SYN flood, stealth scans)

Mastery of TCP behavior is essential for becoming a high-level security
engineer.

------------------------------------------------------------------------

# 1. What is TCP?

TCP (Transmission Control Protocol) is a transport-layer protocol that
provides:

-   Reliable data transmission
-   Ordered delivery of packets
-   Error checking and recovery
-   Flow control
-   Congestion control
-   Connection-oriented communication

Unlike UDP, TCP requires a connection to be established before any data
is transmitted.

Common protocols that rely on TCP: - HTTP / HTTPS - SSH - FTP - SMTP

------------------------------------------------------------------------

# 2. Why Does TCP Need a Handshake?

Before exchanging data, both client and server must:

-   Agree to communicate
-   Synchronize sequence numbers
-   Allocate system resources (memory buffers, sockets)
-   Confirm bidirectional communication

This negotiation process is called the **3-Way Handshake**.

------------------------------------------------------------------------

# 3. The TCP 3-Way Handshake (Step-by-Step)

Assume:

Client initial sequence number = 1000\
Server initial sequence number = 5000

## Step 1 -- SYN (Client → Server)

The client initiates the connection by sending a SYN packet.

Example: Client → Server\
SYN = 1\
Sequence Number = 1000

Meaning: "I want to start a connection."

Important: The SYN flag consumes one sequence number.

------------------------------------------------------------------------

## Step 2 -- SYN-ACK (Server → Client)

The server responds with both SYN and ACK flags set.

Example: Server → Client\
SYN = 1\
ACK = 1\
Sequence Number = 5000\
Acknowledgment Number = 1001

Why ACK = 1001?

Because: 1000 (client sequence) + 1 (SYN consumes one number)

Meaning: "I received your SYN. Here is my sequence number."

------------------------------------------------------------------------

## Step 3 -- ACK (Client → Server)

The client acknowledges the server's sequence number.

Example: Client → Server\
ACK = 1\
Acknowledgment Number = 5001

Meaning: "I received your response. Connection established."

At this point, the TCP connection state becomes:

ESTABLISHED

Data transmission begins.

------------------------------------------------------------------------

# 4. Visual Representation

Client Server \| ---- SYN (1000) ----------\> \| \| \<--- SYN-ACK
(5000,1001) --- \| \| ---- ACK (5001) ----------\> \|

Connection Established

------------------------------------------------------------------------

# 5. TCP Flags Explained

TCP uses control flags inside its header:

-   SYN → Synchronize sequence numbers
-   ACK → Acknowledge received data
-   FIN → Graceful connection termination
-   RST → Forcefully reset connection
-   PSH → Push data immediately to application
-   URG → Urgent pointer field valid

Security engineers must understand these flags to detect abnormal
behavior.

------------------------------------------------------------------------

# 6. TCP Connection States (Linux Perspective)

You can observe TCP states using:

    ss -ant

Common states:

LISTEN → Server waiting for connection\
SYN-SENT → Client sent SYN\
SYN-RECV → Server received SYN, waiting for ACK\
ESTABLISHED → Connection active\
FIN-WAIT → Closing initiated\
TIME-WAIT → Waiting before full closure\
CLOSE-WAIT → Waiting for application to close

Understanding states is critical for firewall and intrusion detection
analysis.

------------------------------------------------------------------------

# 7. Security Implications

## SYN Flood Attack

Attack scenario:

Attacker sends multiple SYN packets\
Server replies with SYN-ACK\
Attacker never sends final ACK

Result: Server connections remain in SYN-RECV state\
Memory resources get exhausted\
Leads to Denial of Service (DoS)

------------------------------------------------------------------------

## Defensive Mechanisms

-   SYN cookies
-   Rate limiting
-   Stateful firewall tracking
-   IDS/IPS monitoring
-   Load balancer filtering

------------------------------------------------------------------------

# 8. Nmap and Half-Open Scanning

Command:

    nmap -sS target_ip

This performs a SYN scan:

1.  Sends SYN
2.  Receives SYN-ACK
3.  Sends RST instead of ACK

Connection never fully establishes.

This is called a Half-Open Scan and is stealthier than full TCP connect
scan.

------------------------------------------------------------------------

# 9. Practical Lab

On Kali Linux:

Check active connections:

    ss -ant

Open a browser and visit a website.

Run again:

    ss -ant

Observe new ESTABLISHED connections.

This demonstrates live TCP handshake activity.

------------------------------------------------------------------------

# 10. Key Takeaways

-   TCP is connection-oriented and reliable.
-   The 3-way handshake synchronizes communication.
-   SYN consumes one sequence number.
-   Attackers abuse handshake mechanisms.
-   Security engineers must understand TCP states deeply.
-   Monitoring TCP behavior is fundamental for network defense.

------------------------------------------------------------------------

# Conclusion

The TCP 3-Way Handshake is not just a networking concept --- it is the
foundation of transport-layer security analysis.

Mastering this topic enables deeper understanding of:

-   Firewall state tracking
-   Intrusion detection systems
-   DoS attack mechanics
-   Port scanning techniques
-   Packet-level traffic analysis


