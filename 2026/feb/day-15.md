# Learning Notes Author: Ashim Nepali Topic: mtr Command Deep Study



## Definition

mtr stands for My Traceroute. It is a network diagnostic tool that
combines the functionality of ping and traceroute. It continuously sends
packets to a destination and measures the route taken and performance of
each hop.

Core Purpose

mtr is used to analyze network paths between the local machine and a
remote host. It helps detect:

Packet loss Latency issues Network congestion Routing instability

How mtr Works

mtr sends a sequence of ICMP Echo Requests or UDP packets to a
destination. Each router along the path responds with timing
information. mtr continuously updates statistics, allowing real-time
monitoring of:

Round-trip time Packet loss percentage Number of transmitted packets
Best, worst, and average latency

Basic Usage

```bash
mtr google.com
```

This command starts interactive mode. It shows live hop-by-hop
statistics.

Key Columns in Output

Loss% Percentage of packets lost at each hop.

Snt Number of packets sent.

Last Latency of the most recent packet.

Avg Average round-trip time.

Best Lowest recorded latency.

Wrst Highest recorded latency.

StDev Standard deviation of latency.

## Advanced Options

1. Report Mode

 ```bash mtr -r google.com ```

Runs mtr once and prints a summary report instead of live display.

2. Set Packet Count

```bash mtr -r -c 10 google.com ```

Sends exactly 10 packets per hop and prints summary.

3. Change Packet Size

```bash mtr -s 200 google.com```

Sends packets of 200 bytes. Useful for testing MTU or fragmentation
issues.

4. Set Interval Between Packets

```bash mtr -i 2 google.com```

Sends one packet every 2 seconds.

5. Use TCP Instead of ICMP

```bash mtr -T google.com```

Uses TCP packets instead of ICMP. Useful when ICMP is blocked by
firewall.

6. Use Specific Port

```bash mtr -T -P 443 google.com```

Sends TCP packets to port 443.

7. Numeric Output Only

```bash mtr -n google.com```

Prevents DNS resolution. Shows only IP addresses. Faster and useful in
troubleshooting.

## Practical Case Scenarios

**Detect Packet Loss**

If Loss% increases at a specific hop and continues afterward, the
problem may originate from that router or beyond.

**Detect High Latency**

If Avg time increases significantly at a hop and remains high,
congestion may exist at that point.

**Firewall Restrictions**

If no response appears after first hop, ICMP may be blocked. Using -T
option may bypass that limitation.

**Professional Understanding**

**mtr** is superior to ping because it reveals intermediate network nodes.
It is superior to traceroute because it provides continuous statistics
instead of single measurements.

It is a critical tool for system administrators, DevOps engineers, and
backend engineers diagnosing distributed systems.

Learning Reflection

Understanding mtr builds foundational knowledge in networking. It
connects system administration, infrastructure reliability, and backend
performance monitoring.

End of today's notes.
