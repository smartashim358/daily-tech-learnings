# Linux Process & PID Management (Backend Core)

Clean, practical notes on finding and managing **PIDs (Process IDs)** in Linux.  
Focused only on what is required for **backend development and hosting**.

---

## 1. What is PID 
**PID (Process ID)** is a unique number assigned to every running process.

Used to:
- Stop backend apps
- Fix port conflicts
- Manage running services

---

## 2. Find PID by Application Name

### Using `ps`
```bash
ps aux | grep node
```

Example:
```
ubuntu   24567  0.2  node server.js
```

- `24567` → PID
- Ignore the `grep` line

---

### Using `pgrep` (preferred)
```bash
pgrep node
```

With command details:
```bash
pgrep -fl node
```

Use when:
- You know the process name (node, nginx, pm2, mongo)

---

## 3. Find PID by Port (Most Important for Backend)

```bash
lsof -i :3000
```

Example:
```
node   24567 user   TCP *:3000 (LISTEN)
```

- `24567` → PID using port `3000`

Used when:
- Port already in use
- App not starting

---

### Alternative
```bash
netstat -tulpn | grep 3000
```

---

## 4. Find PID of System Services

```bash
systemctl status nginx
```

Example:
```
Main PID: 1234 (nginx)
```

Used for:
- Nginx
- Redis
- MySQL
- SSH

---

## 5. Live Process Monitoring

```bash
top
```

Better:
```bash
htop
```

Used to:
- Check CPU usage
- Check memory usage
- Identify stuck processes

Exit with:
```bash
q
```

---

## 6. Find Exact PID

```bash
pidof nginx
```

Output:
```
1234 1235
```

Multiple PIDs = worker processes.

---

## 7. Kill a Process

Normal stop:
```bash
kill PID
```

Force stop:
```bash
kill -9 PID
```

Use `-9` only if normal kill fails.

---

## 8. Backend Practical Flow

```bash
node server.js
pgrep -fl node
kill PID
lsof -i :3000
```

No output from `lsof` = port is free.

---

## 9. PM2 Rule

Do NOT kill Node processes manually when using PM2.

Correct way:
```bash
pm2 list
pm2 stop app_name
pm2 restart app_name
```

---

## 10. Quick Reference

| Task | Command |
|-----|--------|
| Find by name | `pgrep -fl app` |
| Find by port | `lsof -i :PORT` |
| Service PID | `systemctl status service` |
| Monitor | `top` / `htop` |
| Kill | `kill PID` |

---
