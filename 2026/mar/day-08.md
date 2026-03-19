# Linux `top` Command - Complete Guide

## Overview
The `top` command is a real-time system monitoring utility in Linux. It displays running processes and system resource usage such as CPU, memory, and uptime.

---

## Basic Usage

```bash
top
```

- Starts interactive monitoring
- Press `q` to exit

---

## Process Fields Explained

| Field | Description |
|------|------------|
| PID | Process ID |
| USER | Owner of the process |
| PR | Priority (lower = higher priority) |
| NI | Nice value (lower = higher priority) |
| VIRT | Virtual memory used |
| RES | Physical RAM used |
| SHR | Shared memory |
| %CPU | CPU usage |
| %MEM | Memory usage |
| TIME+ | CPU time |
| COMMAND | Command name |

---

## Output Sections

### 1. System Summary
- Current time
- Uptime
- Logged-in users
- Load average (1, 5, 15 minutes)

### 2. Tasks
- Total processes
- Running
- Sleeping
- Stopped
- Zombie

### 3. CPU Usage
- us → User processes
- sy → System processes
- ni → Nice processes
- id → Idle
- wa → Waiting for I/O
- hi → Hardware interrupts
- si → Software interrupts
- st → Stolen CPU (VM)

### 4. Memory (RAM)
- Total
- Used
- Free
- Buff/Cache

### 5. Swap
- Total
- Used
- Free
- Available memory

---

## Common Options

```bash
top -v            # Show version
top -p <PID>      # Monitor specific process
top -b -n 1       # Batch mode (for scripts)
top -1            # Per-core CPU usage
top -h            # Help
top -n 10         # Exit after 10 updates
top -u username   # Show user processes
top -d 2          # Refresh every 2 seconds
```

---

## Interactive Controls

| Key | Action |
|-----|-------|
| q | Quit |
| k | Kill process |
| r | Change priority (renice) |
| z | Toggle colors |
| c | Show full command path |
| Shift + P | Sort by CPU |
| A | Alternate display mode |

---

## Useful Tips

- Use `top -p PID` to track a specific process
- Use `Shift + P` to find high CPU processes
- Use `z` for better visibility
- Use batch mode (`-b`) for logging

---

## Alternatives

| Tool | Description |
|------|------------|
| htop | Interactive and user-friendly |
| glances | Full system monitoring |
| nmon | Performance monitoring |
| atop | Advanced tracking with history |
| dstat | Combined resource stats |
| sar | Historical system data |

---

## Summary
- `top` provides real-time system monitoring
- Helps identify resource-heavy processes
- Supports interactive process management
- Essential for Linux system administration

