#  Linux `ps` Command – Professional Guide

##  Overview
The `ps` (process status) command in Linux is used to display information about **currently running processes**. It provides a **snapshot** of system processes at the moment of execution.

### 🔹 Key Uses
- View running processes
- Identify Process IDs (PIDs)
- Monitor CPU and memory usage
- Inspect background services (daemons)
- Filter processes by user, PID, terminal, or command

---

##  Basic Syntax
```bash
ps [options]
```

---

##  Default Behavior
```bash
ps
```
Displays processes running in the **current terminal session**.

### Output Fields
- **PID** → Process ID
- **TTY** → Terminal
- **TIME** → CPU time used
- **CMD** → Command name

---

##  Important `ps` Options

### 1. Show All Processes
```bash
ps -e
# or
ps -A
```
Displays all running processes in the system.

---

### 2. Full Format Output
```bash
ps -ef
```
Shows detailed information including:
- Parent PID (PPID)
- User
- Start time

---

### 3. Filter by User
```bash
ps -u username
```
Example:
```bash
ps -u root
```

---

### 4. Show Background Processes (No TTY)
```bash
ps -x
```
Useful for viewing **services and daemons**.

---

### 5. Processes with Terminal (All Users)
```bash
ps -a
```
Excludes session leaders.

---

### 6. Filter by PID
```bash
ps -p 1
ps -p 1,2,3
```

---

### 7. Process Tree View
```bash
ps -ef --forest
```
Displays parent-child process relationships.

---

### 8. Exclude Processes
```bash
ps -a -N
```
Shows processes that **do NOT match criteria**.

---

### 9. Detailed System Snapshot
```bash
ps aux
```
Includes:
- CPU usage
- Memory usage
- Process owner
- Command

---

### 10. Current Terminal Processes
```bash
ps -T
```

---

### 11. Filter by Command Name
```bash
ps -C systemd
```

---

### 12. Filter by Group
```bash
ps -G root
ps -g 1
```

---

##  Process Monitoring Tools (Beyond `ps`)

### 1. `top` – Real-Time Monitoring
```bash
top
```
- Live process updates
- CPU & memory usage
- Interactive process management

---

### 2. `htop` – Advanced Interactive Viewer
```bash
htop
```
- User-friendly UI
- Search & filter processes
- Color-coded metrics

---

### 3. `atop` – Advanced System Monitoring
```bash
sudo apt install atop
atop
```
- CPU, memory, disk, network stats
- Historical logging

---

### 4. `pgrep` – Find Process IDs
```bash
pgrep process_name
```
Example:
```bash
pgrep systemd
```

Use with `ps`:
```bash
ps -p <PID>
```

---

##  Pro Tips
- Use `ps aux | grep <name>` to quickly find processes
- Combine options for powerful filtering
- Use `top` or `htop` for real-time monitoring
- Use `pgrep` in scripts for automation

---

##  Summary
The `ps` command is a **core Linux tool** for process management. It provides a quick snapshot of system activity and is essential for:

- System monitoring
- Troubleshooting
- Process control

---

 Keep practicing with combinations like:
```bash
ps aux | grep nginx
ps -ef --forest
ps -u $(whoami)
```

